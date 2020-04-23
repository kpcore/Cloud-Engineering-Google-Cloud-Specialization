## 1. Module Overview

* GCP uses a software-defined network that is built on a global fiber infrastructure. This infrastructure makes GCP one of the world's largest and fastest networks. 
* Thinking about resources as services instead of as hardware, will help you understand the options that are available and their behavior.
* we start by introducing virtual private cloud or VPC, which is Google's managed networking functionality for your cloud platform resources. Then we dissect networking into its fundamental components which are projects, networks, subnetworks, IP addresses, routes and firewall rules, along with network pricing. 
* Next, you will explore GCP's network structure in a lab by creating networks of many different varieties and exploring the network of relationships between them. After that, we will look at common network designs. On a high level, GCP consists of regions, points of presence or PoPs, a global private network and services.
* A region is a specific geographical location where you can run your resources. Several regions that are currently operating as well as future regions. The number on each region represents the zones within that region.
* The PoPs are where Google's network is connected to the rest of the Internet. GCP can bring its traffic closer to its peers because it operates an extensive global network of interconnection points. This reduces costs and provides users with a they better experience.
* The network connects regions and PoPs and it's composed of a global network of fiber optic cables with several submarine cable investments.

## 2. Virtual Private Cloud

* You can define fine-grained network and policies within GCP and between GCP and On-premises or other public Clouds.
* Projects are going to encompass every single service that you use including networks. 
* Networks come in three different flavors; default, auto mode, and custom mode. 
* Subnetworks allow you to divide or segregate your environment. 
* Regions in zones represents Google's datacenters and they provide continuous Data Protection and high availability. 
* VPC provides IP addresses for internal and external use along with granular IP address range selections. 
* virtual machines, we will focus on configuring VM instances from a networking perspective. 
* We'll go over routes and firewall routes.

## 3. Projects, networks, and subnetworks

* Projects are the key organizer of infrastructure resources in GCP. A project associates objects and services with billing. Now, it's unique that projects actually contain entire networks. The default quota for each project is five networks but you can simply request additional quota using the GCP console. 
* These networks can be shared with other projects or they can be peered with networks in other projects. These networks do not have IP ranges but are simply a construct of all of the individual IP addresses and services within that network. 
* GCP networks are global spending all available regions across the world that I showed earlier. So you can have one network that later exists anywhere in the world, Asia, Europe, Americas, all simultaneously.  Inside a network you can segregate your resources with regional subnetworks. 
* Every project is provided with a default VPC network with presets subnets and firewall rules. Specifically a subnet is allocated for each region with non-overlapping sider blocks and firewall rules that allow ingress traffic from ICMP, RDP, and SSH traffic from anywhere as well as ingress traffic from within the default network for all protocols and ports. 
* In an Auto Mode network, one subnets from each region is automatically created within it. The default network is actually an auto mode network. These automatically created subnets uses set of predefined IP ranges with a /20 mask that can be expanded to a /16. All of these subnets fit within the 10.128.0.0/9 cider block. Therefore, as new GCP regions become available, new subnets and dose regions are automatically added to automotive networks using an IP range from that block.
* A Custom Mode network does not automatically create subnets. This type of network provides you with complete control over its subnets and IP ranges. You decide which subnets to create in regions you choose and using IP ranges you specify within the RFC 1918 address space. These IP ranges cannot overlap between subnets of the same network.
* Essentially your virtual machines even if they exist in different locations across the world, take advantage of Google's global fiber network. Those Virtual Machines appear as though they're sitting in the same rack, when it comes to a network configuration protocol. 
* subnetworks work on a regional scale. Because a region contains several zones, subnetworks can cross zones.
* This makes the first and second available addresses 10.0.0.2 and 10.0.0.3 which are assigned to the VM instances. The other reserved addresses in every subnets are the second-to-last address in the range and the last address which is reserved as the broadcast address. So to summarize, every subnet has four reserved IP addresses in its primary IP range.
* Speaking of IP addresses of a subnet, Google Cloud VPC's let you increase the IP address space of any subnets without any workload shutdown or downtime.
* network with subnets that have different subnet masks allowing for more instances in some subnets than others. This gives you flexibility and growth options to meet your needs but there are some things to remember. 
* The new subnet must not overlap with other subnets in these same VPC network in any region. Also, the new subnets must stay inside the RFC 1918 address spaces.
* The new network range must be larger than the original which means the prefix length value must be a smaller number. you cannot undo an expansion.
* auto mode subnets start with a /20 IP range. They can be expanded to a /16 IP range but no larger. Alternatively, you can convert the auto mode subnetwork to a custom mode subnetwork to increase IP range further. 
* Also avoid creating large subnets. Overly large subnets are more likely to cause site arrange collisions when using multiple network interfaces and VPC network peering or when configuring a VPN or other connections to an on-premises network. Do not scale your subnet beyond what you actually need.

## QuizNotes

*
	
## Resources

[Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/)

[Google's Netwoking Infastructure](https://peering.google.com/#/infrastructure)
