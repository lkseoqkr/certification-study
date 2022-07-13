# Gcloud
- **CLI(Command line interface)** to interact with Google Cloud Resources
- *(REMEMBER) SOME GCP services have specific CLI tools*
  - Cloud Storage - gsutil
  - Cloud BigQuery - bq
  - Cloud Bigtable - cbt
  - Kubernetes - kubectl
# Gcloud - Getting Started
- install SDK or also use Gcloud on Cloud Shell
- Connecting to GCP
  - gcloud init - initialize or reinitialize gcloud
  - gcloud config list - lists all properties of the active configuration
# gcloud config set
- Sets the specified property in your active configuration
- Opposite - gcloud config unset
# Playing with gcloud config set
```
gcloud config set compute/region us-east2
gcloud config set compute/zone us-east1-b
gcloud config list
  [component_manager]
  disable_update_check = True
  [compute]
  gce_metadata_read_timeout_sec = 30
  region = us-east1
  zone = us-east1-b
  [core]
  account = testing@gmail.com
  disable_usage_reporting = True
  project = useful-device-303710
  verbosity = info
  [metrics]
  environment = devshell
```
# Gcloud - Managing Multiple Configurations
1. Create new configuration
2. Activate specific configuration
3. ```gcloud config configurations activate NAME(dev)```
# gcloud command structure - Playing with Services
- gcloud GROUP SUBGROUP ACTION
  - GROUP - config or compute or container or dataflow or functions or iam or
  - SUBGROUP - instances or images or instance-templates or machine-types or regions or zones
  - ACTION - create or list or start or stop or describe
- example
  - gcloud compute instances list
  - gcloud compute regions list
  - gcloud compute machine-types list --filter="zone:us-central1-b"
  - gcloud compute instances create [NAME]
# Compute Instances - Default Region and Zone
- 3 (Command Specific) overrides Option 2 (Local gcloud configuration) overrides Option 1 (Centralized Configuration)

