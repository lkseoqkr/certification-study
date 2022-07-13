# Typical identity management in the cloud
- resources in the cloud
- identities (human and non-human) that need to access those resources and perform actions
# Cloud Identity and Access Management (IAM)
- Authentication (is it the right user?) and
- Authorization (do they have the right access?)
- Identities can be
  - A GCP User (Google Account or Externally Authenticated U
  - A Group of GCP Users
  - An Application running in GCP
  - An Application running in your data center
  - Unauthenticated users
- Provides very granular control
  - Limit a single user:
    - to perform single action
    - on a specific cloud resource
    - from a specific IP address
    - during a specific time window
# Cloud IAM Example
- I want to provide access to manage a specific cloud storage bucket to a colleague of mine:
  - General
    - Member: My colleague
    - Resource: Specific cloud storage bucket
    - Action: Upload/Delete Objects
  - In Google Cloud IAM:
    - Roles: A set of permissions
    - How do you assign permissions to a member?
# IAM - Roles
- Roles are Permissions
- Three Types
  - Basic Roles (or Primitive roles) - Owner/Editor/Viewer
    - Viewer(roles.viewer) - Read-only actions
    - Editor(roles.editor) - Viewer + Edit actions
    - Owner(roles.owner) - Editor + Manage Roles and Permissions + Billing
    - NOT RECOMMENDED: Don't use in production
  - Predefined Roles - Fine grained roles predefined and managed by Google
  - Custom Roles - When predefined roles are NOT sufficient, you can create your own
# IAM - Predefined Roles - Example Permissions
- Important Cloud Storage Roles
  - Storage Admin (roles/storage.admin)
    - storage.buckets.*
    - storage.objects.*
  - Storage Object Admin (roles/storage.objectAdmin)
    - storage.objects.*
  - Storage Object Creator (roles/storage.objectCreator)
    - storage.objects.create
  - Storage Object Viewer (roles/storage.objectViewer)
    - storage.objects.get
    - storage.objects.list
- All four roles have these permissions
  - resourcemanager.projects.get
  - resourcemanager.projects.list
# IAM - Most Important Concepts - A Review
- Roles : Permissions (What Actions? What Resources?)
- Policy : Assign Permissions to Members
  - **Remember**: Permissions are NOT directly assigned to Member
    - Member gets permissions through Role!
- Role can have multiple permissions
# IAM policy
- Roles are assigned to users through IAM Policy documents
- Member type is identified by prefix
  - Example: user, serviceaccount, group or domain
# IAM policy - Example
```
{
  "bindings": [
    {
      "role": "roles/storage.objectAdmin",
       "members": [
         "user:you@in28minutes.com",
         "serviceAccount:myAppName@appspot.gserviceaccount.com",
         "group:administrators@in28minutes.com",
         "domain:google.com"
      ] 
    },
    {
      "role": "roles/storage.objectViewer",
      "members": [
        "user:you@in28minutes.com"
      ],
      "condition": {
        "title": "Limited time access",
        "description": "Only upto Feb 2022",
        "expression": "request.time < timestamp('2022-02-01T00:00:00.000Z')",
      } 
    }
  ] 
}
```
# Service Accounts
- Application on a VM needs access to cloud storage
- (RECOMMENDED) Use Service Accounts
- Service account types
  - Default service account - Automatically created when some services are used
  - User Managed - User created
    - (RECOMMENDED) Provides fine grained access control
  - Google-managed service accounts - Created and managed by Google
    - Used by GCP to perform operations on user's behalf
# Use case 1 : VM <-> Cloud Storage
- Create a Service Account Role with the right permissions
- Assign Service Account role to VM instance
- Uses Google Cloud-managed keys
  - Key generation and use are automatically handled by IAM
  - Automatically rotated
  - No need to store credentials in config files
- Do NOT delete service accounts used by running instances
# Use case 2 : On Prem <-> Cloud Storage (Long Lived)
- You CANNOT assign Service Account directly to an On Prem App
- Create a Service Account with right permissions
- Create a Service Account User Managed Key
  - Download the service account key file
- Make the service account key file accessible to your application
  - Set environment variable GOOGLE_APPLICATION_CREDENTIALS
- Use Google Cloud Client Libraries
  - Google Cloud Client Libraries use a library
# Use case 3 : On Prem <-> Google Cloud APIs (Short Lived)
- Make calls from outside GCP to Google Cloud APIs with short lived permissions
  - Less risk compared to sharing service account keys
  - Few hours or shorter
- Credential Types
  - OAuth 2.0 access tokens
  - OpenID Connect ID tokens
- Examples
  - When a member needs elevated permissions, he can assume the service account role
# Service Account Use case Scenarios
| Scenario                                                                                              | Solution                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Application on a VM wants to talk to a Cloud Storage bucket                                           | Configure the VM to use a Service Account with right permissions                                                                                                   |
| Application on a VM wants to put a message on a Pub Sub Topic                                         | Configure the VM to use a Service Account with right permissions                                                                                                   |
| Is Service Account an identity or a resource?                                                         | It is both. You can attach roles with Service Account (identity). You can let other members access a SA by granting them a role on the Service Account (resource). |
| VM instance with default service account in Project A needs to access Cloud Storage bucket in Project | In project B, add the service account from Project A and assign Storage Object Viewer Permission on the bucket                                                     |
# ACL (Access Control Lists)
- ACL: Define who has access to your buckets and objects, as well as what level of access they have
- How is this different from IAM?
  - IAM permissions apply to all objects within a bucket
  - ACLs can be used to customized specific accesses to different objects
- IAM (all object in bucket) vs ACL(specific object)
- (**Remember**) Use IAM for common permissions to all objects in a bucket
- (**Remember**) Use ACLs if you need to customize access to individual objects
# Access Control - Overview
- How do you control access to objects in a Cloud Storage bucket?
  - Uniform (Recommended) - Uniform bucket level access using IAM
  - Fine-grained - Use IAM and ACLs to control access
- Use Uniform access when all users
- Fine grained access with ACLs can be used when you need to customize the access at an object level
# Cloud Storage - Signed URL
- allow a user limited time access to your objects:
  - Users do NOT need Google accounts
- A URL that gives permissions for limited time duration to perform specific actions
# Cloud Storage - Static website
- Create a bucket with the same name as website name
- Copy the files to the bucket
- Add member allUsers and grant Storage Object Viewer option
