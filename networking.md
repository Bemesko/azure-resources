# Azure Networking

## Sources

https://www.youtube.com/watch?v=feQvnIUJ3Iw&ab_channel=K21Academy

## Virtual Networks Overview

### Fundamentals
- Basics
  - IPv4 
    - X.X.X.X, each X can be 0 to 255
    - Classes
        - A: 0 - 126
        - B: 128 - 191
        - C: 192 - 223
        - D: 224 - 239
        - E: 240 - 255
        - 127 - Loopback
    - CIDR: Classless Interdomain Routing
      - X.X.X.X/YY
      - Bigger masks leave space for less IPs in the network
    - Public vs Private
      - Public
            - Microsoft gets their public IPs from IANA
            - Public IPs are generally used for management
      - Private:
        - Generally used for data traffic
        - Private Ranges:
            - 10.0.0.0 - 10.255.255.255
            - 172.16.0.0 - 172.31.255.255
            - 192.168.0.0 - 192.168.255.255
            - Addresses can be used once per subscription in Azure
#### Virtual Networks
  - Rule of Thumb: Everyone in the vnet can talk to everyone in the vnet
    - To remedy this, the vnet can be limited to subnets
  - Azure restricts the use of addresses 0, 1, 2, 3 and 255 for subnets
    - 0: Network Identifier
    - 1, 2, 3: Reserved by Azure
    - 255: Broadcast ID
  - Limit of vnets per Azure subscription
    - soft: 50 vnets
      - Once the number reaches this, anyone can call Microsoft to increase their limit to 500
    - hard: 500 vnets
- Virtual Networks can connect to either other virtual networks or on-premises networks

#### Virtual Network Security
- Shared Responsibility: Microsoft does some things, but the customers also have to enforce security on their side
- Vnet perimeter security:
  - DDoS
  - Firewall (firewall as a service)
    - Expensive
    - Access Control Lists (ACL) can be setup to allow or deny certain sites

### IP Addresses
- Public: Can be accesses directly from anywhere
- Private: Can only be accessed directly if you're connected to the vnet
- Dynamic: The IP itself isn't guaranteed to remain the same
  - Example: Virtual Machines
- Static: The IP will always be the same

### Route Tables
- Use cases:
  - Application in vnet1 needs to access some resource outside of the network, some on premises application or something in vnet2
- Route tables help with connections outside the current vnet
- Rules allow the redirection of traffic from certain IP ranges to other types of resources (next hop types)
- Route tables need to be associated to a subnet

### Network Security Group (NSG)
- Sort of a firewall at a network traffic
- Filters traffic coming to and from a network
- Has security rules for ingress (what goes in) and egress (what comes out)
  - Each rule can allow or deny a collection of IPs
- Can be associated with a subnet or a Network Interface Card

### Service Endpoint
- Helps filter traffic to a particular azure service
- Are created in the vnet options
- Creates a definition for a resource inside the vnet

### Application Security Group
- Logical grouping of virtual machines that share common rules
- It's easier to set up than specifying separate routing tables for each virtual machine
- Practice Scenario:
  - WebServer ASG can access only AppServers and be accessed by the internet
  - AppServers ASG can access DbServers and be accessed by WebServers
  - DbServers ASG can only be accessed by AppServers

**Checkpoint:** 43:17

## Doubts
- What is the Propagate Gateway Routes option when creating a route table?
- How can service endpoints be accessed in practice?
- Are ASGs useful only for virtual machines?