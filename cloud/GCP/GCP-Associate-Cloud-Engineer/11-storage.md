# Storage Types - Block Storage and File Storage
- What is the type of storage of your hard disk?
  - Block Storage
- created a file share to share a set of files with your colleagues in a enterprise. 
  - File Storage
# Block Storage
- Harddisks attached to your computers
- Typically, ONE Block Storage device can be connected to ONE virtual server
  - (EXCEPTIONS) You can attach read only block devices with multiple virtual servers and certain cloud providers are exploring multi-writer disks as well
- HOWEVER, you can connect multiple different block storage devices to one virtual server
- Direct-attached storage (DAS) - Similar to a hard disk
- Storage Area Network (SAN) - High-speed network connecting a pool of storage devices 
  - Used by Databases - Oracle and Microso� SQL Server
# File Storage
- Media workflows need huge shared storage for supporting processes like video editing
- These file shares are shared by several virtual servers
# GCP - Block Storage and File Storage
- Block Storage
  - Persistent Disks: Network Block Storage
    - Zonal: Data replicated in one zone
    - Regional: Data replicated in multiple zone
  - Local SSDs: Local Block Storage
- File Storage
  - Filestore: High performance file storage
# GCP - Block Storage
- Local SSDs are physically attached to the host of the VM instance
  - Temporary data
  - Lifecycle tied to VM instance
- Persistent Disks are network storage
  - More durable
  - Lifecycle NOT tied to VM instance
# Local SSDs
- Physically attached to the host of VM instance
  - Provide very high (IOPS) and very low latency
  - Ephemeral storage
    - Enable live migration for data to survive maintenance events
  - Data automatically encrypted
    - CANNOT configure encryption keys
  - ONLY some machine types support
- **Remember**
  - Choose NVMe-enabled and multi-queue SCSI images for best performance
  - Larger Local SSDs (more storage), More vCPUs (attached to VM) => Even Better Performance
# Local SSDs - Advantages and Disadvantages
- Advantages
  - Higher throughput and lower latency
- Disadvantages
  - Ephemeral storage
  - CANNOT detach and attach it to another VM instance
# Persistent Disks (PD)
- Network block storage attached to your VM instance
- Provisioned capacity
- Very Flexible
  - Increase size when you need it
- Independent lifecycle from VM instance
- Options: Regional and Zonal
- Use case : Run your custom database
# Persistent Disks vs Local SSDs
| Feature | Persistent Disks | Local SSDs |
| ------ | ------ | ------ |
| Attachment to VM instance | As a network drive | Physically attached |
| Lifecycle | Separate from VM instance | Tied with VM instance |
| I/O Speed | Lower (network latency) | 10-100X of PDs |
| Snapshots | Supported | Not Supported |
| Use case | Permanent storage | Ephemeral storage |
# Persistent Disks - Standard vs Balanced vs SSD
| Feature                                        | Standard                  | Balanced                             | SSD               |
|------------------------------------------------|---------------------------|--------------------------------------|-------------------|
| Underlying Storage                             | Hard Disk Drive           | Solid State Drive                    | Solid State Drive |
| Referred to as                                 | pd-standard               | pd-balanced                          | pd-ssd            |
| Performance - Sequential IOPS (Big Data/Batch) | Good                      | Good                                 | Very Good         |
| Performance - Random IOPS (Transactional Apps) | Bad                       | Good                                 | Very Good         |
| Cost                                           | Cheapest                  | In Between                           | Expensive         |
| Use cases                                      | Big Data (cost efficient) | Balance between cost and performance | High Performance  |
# Persistent Disks - Snapshots
- Take point-in-time snapshots of your Persistent Disks
- can also schedule snapshots (configure a schedule)
- Snapshots are incremental
  - only deletes data which is NOT needed by other snapshots
- Keep similar data together on a Persistent Disk:
# Persistent Disks - Snapshots - Recommendations
- Avoid taking snapshots more often than once an hour
- Snapshots reduce performance
  - Schedule snapshots during off-peak hours
- Create an image from snapshot and use the image to create disks
- only deletes data which is NOT needed by other snapshots
# Playing with Machine Images
- **(Remember)** Machine Image is different from Image
- Multiple disks can be attached with a VM
  - One Boot Disk (Your OS runs from Boot Disk)
  - Multiple Data Disks
- An image is created from the boot Persistent Disk
- HOWEVER, a Machine Image is created from a VM instance:
- Recommended for disk backups, instance cloning and replication
# Compare
| Scenarios                  | Machine image  | Persistent disk snapshot | Custom image | Instance template |
|----------------------------|----------------|--------------------------|--------------|-------------------|
| Single disk backup         | Yes            | Yes                      | Yes          | No                |
| Multiple disk backup       | Yes            | No                       | No           | No                |
| Differential backup        | Yes            | Yes                      | No           | No                |
| Instance cloning           | Yes            | No                       | Yes          | Yes               |
| Base image for replication | No             | No                       | Yes          | No                |
# Playing with Machine Images - Command Line
- (**Remember**) gcloud commands for machine images are IN BETA
# Storage - Scenarios - Persistent Disks **(sample-example)**
| Scenario                                                                      | Solution                                                        |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------|
| You want to improve performance of Persistent Disks (PD)                      | Increase size of PD or Add more PDs. Increase vCPUs in your VM. |
| You want to increase durability of Persistent Disks (PD)                      | Go for Regional PDs (2X cost but replicated in 2 zones)         |
| You want to take hourly backup of Persistent Disks (PD) for disaster recovery | Schedule hourly snapshots!                                      |
| You want to delete old snapshots created by scheduled snapshots               | Configure it as part of your snapshot scheduling!               |
# Cloud Filestore
- Shared cloud file storage
- Suitable for high performance workloads
- Supports HDD (general purpose) and SSD (performance-critical workloads)
- Use cases : file share, media workflows and content management
# Review - Global, Regional and Zonal Resources
- Global 
  - Images 
  - Snapshots 
  - Instance templates (Unless you use zonal resources in your templates)
- Regional 
  - Regional managed instance groups 
  - Regional persistent disks
- Zonal 
  - Zonal managed instance groups 
  - Instances 
  - Persistent disks
# Storage - Scenarios **(sample-example)**
| Scenario                                                                                                | Solution               |
|---------------------------------------------------------------------------------------------------------|------------------------|
| You want Very High IOPS but your data can be lost without a problem                                     | Local SSDs             |
| You want to create a high perfomance file sharing system in GCP which can be attached with multiple VMs | Filestore              |
| You want to backup your VM configuration along with all its attached Persistent Disks                   | Create a Machine Image |
| You want to make it easy to launch VMs with hardened OS and customized software                         | Create a Custom Image  |

  
 
