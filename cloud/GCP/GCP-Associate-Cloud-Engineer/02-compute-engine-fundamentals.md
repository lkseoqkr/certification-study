# GCE (google compute engine)
- applications are deployed to physical servers
- where are applications deployed in cloud?
  - VM (Virtual Machine) - virtual servers in GCP
  - GCE (Google Compute Engine) - provision & manage virtual machine
# Compute Engine Features
- create & manage VM lifecycle
- **Load balancing** and **auto scaling** for VM
- **attach storage** to VM
- manage **network connectivity and configuration** for VM
# Compute Engine Machine Family
- **General Purpose(E2, N2, N2D, N1)**: Best price performance ratio
  - web and application server, small-medium DB, dev environment
- **Memory Optimized(M2, M1)**: Ultra high memory workloads
  - large in memory DB/analytics
- **Compute Optimized(C2)**: Compute intensive workload
  - gaming app
# Compute Engine Machine Type
- e2-standard-2
  - e2 - machine type family
  - standard - type of workload
  - 2 - number of CPU
- memory, disk and networking capabilities increase along with CPU
# Image
- OS or SW on the instance
- public image: provided & managed by google or open source
- custom image: created by user
# Internal and External IP Addresses
- external (public): **internet addressable**
  - cannot have two resource with the same IP
- internal (private): **internal to corporate network**
  - two different corporate network can have resources with the same IP
- all **VM instances** are assigned at least one internal IP
- VM instance can have external IP
  - *(REMEMBER) when VM is stopped, external IP is lost*
# Static IP Address
- constant external IP
  - quick and dirty way to get constant external IP
- can *be switched* to another VM in same project
- *remain attached* even though VM is stopped. need manual detach
- *(REMEMBER) you are billed* for static IP *when you are not using it*
# Simplify VM http server setup
- startup script
  - ```sudo -y install apache```
- instance template
  - define machine type/image/label/startup script
  - **cannot update**
  - *increases boot up time*, Installing OS patches and software at launch of VM instances 
- custom image
  - OS and patched are pre-installed
  - **Prefer using Custom Image** to Startup script
# Sustained use discount
- Automatic discount for running VM
- applicable for instance created by **Google K8s Engine** or **Compute Engine**
- Restriction
  - not for E2 & A2
  - not for instance created by App Engine flexible and Dataflow
# Committed use discount
- for workload with **predictable resource** needs
- commit for **1 or 3 years**
- **Up to 70% discount** on machine type and GPUs
- applicable for instance created by **Google K8s Engine** or **Compute Engine**
- Restriction
  - not for instance created by App Engine flexible and Dataflow
# Preemptible VM
- **Short-lived cheaper** compute instance
  - can be stopped by GCP any time
- Use preempt VM's if:
  - fault tolerant
  - cost sensitive
  - not immediate
  - ex) non immediate batch proccessing
# Google Compute Engine - billing
- **billed by the second**
- not billed during instance stop
- **always create budget alert**
# Compute Engine : Live Migration & Availability Policy
- Live migration
  - migrated to another host in the same zone
  - NOT SUPPORTED for GPUs and preemptible instances
- Important Configuration - **Availability Policy**
  - On host maintenance: during periodic infrastructure maintenance
    - Migrate (default): Migrate VM instance to other hardware
    - Terminate: Stop the VM instance
  - Automatic restart
    - Restart VM instances terminated due to non-user-initiated reasons (maintenance event, hardware failure etc.)
# Compute Engine Features: Custom Machine Types 
- Custom Machine Type: Adjust vCPUs, memory and GPUs
  - Choose between E2, N2, or N1 machine types
  - Billed per vCPUs, memory provisioned to each instance
# Compute Engine Features: GPUs
- math intensive and graphics-intensive workloads
- (REMEMBER) Use images with GPU libraries (Deep Learning) installed OTHERWISE, GPU will not be used
- GPU restrictions
  - **NOT supported on all machine types**
  - **On host maintenance** can **only** have the value **Terminate VM instance**
# Virtual Machine - *REMEMBER*
- Associated with a project
- **Instances are Zonal** (Run in a specific zone (in a specific region))
  - Images are global (You can provide access to other projects - if needed)
  - Instance templates are global (Unless you use zonal resources in your templates)
- **Automatic Basic Monitoring**
# Virtual Machine - Best Practices
- Choose right machine type, Zone and Region
- Reserve for "committed use discounts" for constant workloads
- Use preemptible instances for fault-tolerant, NON time critical workloads
# Compute Engine Scenarios (*sample-question*)
- What are the pre-requisites to be able to create a VM instance?
  - Project
  - Billing Account
  - Compute Engines APIs should be enabled
- You want dedicated hardware for your compliance, licensing, and management needs
  - Sole-tenant nodes
- I have 1000s of VM and I want to automate OS patch management,
  OS inventory management and OS configuration management (manage so�ware installed)
  - Use "VM Manager"
- You want to login to your VM instance to install software
  - You can SSH into it
- You do not want to expose a VM to internet
  - Do NOT assign an external IP Address
- You want to allow HTTP traffic to your VM
  - Configure Firewall Rules
# Quick Review (*sample-question*)
- Image
  - What operating system and what software do you want on the VM instance?
  - Reduce boot time and improve security by creating custom hardened Images.
  - You can share an Image with other projects
- Machine Types
  - Optimized combination of compute(CPU, GPU), memory, disk (storage) and networking for specific workloads.
  - You can create your own Custom Machine Types when existing ones don't fit your needs
- Static IP Addresses: Get a constant IP addresses for VM instances
- Instance Templates: Pre-configured templates simplifying the creation of VM instances
- Sustained use discounts: Automatic discounts for running VM instances for significant portion of the billing month
- Committed use discounts: 1 year or 3 year reservations for workloads with predictable resource needs
- Preemptible VM: Short-lived cheaper (upto 80%) compute instances for non- time-critical fault-tolerant workloads

