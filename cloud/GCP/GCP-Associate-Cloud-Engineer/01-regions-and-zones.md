# Regions and Zones
## one data center
- high latency
- low availability
## multiple data center
- still slow from the world level
- higher availability than one, but still risky
## multiple regions
- low latency partly
- high availability
## regions
- 20+ regions
- Advantages
  - high availability
  - low latency
  - global footprint
  - adhere to government regulations
## zones
- high availability in the same region
- 1 region has 3 <= zones
- (REMEMBER) each zone has *one or more discrete clusters*
  - Cluster: distinct physical infrastructure that is housed in a data center
- (REMEMBER) zones in a region are connected through *low-latency* links
## regions and zones example
- regions: Dalles, Oregon, North America
- zones: us-west1-a, us-west1-b, us-west1-c

