# Cloud VPN
- Cloud VPN - Connect on-premise network to the GCP network
  - Implemented using IPSec VPN Tunnel
  - Traffic through internet (**public**)
  - Traffic encrypted using Internet Key Exchange protocol
- Two types of Cloud VPN solutions:
  - HA VPN (SLA of 99.99% service availability with two external IP addresses)
    - Only dynamic routing (BGP) supported
  - Classic VPN (SLA of 99.9% service availability, a single external IP address)
    - Supports Static routing (policy-based, route-based) and dynamic routing using BGP
# Cloud Interconnect
- High speed physical connection between on-premise and VPC networks:
  - Highly available and high throughput
  - Two types of connections possible
    - Dedicated Interconnect - 10 Gbps or 100 Gpbs configurations
    - Partner Interconnect - 50 Mbps to 10 Gbps configurations
- Data exchange happens through a **private network**:
  - Communicate using VPC network's internal IP addresses from on-premise network
  - Reduces egress costs
    - As public internet is NOT used
- Supported Google API's and services can be privately accessed from on-premise
- Use **only for high bandwidth** needs
  - For low bandwidth, Cloud VPN is recommended
# Direct Peering
- Connect customer network to google network using network peering
  - Direct path from on-premises network to Google services
- Not a GCP Service
  - Lower level network connection outside of GCP
- **NOT RECOMMENDED**
  - Use Cloud Interconnect and Cloud VPN
