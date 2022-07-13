# Cloud Storage
- Most popular, very flexible & inexpensive storage service
  - Serverless: Autoscaling and infinite scale
- Store large objects using a key-value approach
  - Treats entire object as a unit (Partial updates not allowed)
  - Also called Object Storage
- Store all file types - text, binary, backup & archives
# Cloud Storage - Objects and Buckets
- Objects are stored in buckets
  - Bucket names are globally unique
  - Can't start with goog prefix or should not contain google (even misspelled)
- Each object is identified by a unique key
  - Key is unique in a bucket
- Max object size is 5 TB
# Cloud Storage - Storage Classes - Introduction
- Different kinds of data can be stored in Cloud Storage
- Storage classes help to optimize your costs based on your access needs
  - durability of 99.999999999%(11 9’s)
# Cloud Storage - Storage Classes - Comparison
| Storage Class    | Name     | Minimum Storage duration | Typical Monthly availability                                | Use case                                   |
|------------------|----------|--------------------------|-------------------------------------------------------------|--------------------------------------------|
| Standard         | STANDARD | None                     | > 99.99% in multi region and dual region, 99.99% in regions | Frequently used data/Short period of time  |
| Nearline storage | NEARLINE | 30 days                  | 99.95% in multi region and dual region, 99.9% in regions    | Read or modify once a month on average     |
| Coldline storage | COLDLINE | 90 days                  | 99.95% in multi region and dual region, 99.9% in regions    | Read or modify at most once a quarter      |
| Archive storage  | ARCHIVE  | 365 days                 | 99.95% in multi region and dual region, 99.9% in regions    | Less than once a year                      |
# Features across Storage Classes
- Low latency
- Unlimited storage
- Committed SLA is 99.95% for multi region and 99.9% for single region for Standard, Nearline and Coldline storage classes
# Cloud Storage - Uploading and Downloading Objects
| Option                     | Recommended for Scenarios                                                                                                       |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Simple Upload              | Small files (that can be re uploaded in case of failures) + NO object metadata                                                  |
| Multipart upload           | Small files (that can be re uploaded in case of failures) + object metadata                                                     |
| Resumable upload           | Larger files. RECOMMENDED for most usecases(even for small files - costs one additional HTTP request)                           |
| Streaming transfers        | Upload an object of unknown size                                                                                                |
| Parallel composite uploads | File divided up to 32 chunks and uploaded in parallel. Significantly faster if network and disk speed are not limiting factors. |
| Simple download            | Downloading objects to a destination                                                                                            |
| Streaming download         | Downloading data to a process                                                                                                   |
| Sliced object download     | Slice and download large objects                                                                                                |
# Object Versioning
- Prevents accidental deletion & provides history
- Live version is the latest version
- Reduce costs by deleting older (noncurrent) versions!
# Object Lifecycle Management
- save costs by moving files automatically between storage classes?
  - Solution: Object Lifecycle Management
- Two kinds of actions
  - SetStorageClass actions (change from one storage class to another)
  - Deletion actions (delete objects)
- Allowed Transitions
  - (Standard or Multi-Regional or Regional) to (Nearline or Coldline or Archive)
  - Nearline to (Coldline or Archive)
  - Coldline to Archive
# Cloud Storage - Encryption
- Cloud Storage always encrypts data on the server side!
- Configure Server-side encryption
  - Google-managed encryption key - Default (No configuration required)
  - Customer-managed encryption keys - Created using Cloud Key Management Service (KMS). Managed by customer in KMS.
- (OPTIONAL) Client-side encryption - Encryption performed by customer before upload
# Cloud Storage - Scenarios
| Scenario                                                                                                       | Description                                                                                                        |
|----------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| How do you speed up large uploads (example: 100 GB) to Cloud Storage?                                          | Use Parallel composite uploads (File is broken in to small chunks and uploaded)                                    |
| You want to permanently store application logs for regulatory reasons. You don't expect to access them at all. | Cloud storage - Archive                                                                                            |
| Log files stored in Cloud storage. You expect to access them once in quarter.                                  | Cold Line                                                                                                          |
| How do you change storage class of an existing bucket in Cloud Storage?                                        | Step 1: Change Default Storage Class of the bucket. Step 2: Update the Storage Class of the objects in the bucket. |
# Cloud Storage - Command Line - gsutil
- (**REMEMBER**) gsutil is the CLI for Cloud Storage (NOT gcloud)

