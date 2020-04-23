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

## 4. IP addresses

* In GCP, each virtual machine can have two IP addresses assigned. One of them is an internal IP address, which is going to be assigned via DHCP internally. Every VM that starts up and any service that depends on virtual machines gets an internal IP address. Example of such services are App Engine and Kubernetes Engine.
* When you create a VM in GCP, it's symbolic name is registered with an internal DNS service that translates the name to the internal IP address. DNS is scoped to the network, so it you can translate web URLs and VM names of hosts in the same network, but it can't translate host names from VMs in a different network.
* The other IP address is the external IP address, but this one is optional. You can assign an external IP address if your device or your machine is externally facing. That external IP address can be assigned from a pool, making it ephemeral, or it can be assigned a reserved external IP address, making it static. 
* If you preserve a static external IP address and do not assign it to a resource such as a VM instance or a forwarding rule, you are charged at a higher rate than for static and ephemeral external IP addresses that are in use.

## 5. Mapping IP addresses

* Regardless of whether you use an ephemeral or static IP address, the external address is unknown to the OS of the VM. The external IP address is mapped to the VMs internal address transparently by VPC.
* internal addresses, each in Instance has a host name that can be resolved to an internal IP address. This hostname is the same as the instance name. There's also an internal fully qualified domain name or fqdn for an instance that uses the format shown on the slide.
* If you delete and recreate an instance, the internal IP address can change. This change can disrupt connections from other compute engine resources, which must obtain the new IP address before they can connect again. However, the DNS name always points to specific instance no matter what the internal IP address is. 
* Each instance has a metadata server that also acts as a DNS resolver for that instance. The metadata server handles all DNS queries for local network resources and routes all other queries to Google's public DNS servers for public name resolution. 
* instance is not aware of any external IP address assigned to it. Instead, the network stores a lookup table that matches external IP addresses with the internal IP addresses of the relevant instances. 
* Instances with external IP addresses can allow connections from hosts outside of the project. Users can do so directly using the external IP address. 
* Public DNS records pointing to instances are not published automatically. However, admins can publish these using existing DNS servers. Domain and servers can be hosted on gcp using Cloud DNS. This is a managed service that's definitely worth considering 
* Cloud DNS is a scalable, reliable and managed authoritive domain name system or DNS service running on the same infrastructure as Google. Cloud DNS translate requests for domain names like google.com into IP addresses. Cloud DNS uses Google's Global Network of any cast name servers to serve your DNS zones from a download locations around the world providing lower latency and high availability for your users.
* High availability is very important because if you can't look up a domain name the internet might as well be down. That's why gcp offers a 100% up-time service level agreement or SLA for domains configured in cloud DNS.
* Cloud DNS lets you create and update millions of DNS records without the burden of managing your own DNS service and software. Instead, you use a simple user interface, command line face or API.
* Another networking feature of gcp is alias IP ranges, alias IP ranges that you assign a range of internal addresses as an alias to Virtual machines network interface. This is useful if you have multiple services running on a VM and you want to assign a different IP address to each service. In essence, you can configure multiple IP addresses representing containers or applications hosted in a VM. Without having to define a separate network interface. You just draw the alias IP range from the local subnets primary or secondary side arranges.

## 6. Routes and firewall rules

* By default, every network has routes that let instances in a network send traffic directly to each other even across subnets.  In addition, every network has a default route that directs packets to destinations that are outside the network. Although these routes cover most of your normal routing needs, you can also create special routes that overwrite these routes.
* Just creating a route does not ensure that your packet will be received by the specified next top. Firewall rules must also allow the packet. The default network has preconfigured firewall rules that allow all instances in the network to talk with each other.
* Routes match packets by destination IP addresses. However, no traffic will flow without also matching a firewall rule. A route is created when a network is created, enabling traffic delivery from anywhere. Also, a route is created when a subset is created. This is what enables VM's on the same network to communicate
* Each route in the routes collection may apply to one or more instances. A route applies to an instance if the network and instance tags match. If the network matches and there are no instance tags specified, the route applies to all instances in that network. 
* Compute engine then uses the routes collection to create individual read-only routing tables for each instance. Every virtual machine instance in the network is directly connected to this router, and all packets leaving a virtual machine instance are first handled at this layer before they are forwarded to the next hop. The virtual network router selects the next hop for a packet by consulting the routing table for that instance.
* GCP firewall rules to protect you virtual machine instances from unapproved connections both inbound and outbound known as ingress and egress respectively.
* Essentially, every VPC network functions as a distributed firewall. Although firewall rules are applied to the network as a whole, connections are allowed or denied at the instance level. You can think of the firewall as existing not only between your instances and other networks, but between individual instances within the same network. 
* GCP firewall rules are stateful. This means that if a connection is allowed between a source and a target or a target at a destination, all subsequent traffic in either direction will be allowed. In other words, firewall rules allow bidirectional communication once a session is established.
* Also if for some reason all firewall rules in a network are deleted, there is still an implied deny all ingress rule and an implied allow all egress rule for the network.
* You can express your desired firewall configuration as a set of firewall rules. Conceptually, a firewall rule is composed of the following parameters: 
* the direction of the rule Inbound connections are matched against ingress rules only, and outbound connections are matched against egress rules only. The source of the connection for ingress packets or the destination of the connection for egress packets. The protocol and port of the connection where any rule can be restricted to apply to specific protocols only or specific combinations of protocols imports only. The action of the rule which is to allow or deny packets that match the direction, protocol port and source or destination of the rule. The priority of the rule which governs the order in which rules are evaluated. The first matching rule is applied. The rule assignment. By default all rules are assigned to all instances but you can assign certain rules to certain instances only.
* Egress firewall rules control outgoing connections originated inside your GCP network. Egress allow rules allow outbound connections that match specific protocol ports and IP addresses. Egress deny rules prevent instances from initiating connections that match non permitted port protocol and IP range combinations. For egress firewall rules, destinations to which a rule applies may be specified using IP CIDR ranges. Specifically, you can use the destination ranges to protect from undesired connections initiated by a VM instance towards an external host as shown on the left. You can also use destination ranges to prevent undesired connections from internal VM instances to specific GCP CIDR ranges.
* Ingress firewall rules protect against incoming connections to the instance from any source. Ingress allow rules allow specific protocol ports and IP ranges to connecting. The firewall prevents instances from receiving connections on non-permitted ports and protocols. Rules can be restricted to only affect particular sources. Source CIDR ranges can be used to protect an instance from undesired connections coming either from external networks or from GCP IP ranges.
* You can control ingress connections from a VM instance by constructing inbound connection conditions using source CIDR ranges, protocols, or ports.

## QuizNotes

*
	
## Resources

[Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/)

[Google's Netwoking Infastructure](https://peering.google.com/#/infrastructure)

[IP Addresses](https://cloud.google.com/compute/docs/ip-addresses/)

[Internal DNS](https://cloud.google.com/compute/docs/internal-dns)

[Cloud DNS Service Level Agreement (SLA)](https://cloud.google.com/dns/sla)

[Alias IP ranges overview](https://cloud.google.com/vpc/docs/alias-ip)

[Cloud DNS documentation](https://cloud.google.com/dns/docs/)

[Firewall rules overview](https://cloud.google.com/vpc/docs/firewalls#firewall_rule_components)

