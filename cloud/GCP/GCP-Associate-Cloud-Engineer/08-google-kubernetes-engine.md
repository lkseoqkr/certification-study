# Kubernetes
- Most popular open source container orchestration solution
- Provides all important container orchestration features:
  - Auto Scaling
  - Service Discovery
  - Load Balancer
  - Self Healing
  - Zero Downtime Deployments
# Google Kubernetes Engine (GKE)
- Managed Kubernetes service
- auto-repair (repair failed nodes) and auto-upgrade (use latest version of K8S always) features
- Pod and Cluster Autoscaling
- Cloud Logging and Cloud Monitoring
- Container-Optimized OS
- Persistent disks and Local SSD
# Google Kubernetes Engine (GKE) Cluster
- Cluster : Group of Compute Engine instances
  - Master Node(s) - Manages the cluster
  - Worker Node(s) - Run your workloads (pods)
- Master Node (Control plane) components:
  - API Server - Handles all communication for a K8S cluster (from nodes and outside)
  - Scheduler - Decides placement of pods
  - Control Manager - Manages deployments & replicasets
- Worker Node components:
  - Runs your pods
  - Kubelet - Manages communication with master node(s)
# GKE Cluster Types
| Type | Description |
| ----- | ----- |
| Zonal Cluster | Single Zone - Single Control plane. Nodes running in the same zone. |
| | Multi-zonal - Single Control plane but nodes running in multiple zones |
| Regional cluster | Replicas of the control plane runs in multiple zones of a given region. Nodes also run in same zones where control plane runs.
| Private cluster | VPC-native cluster. Nodes only have internal IP addresses. |
| Alpha cluster | Clusters with alpha APIs - early feature API's. Used to test new K8S features. |
# Kubernetes - Pods
- Smallest deployable unit
- contains one or more containers
- Each Pod is assigned an ephemeral IP address
- All containers in a pod share:
  - Network 
  - Storage 
  - IP Address 
  - Ports and 
  - Volumes (Shared persistent disks)
# Kubernetes - Deployment vs Replica Set
- A deployment is created for each microservice:
  - Deployment manages new releases ensuring zero downtime
- Replica set ensures that a specific number of pods are running for a specific microservice version
  - Even if one of the pods is killed, replica set will launch a new one
# Kubernetes - Service
- Each Pod has its own IP address
- Three Types:
  - ClusterIP: Exposes Service on a cluster-internal IP
    - Use case: You want your microservice only to be available inside the cluster (Intra cluster communication)
  - LoadBalancer: Exposes Service externally using a cloud provider's load balancer
    - Use case: You want to create individual Load Balancer's for each microservice
  - NodePort: Exposes Service on each Node's IP at a static port (the NodePort)
    - Use case: You DO not want to create an external Load Balancer for each microservice (You can create one Ingress component to load balance multiple microservices)
# Container Registry - Image Repository
- Container Registry - fully-managed container registry provided by GCP
- (Alternative) Docker Hub
- **HostName/ProjectID/Image:Tag - gcr.io/projectname/helloworld:1**
# GKE - **Remember**
- **Replicate master nodes** across multiple zones for high availability
- (REMEMBER) Some **CPU** on the nodes is **reserved by Control Plane:** 
  - 1st core - 6%, 2nd core - 1%, 3rd/4th - 0.5, Rest - 0.25
- Creating Docker Image for your microservices(Dockerfile):
  - Build Image -> Test it Locally -> Push it to Container Repository
- Kubernetes supports Stateful deployments like Kafka, Redis, ZooKeeper
  - **StatefulSet** - Set of Pods with unique, persistent identities and stable hostnames
- How do we run services on nodes for log collection or monitoring?
  - DaemonSet - One pod on every node! (for background services)
- (Enabled by default) Integrates with Cloud Monitoring and Cloud Logging
  - Cloud Logging System and Application Logs can be exported to Big Query or Pub/Sub
# GKE - Cluster Management - Command Line
- gcloud container clusters create / resize / update / delete / ...
# GKE - Workload Management - Command Line
- kubectl get pods/services/replicasets
# Google Kubernetes Engine - Scenarios (*sample-question*)
- You want to keep your costs low and optimize your GKE implementation
  - Consider Preemptible VMs, Appropriate region, Committed- use discounts.
  - E2 machine types are cheaper than N1.
  - Choose right environment to fit your workload type (Use multiple node pools if needed).
- You want an efficient, completely auto scaling GKE solution
  - Configure Horizontal Pod Autoscaler for deployments and Cluster Autoscaler for node pools
- You want to execute untrusted third-party code in Kubernetes Cluster
  - Create a new node pool with GKE Sandbox. Deploy untrused code to Sandbox node pool
- You want enable ONLY internal communication between your microservice deployments in a Kubernetes Cluster
  - Create Service of type ClusterIP
- My pod stays pending
  - Most probably Pod cannot be scheduled onto a node(insufficient resources)
- My pod stays waiting
  - Most probably failure to pull the image
