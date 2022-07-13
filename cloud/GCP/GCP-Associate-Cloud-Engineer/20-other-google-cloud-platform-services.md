# Pricing Calculator
- Estimating the cost of a Google Cloud solution is NOT easy
- Estimates for 40+ Services:
- (REMEMBER) These are Estimates! (NOT binding on GCP)
# Google Cloud Deployment Manager - Introduction
- Lets consider an example:
  - want to create a new VPC and a subnet
  - provision a Load balancer, Instance groups with 5 Compute
- AND I would want to create 4 environments
- Deployment Manager can help you do all these with a simple (actually NOT so simple) script!
# Google Cloud Deployment Manager - Advantages
- Automate deployment and modification of Google Cloud resources in a controlled, predictable way
- Avoid mistakes with manual configuration
- Important Note - Always modify the resources created by Deployment Manager using Deployment Manager
# Google Cloud Deployment Manager
- All configuration is defined in a simple text file - YAML
- (Default) Automatic rollbacks on errors (Easier to retry)
# Cloud Deployment Manager - Terminology
- Configuration file: YAML file
- Templates: Reusable resource definitions that can be used in multiple configuration files
- Deployment: Collection of resources that are deployed and managed together
- Manifests: Read-only object containing original deployment configuration
# Cloud Marketplace (Cloud Launcher)
- Cloud Marketplace: Central repo of easily deployable apps & datasets Similar to App Store/Play Store for mobile applications
# Cloud DNS
- What would be the steps in setting up a website with a domain name (for example, in28minutes.com)?
  - Step I : Buy the domain name in28minutes.com (Domain Registrar)
  - Step II : Setup your website content (Website Hosting)
  - Step III : Route requests to in28minutes.com to the my website host server(DNS)
- Cloud DNS = Global Domain Name System (Step III)
# Cloud Dataflow
- Cloud Dataflow is a difficult service to describe
  - Let's look at a few example pipelines you can build:
    - Pub/Sub > Dataflow > BigQuery (Streaming)
    - Pub/Sub > Dataflow > Cloud Storage (Streaming - files)
    - Cloud Storage > Dataflow > Bigtable/CloudSpanner/Datastore/BigQuery (Batch - Load data into databases)
- Streaming and Batch Usecases
  - Realtime Fraud Detection, Sensor Data Processing, Log Data Processing, Batch Processing (Load data, convert formats etc)
- Use pre-built templates
- Based on Apache Beam (supports Java, Python, Go ...)
- Serverless (and Autoscaling)
# Cloud Dataproc
- Managed Spark and Hadoop service:
- Multiple Cluster Modes:
- Use case: Move your Hadoop and Spark clusters to the cloud
- (REMEMBER) Cloud Dataproc is a data analysis platform
- (ALTERNATIVE) BigQuery - When you run SQL queries on Petabytes
  - Go for Cloud Dataproc when you need more than queries
