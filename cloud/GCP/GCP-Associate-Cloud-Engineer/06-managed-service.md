# Managed Services
- want to continue running applications in the cloud, the same way you run them in your data center?
- should understand some terminology used with cloud services
  - IaaS (Infrastructure as a Service)
  - PaaS (Platform as a Service)
  - FaaS (Function as a Service)
  - CaaS (Container as a Service)
  - Serverless
# IAAS (Infrastructure as a Service)
- Use **only infrastructure** from cloud provider
- Example: Using VM to deploy your applications or databases
- cloud provider is responsible for
  - network / physical hardware / virtualization
- You are responsible for
  - Application Code and Runtime
  - Configuring load balancing
  - Auto scaling
  - OS upgrades and patches
  - Availability
  - os / application runtime / applications
# PAAS (Platform as a Service)
- Cloud provider is responsible for:
  - Auto scaling, Availability & Load balancing
  - network / physical hardware / virtualization / os / application runtime
- You are responsible for
  - Configuration (of Application and Services)
  - Application code (if needed)
- Varieties:
  - CaaS (Container as a Service): Containers instead of Apps
  - FaaS (Function as a Service): Functions instead of Apps
  - Databases - Relational & NoSQL (Amazon RDS, Google Cloud SQL, Azure SQL Database etc), Queues, AI, ML, Operations etc
# Microservices
- Flexibility to innovate and build applications in different programming languages (Go, Java, Python, JavaScript, etc)
- BUT deployments become complex
  - one way of deploying Go, Java, Python or JavaScript .. microservices?
    - Enter containers!
# Containers - Docker
- Create Docker images
- Docker image has all needs of a microservice
  - Application Runtime (JDK or Python or NodeJS)
  - Application code and Dependencies
- Runs the same way on any infrastructure
- Advantages
  - Docker containers are light weight
  - Docker provides isolation for containers
  - cloud neutral
# Container Orchestration
- Requirement
  - 10 instances of Microservice A container, 15 instances of Microservice B container, ...
- Typical Features
  - Auto Scaling
  - Service Discovery - Help microservices find one another
  - Load Balancer
  - Self Healing - Do health checks and replace failing instances
  - Zero Downtime Deployments - Release new versions without downtime
# Serverless
- What do we think about when we develop an application?
  - Where to deploy? What kind of server? What OS?
  - How do we take care of scaling and availability of the application?
- What if you **don't need to worry about servers and focus on your code**?
  - Enter Serverless
  - _NOT mean "No Servers"_
- Serverless for me
  - don't worry about infrastructure
  - Pay for use, ZERO REQUESTS => ZERO COST
- You focus on code and the cloud managed service takes care of all that is
  needed to scale your code to serve millions of requests
  - **pay for requests and NOT servers!**
# Serverless - My Perspective!
- Serverless - Important Features
  - 1: Zero worry about infrastructure, scaling and availability 
  - 2: Zero invocations => Zero Cost (Can you scale down to ZERO instances?) 
  - 3: **Pay for invocations and NOT for instances** (or nodes or servers) 
  - Serverless Level 1: Features (1 + 2)
  - Serverless Level 2: Features (1 + 2 + 3)
- When I refer to Serverless, I'm referring to Level 2
- HOWEVER cloud providers include managed services at Level 1 and Level 2:
  - Level 1: Google App Engine
    - Scale down to ZERO instances when there is no load, 
    - BUT you pay for number (and type) of instances running!
  - Level 2: Google Functions, AWS Lambda, Azure Functions
    - You pay for invocations
# GCP Managed Services for Compute (*sample-question*)
- Compute Engine (IaaS)
  - High-performance and general purpose VMs that scale globally
- Google Kubernetes Engine (Caas)
  - Orchestrate containerized microservices on Kubernetes Needs advanced cluster configuration and monitoring
- App Engine (PaaS, Caas, Serverless)
  - Build highly scalable applications on a fully managed platform using open and familiar languages and tools
- Cloud Functions (Faas, Serverless)
  - Build event driven applications using simple, single-purpose functions
- Cloud Run (CaaS, Serverless)
  - Develop and deploy highly scalable containerized applications. 
  - Does NOT need a cluster!
