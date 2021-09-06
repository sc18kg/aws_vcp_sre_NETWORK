# AWS Virtual Private Cloud (VPC)
![AWSIMAGE](AWS_deployment_networking_security.png)
## What is a VPC?
- AWS isolated virtual network - it allows us to control virtual network environment including selections of your own IPs address range, we can create multiple subnets within one VPC with specific network configuration. We can use both IPV4 and IPV6 for most resources, It provides security for your services or instances.

## Internet Gateway (IG)
- A horizontally scaled, redundant and highly available VPC component that allows the communication between the VPC and the internet which serves two purposes:
  - Provide a target in your VPC route tables for internet-routable traffic
  - Perform Network Address Translation for instances that have been assigned public IPV4 addresses.

![INTGATE](sch-General-InternetGateways.png)

## Subnets
- A logical subdivision of an IP network, This enables us to split the network into both public and private networks which allows for more efficiency. The smaller interconnected networks are used to help minimise traffic and also navigate traffic security.

![SUBNET](vpc-configuration-new.png)

## Route Tables (RT)
- Each VPC has an implicit router, and you use route tables to control where the network traffic is directed. Each subnet must also be associated with a route table, this can be seperate from the main route table. If not specified the network will default to the main route table. Each table contains a set of rules, called routes which are used to determine where the network traffic of the subnets or gateway is directed

![ROUTETABLE](TBSja.png)
## Network Access Control List (NACLs)
- Stateless, Controls the traffic to or from a subnet according to a set of inbound and outbound rules which we have to explicitly. This is representing network level security at the subnet level. For example an inbound rule might deny incoming traffic from a range of IP addresses, while an outbound rule might allow all traffic to leave the subnet.

![NACLS](nacl-example-diagram.png)
## Security Groups
- A security group acts as a virtual firewall for your instances to control the incoming and outgoing traffic. When launching an instance you can specify the security group it belongs to. The aim is to create a secure network with full control over who is able to access the instances.

## AWS Regions and Availablity Zones
- Regions
    - Each region is designed to be isolated from the other amazon regions, this achieves the greatest possible fault tolerance and stability. When viewing resources you are only able to see the resources that are tied to the specified region as they are not automatically replicated across regions.
- Availablity Zones
    - an availability zone is one or more discrete data centres with redundant power, networking and connectivity in a AWS region. This gives uses the ability to operate production applications and databases that are more highly available, fault tolerant and scaleable.
![INFRA](NA-500x500.f8738d3a3341a06a83fa838b927ba4b85b473918.png)
![key](mapkey.png) - Edge Locations
![region](region.png) - Regions

## Steps
- Create a VPC with an IPV valid CIDR block
  - `10.0.0.0/16` - Amy - `10.0.5.0/16`
- Create Internet Gateway (IG)
  - Attach the IG to our VPC - Each IG is a seperate resource that attaches to the VPC
- Create our route tables
  - Edit route and insert the IG in `target`
- Create Public Subnet
  - `10.0.1.0/24`
  - Associate Public Subnet with our RT
- Create Public NACLs
  - Set the inbound and outbound rules for the subnet `port:80`, `port:3000`, `port:22` 
- Create a Security Group for the app
