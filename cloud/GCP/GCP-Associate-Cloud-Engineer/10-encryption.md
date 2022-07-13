# Data States
- Data at rest: Stored on a device or a backup
  - Examples : data on a hard disk, in a database, backups and archives
- Data in motion: Being transferred across a network
  - examples : Data copied from on-premise to cloud storage
  - Two Types:
    - In and out of cloud (from internet)
    - Within cloud
- Data in use: Active data processed in a non-persistent state
  - Example: Data in your RAM
# Encryption
- If you store data as is, what would happen if an unauthorized entity gets access to it?
- First law of security : Defense in Depth
- enterprises encrypt all data
  - Data on your hard disks
  - Data in your databases 
  - Data on your file servers
- Is it sufficient if you encrypt data at rest?
  - No. Encrypt data in transit - between application to database as well.
# Symmetric Key Encryption
- Symmetric encryption algorithms use the same key for encryption and decryption
- Key Factor 1: Choose the right encryption algorithm Key 
- Factor 2: How do we secure the encryption key? 
- Key Factor 3: How do we share the encryption key?
# Asymmetric Key Encryption
- Two Keys : Public Key and Private Key
- Also called Public Key Cyptography
# Cloud KMS
- Create and manage cryptographic keys (symmetric and asymmetric)
- Control their use in your applications and GCP Services
- Integrates with almost all GCP services that need data encryption:
  - Google-managed key: No configuration required
  - Customer-managed key: Use key from KMS
  - Customer-supplied key: Provide your own key
