# Instance Groups
- Group of VM instances managed as a single entity (lifecycle as one unit) 
- Two Types of Instance Groups
  - Managed : Identical VMs created using a template
  - Unmanaged : Different configuration for VMs in same group
    - Does NOT offer auto scaling, auto healing & other services
    - Not recommended
  - Location can be Zonal or Regional
# Managed Instance Groups (MIG)
- Identical VMs created using an instance template
- Maintain certain number of instances
- Detect application failures using health checks (Self Healing)
- Auto Scaling
- Load Balancer
- Release new application versions without downtime
  - Rolling updates
  - Canary Deployment: Test new version with a group of instances before releasing it across all instances
# Creating Managed Instance Group (MIG)
- Instance template is mandatory
- Configure auto-scaling
  - max/Minimum number of instances
  - Autoscaling metrics: CPU Utilization target or Load Balancer Utilization
  - Autohealing
# Updating a Managed Instance Group (MIG)
- Rolling update
  - new instance template
- Rolling Restart/replace
  - No change in template BUT replace/restart existing VMs
- Configure Maximum surge, Maximum unavailable
# Playing with Managed Instance Groups - Command Line
- Create/auto scaling/update instance group
  - gcloud compute instance-groups managed create my-mig --zone us-central1-a --template my-instance-template --size 1
# Playing with Managed Instance Groups - Scenarios
- one healthy instance running all the time
  - gcloud compute instance-groups managed **set-autoscaling** my-group --max-num- replicas=1 **--min-num-replicas=1**
- no reduction in available number of instances
  - gcloud compute instance-groups managed **rolling-action start-update** my-group -- version=template=my-v1-template --max-surge 1 **--max-unavailable 0**
# Instance Group Scenarios (*sample-question*)
- You want MIG managed application to survive Zonal Failures
  - Create multiple zone MIG (or regional MIG)
- You want to create VMs of different configurations in the same group
  - Create Un-managed Instance Group
- You want to preserve VM state in an MIG
  - **Stateful MIG** - Preserve VM state (Instance name, attached Persistent disks and Metadata). Recommended for stateful workloads (database, data processing apps)
- You want high availability in an MIG even when there are hardware/so�ware updates
  - Use an instance template with availability policy 
  - automatic restart: enabled & on-host maintenance: migrate Ensures live migration and automatic restarts
- You want unhealthy instances to be automatically replaced
  - Configure health check on the MIG (self healing)
- Avoid frequent scale up & downs
  - Cool-down period/Initial delay
