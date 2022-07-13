# Resource Hierarchy in GCP
- Well defined hierarchy
  - Organization > Folder > Project > Resources
# Resource Hierarchy - Recommendations for Enterprises
- Create separate projects for different environments:
  - Complete isolation between test and production environments
- Create separate folders for each department
  - Isolate production applications of one department from another 
  - We can create a shared folder for shared resources
- One project per application per environment
  - Let's consider two apps: "A1" and "A2"
  - Let's assume we need two environments: "DEV" and "PROD"
  - In the ideal world you will create four projects: A1-DEV, A1-PROD, A2-DEV, A2-PROD:
# Billing Accounts
- Billing Account is mandatory for creating resources in a project
- Billing Account can be associated with one or more projects
- You can have multiple billing accounts in an Organization
- (**RECOMMENDATION**) Create Billing Accounts representing your organization structure:
- Two Types:
  - Self Serve : Billed directly to Credit Card or Bank Account 
  - Invoiced : Generate invoices (Used by large enterprises)
# Managing Billing - Budget, Alerts and Exports
- Setup a Cloud Billing Budget to avoid surprises:
  - (RECOMMENDED) Configure Alerts
- Billing data can be exported (on a schedule) to:
  - Big Query (if you want to query information or visualize it)
  - Cloud Storage (for history/archiving)
# IAM Best Practices
- Principle of Least Privilege
- Separation of Duties - Involve atleast 2 people in sensitive tasks:
- Constant Monitoring: Review Cloud Audit Logs to audit changes to IAM policies and access to Service Account keys
- Use Groups when possible
# User Identity Management in Google Cloud
- Email used to create free trial account => "Super Admin"
  - However, this is NOT recommended for enterprises
- Option 1: Your Enterprise is using Google Workspace
  - Use Google Workspace to manage users (groups etc)
  - Link Google Cloud Organization with Google Workspace
- Option 2: Your Enterprise uses an Identity Provider of its own
  - Federate Google Cloud with your Identity Provider
# Corporate Directory Federation
- Federate Cloud Identity or Google Workspace with your external identity provider (IdP) such as Active Directory or Azure Active Directory.
- Enable Single Sign On:
# IAM Members/Identities
- Google Account - Represents a person (an email address)
- Service account - Represents an application account (Not person)
- Google group - Collection - Google & Service Accounts
  - Has an unique email address
  - Helps to apply access policy to a group
- Google Workspace domain: Google Workspace (formerly G Suite) provides collaboration services for enterprises:
  - Tools like Gmail, Calendar, Meet, Chat, Drive, Docs etc are included
- Cloud Identity domain - Cloud Identity is an Identity as a Service(IDaaS) solution that centrally manages users and groups.
  - You can use IAM to manage access to resources for each Cloud Identity account
# IAM Members/Identities - Use Cases
| Scenario                                                                                                                                           | Solution                                                                                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| All members in your team have G Suite accounts. You are creating a new production project and would want to provide access to your operations team | Create a Group with all your operations team. Provide access to production project to the Group.                                                                          |
| All members in your team have G Suite accounts. You are setting up a new project. You want to provide a one time quick access to a team member.    | Assign the necessary role directly to G Suite email address of your team member If it is not a one time quick access, the recommended approach would be to create a Group |
| You want to provide an external auditor access to view all resources in your project BUT he should NOT be able to make any changes                 | Give them roles/viewer role (Generally basic roles are NOT recommended BUT it is the simplest way to provide view only access to all resources!)                          |
| Your application deployed on a GCE VM (Project A) needs to access cloud storage bucket from a different project (Project B)                        | In Project B, assign the right role to GCE VM service account from Project A                                                                                              |
# Organization Policy Service
- centralized constraints on all resources created in an Organization
- Needs a Role - Organization Policy Administrator
- (**Remember**) IAM focuses on Who
  - Who can take specific actions on resources?
- (**Remember**) Organization Policy focuses on What
  - What can be done on specific resources?
# Resource Hierarchy & IAM Policy
- IAM Policy can be set at any level of the hierarchy
- Resources inherit the policies of All parents
- Policy inheritance is transitive:
  - For example: Organization policies are applied at resource level
- You can't restrict policy at lower level if permission is given at an higher level
# Organization, Billing and Project Roles
- Organization Administrator
  - Define Resource Hierarchy
  - Define Access Management Policies
  - Manage other users and roles
- Billing Account Creator - Create Billing Accounts
- Billing Account Administrator - Manage Billing Accounts (payment instruments, billing exports, link and unlink projects, manage roles on billing account)
- Billing Account User - Associate Projects with Billing Accounts
  - Typically used in combination with Project Creator
  - These two roles allow user to create new project and link it with billing account
- Billing Account Viewer - See all Billing Account details
# Billing Roles - Quick Review
| Roles                         | Description                                   | Use Case      |
|-------------------------------|-----------------------------------------------|---------------|
| Billing Account Creator       | Permissions to create new billing accounts    | Finance Team  |
| Billing Account Administrator | Manages billing account but can't create them | Finance Team  |
| Billing Account User          | Assigns projects to billing accounts          | Project Owner |
| Billing Account Viewer        | View only access to billing account           | Auditor       |
# Organization, Billing and Project Roles - Scenarios
- Scenario 1: I'm creating a project and I want to associate an existing billing account with the project
  - Project Creator and Billing Account User (link project to billing account)
- Scenario 2: I'm a billing auditor
  - Billing Account Viewer role
