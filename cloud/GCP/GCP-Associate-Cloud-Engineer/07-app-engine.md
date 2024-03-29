# App Engine
- Simplest way to deploy and scale your applications
- No usage charges - Pay for resources provisioned
- load balancing & Auto scaling / Managed platform updates & Application health monitoring / Application versioning
# Compute Engine vs App Engine
- Compute Engine
  - IAAS
  - MORE Flexibility / MORE Responsibility 
- App Engine
  - PaaS
  - Serverless
  - LESSER Responsibility
  - LOWER Flexibility
# App Engine environments
- Standard: Applications run in language specific sandboxes
  - V1: Java, Python, PHP, Go (OLD Versions)
  - V2: Java, Python, PHP, Node.js, Ruby, Go (NEWER Versions)
    - Full Network Access and No restrictions on Language Extensions
- Flexible - Application instances run within Docker containers
  - Makes use of Compute Engine virtual machines
  - Support ANY runtime
  - Provides access to background processes and local disks
# App Engine - Application Component Hierarchy
- Application: One App per Project
  - Service(s): Multiple Microservices or App components
    - Version(s): Each version associated with code and configuration
# App Engine - Comparison
| Feature  | standard  | Flexible  |
| -------  | -------   | -------   |
| Pricing Factors | Instance hours | vCPU, Memory & Persistent Disks |
| Scaling | Manual, Basic, Automatic | Manual, Automatic |
| Scaling to zero | Yes | No. Minimum one instance |
| Instance startup time | Seconds | Minutes |
| Rapid Scaling | Yes | No |
| Max. request timeout | 1 to 10 minutes | 60 minutes |
| Local disk | Mostly(except for Python, PHP). Can write to /tmp. | Yes. Ephemeral. New Disk on startup. |
| SSH for debugging | No | Yes |
# App Engine - Scaling Instances
- Automatic - Automatically scale instances based on the load
  - Recommended for Continuously Running Workloads
- Basic - Instances are created as and when requests are received
  - Recommended for Adhoc Workloads
    - Instances are shutdown if ZERO requests
      - Tries to keep costs low
- Manual - Configure specific number of instances to run
  - Adjust number of instances manually over time
# AppEngine - Request Routing
- combination of three approaches
  - Routing with URLs
    - https://PROJECT_ID.REGION_ID.r.appspot.com (default service called)
    - https://SERVICE-dot-PROJECT_ID.REGION_ID.r.appspot.com (specific service)
    - https://VERSION-dot-SERVICE-dot-PROJECT_ID.REGION_ID.r.appspot.com (specific version of service)
  - Routing with a dispatch file
    - gcloud app deploy dispatch.yaml
  - Routing with Cloud Load Balancing
    - Configure routes on Load Balancing instance
# AppEngine - Deploying new versions without downtime
- Option 1: I'm very confident - Deploy & shift all traffic at once
- Option 2: I want to manage the migration from v1 to v2
  - STEP 1: Deploy v2 without shifting traffic
  - STEP 2: Shift traffic to V2:
    - Option 1 (All at once Migration): Migrate all at once to v2
    - Option 2 (Gradual Migration): Gradually shift traffic to v2
    - Option 3 (Splitting): Control the pace of migration
# How do you split traffic between multiple versions
- How do you decide which version receives which traffic?
  - IP Splitting - Based on request IP address
  - Cookie Splitting - Based on a cookie (GOOGAPPUID)
  - Random - Do it randomly
- How to do it?
  - gcloud app services set-traffic s1 --splits=v2=.5,v1=.5 --split- by=cookie
# App Engine - Cron Job
- Use cases:
  - Send a report by email every day
    - Refresh cache data every 30 minutes
```
cron:
- description: "daily summary job"
   url: /tasks/summary
   schedule: every 24 hours
```
# Others Important App Engine yaml files
- override routing rules
```
dispatch:
  - url: "*/mobile/*"
    service: mobile-frontend
  - url: "*/work/*"
    service: static-backend
```
- manage task queues
```
queue:
- name: fooqueue
  rate: 1/s
  retry_parameters:
    task_retry_limit: 7
    task_age_limit: 2d
```
# App Engine - **Remember**
- AppEngine is Regional (services deployed across zones)
  - You CANNOT change an Application's region
- **Good** option **for simple microservices** (multiple services)
  - Use **Standard v2** when you are using **supported languages**
  - **Flexible** if you are building **containerized apps**
- Be aware - **AT LEAST one container** is always running when using **Flexible**:
  - Go for Standard if you want to be able to scale down the number of instances to zero when there is NO load
- Use a combination of resident and dynamic instances
  - Resident Instances: Run continuously
  - **Dynamic Instances**: Added based on load
    - Use all dynamic instances if you are **cost sensitive**
    - If you are **not very cost sensitive**, **keep a set of resident** instances running always
# App Engine - Scenarios (*sample-question*)
- I want to create two Google App Engine Apps in the same project
  - Not possible. You can only have one App Engine App per project. However you can have multiple services and multiple version for each service.
- I want to create two Google App Engine Services inside the same App
  - Yup. You can create multiple services under the same app. Each service can have multiple versions as well.
- I want to move my Google App Engine App to a different region
  - App Engine App is region specific. You CANNOT move it to different region. Create a new project and create new app engine app in the new region.
- Perform Canary deployments
  - Deploy v2 without shi�ing traffic (gcloud app deploy --no- promote)
  - Shi� some traffic to V2 (gcloud app services set-traffic s1 --splits v1=0.9,v2=0.1)