# Compute Engine Roles
- Compute Engine IAM Roles
  - Compute Engine Admin - Complete control of compute - Instances, Images, Load Balancers, Network, Firewalls etc...
  - Compute Instance Admin - Create, modify, and delete virtual machine instances and disks
  - Compute Engine Network Admin - Complete access to networking resources (routes, networks, health checks, VPN, Gateways etc) and READ ONLY access to (firewall rules and SSL certificates)
  - Compute Engine Security Admin - Complete access to firewall rules and SSL certificates
  - Compute Storage Admin - Complete access to disks, images, snapshots
  - Compute Engine Viewer - Read ONLY access to everything in compute
  - Compute OS Admin Login - Log in to a Compute Engine instance as an administrator user
  - Compute OS Login - Log in to a Compute Engine instance as a standard user
# App Engine Roles
- App Engine Roles (CRUD - Create, Read (get/list), Update, Delete)
  - App Engine Creator - applications(CD) (Responsible for creating an application)
  - App Engine Admin - applications(RU), services/instances/versions(CRUD), operations
  - App Engine Viewer - applications/services/instances/versions(R), operations
  - App Engine Code Viewer - appengine.versions.getFileContents (ONLY role that can view code)
  - App Engine Deployer - versions(CRD), applications/services/versions(R)
  - App Engine Service Admin - versions(RUD), applications(R), services/instances(CRUD), operations: Split or migrate traffic, Start and stop a version
- App Engine Roles DO NOT allow you to
  - View and download application logs
  - View Monitoring charts in the Cloud Console
  - Enable and Disable billing
  - Access configuration or data stored in other services
# Compute Engine and App Engine Roles - Few Scenarios
- Scenario 1: What is the difference between Compute Engine Admin vs Compute Instance Admin?
  - Compute Instance Admin can do everything with instances and disks ONLY.
  - Compute Engine Admin is admin for everything in compute - instances, disks, images, network, firewalls etc.
- Scenario 2: What is a secure way of setting up application deployment?
  - Application Deployer - Roles: App Engine Deployer + Service Account User
    - Limited to deploying
    - NOT be able to configure traffic
  - Operations - Role: App Engine Service Admin
    - CANNOT deploy a new version of an app
# Google Kubernetes Engine (GKE) IAM Roles
- Kubernetes Engine Admin (roles/container.admin) - Complete Access to Clusters and Kubernetes API objects
- Kubernetes Engine Cluster Admin - Provides access to management of clusters (Cannot access Kubernetes API objects - Deployments, Pods etc)
- Kubernetes Engine Developer - Manage Kubernetes API objects (and read cluster info)
- Kubernetes Engine Viewer - get/list cluster and kubernetes api objects
# Cloud Storage - Roles
- Storage Admin - storage.buckets.*, storage.objects.*
- Storage Object Admin - storage.objects.* (DOES NOT HAVE storage.buckets.*)
- Storage Object Creator
- Storage Object Viewer
- (**REMEMBER**) Container Registry stores container images in Cloud Storage buckets
- (**REMEMBER**) Storage Admin vs Storage Object Admin
  - Storage Admin can create buckets and play with objects
  - Storage Object Admin CANNOT create buckets but can play with objects in a bucket!
# Cloud BigQuery Roles
- Cloud BigQuery IAM Roles
  - BigQuery Admin
  - BigQuery Data Owner (Does NOT have access to Jobs!)
  - BigQuery Data Editor
  - BigQuery Data Viewer
  - BigQuery Job User
  - BigQuery User
- To see data, you need either BigQuery User or BigQuery Data Viewer roles
- BigQuery Data Owner or Data Viewer roles do NOT have access to jobs!
# Logging IAM Roles and Service Account Roles
- Logging and Audit Logging:
  - roles/logging.viewer (Logs Viewer):
  - roles/logging.privateLogViewer (Private Logs Viewer):
  - roles/logging.admin (Logging Admin): All permissions related to Logging
- Service Accounts:
  - roles/iam.serviceAccountAdmin: Create and manage service accounts
  - roles/iam.serviceAccountUser: Run operations as the service account
  - roles/iam.serviceAccountTokenCreator - Impersonate service accounts
  - roles/iam.serviceAccountKeyAdmin - Create and manage (and rotate) service account keys.
# Other Important IAM Roles
- roles/iam.securityAdmin - Get and set any IAM policy
- roles/iam.securityReviewer - List all resources & IAM policies
- ...
# SSHing into Linux VMs - Options
- Compute Engine Linux VMs uses key-based SSH authentication
- Two Options:
  - Metadata managed: Manually create and configure individual SSH keys
  - OS Login: Manage SSH access without managing individual SSH keys!
- (Windows) Windows instances use password authentication(username and password)
# SSHing into Linux VMs - Details
- Option 1: Console - SSH Button
- Option 2: Gcloud - gcloud compute ssh
- Option 3: Use customized SSH keys
- You can disable Project wide SSH keys on a specific compute instance
# IAM - Scenarios
| Scenario                                                                               | Description                                                                                         |
|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| You want to give permanent access to a sub set of objects in a Cloud Storage bucket    | Use ACLs                                                                                            |
| You want to give permanent access to the entire bucket in a Cloud Storage bucket       | Use IAM                                                                                             |
| You want to provide time limited access to a specific object in a Cloud Storage bucket | Create a Signed URL                                                                                 |
| You want to give access to a set of resources to your development team                 | Create a Group with your development team as member. Bind the right Predefined Roles to your Group. |
| Which Role? Upload objects to Cloud Storage                                            | Storage Object Creator                                                                              |
| Which Role? Manage Kubernetes API objects                                              | Kubernetes Engine Developer                                                                         |
| Which Role? Manage service accounts                                                    | Service Account Admin                                                                               |
| Which Role? View Data in BigQuery                                                      | BigQuery Data Viewer                                                                                |
