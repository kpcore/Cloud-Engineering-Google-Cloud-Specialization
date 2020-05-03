## 1. Module Overview

* In this module, we focus on Interconnecting Networks. Different applications and workloads require different network connectivity solutions. That is why Google supports multiple ways to connect your infrastructure to GCP. 
* In this module, we'll focus on GCP's hybrid connectivity products which are Cloud VPN, Cloud VPN, and Peering. We'll also look at options for sharing VPC network within GCP.

## 2. Cloud VPN

* Cloud VPN securely connects your on-premise network to your GCP VPC network through an IPSec VPN tunnel. Traffic traveling between the two networks is encrypted by one VPN gateway.
* Then decrypted by the other VPN gateway. This protects your data as it travels over the public internet. That's why Cloud VPN is useful for low volume data connections.
* As a managed service Cloud VPN provides an SLA of 99.9 percent service availability and supports site to site VPN static and dynamic routes, and IKEv1 and IKEv2 ciphers. 
* Cloud VPN doesn't support new cases where a client computers need to dial in to a VPN using client VPN software. Also, dynamic routes are configured with Cloud Router
* Let me walk through an example of Cloud VPN. This diagram shows a simple VPN connection between your VPC and on-premise network. Your VPC network has subnets in US-east one and US-west one. With GCP resources in each of those regions. These resources are able to communicate using their internal IP addresses because routing within a network is automatically configured, assuming that firewall rules allow the communication.
* Now, in order to connect to your on-premise network and its resources you need to configure your Cloud VPN gateway on-premise VPN gateway and to VPN tunnels. The Cloud VPN gateway is a regional resource that uses a regional external IP address. Your on-premise VPN gateway can be a physical device in your data center or a physical or software based VPN offering in another Cloud providers network. 
* This VPN gateway also has an external IP address. A VPN tunnel then connects your VPN gateways and serves as the virtual medium through which encrypted traffic is passed. In order to create a connection between two VPN gateways you must establish two VPN tunnels. Each tunnel defines the connection from the perspective of its gateway and traffic can only pass when the pair of tunnels established. Now, one thing to remember when using Cloud VPN is that the maximum transmission unit or MTU for your on-premises VPN gateway cannot be greater than 1,460 bytes. This is because of the encryption and encapsulation of packets.
* I mentioned earlier that Cloud VPN supports both static and dynamic routes. In order to use dynamic routes you need to configure Cloud Router. Cloud Router can manage routes from Cloud VPN tunnel using border gateway protocol or BGP.
* This routing method allows for routes to be updated and exchanged without changing the tunnel configuration. For example, this diagram shows two different regional subnets in a VPC network namely tests and prod. The on-premise network has 29 subnets and the two networks are connected through Cloud VPN tunnels. Now, how would you handle adding new subnets? For example, how would you add a new staging subnet in the GCP network and a new on-premise 10.0.30.0/24 subnet to handle growing traffic in your data center?
* To automatically propagate network configuration changes the VPN tunnel uses Cloud Router to establish a BGP session between the VPC and the on-premise VPN gateway which must support BGP. The new subnets are then seamlessly advertised between networks. This means that instances in the new subnets can start sending and receiving traffic immediately as you will explore in the upcoming lab. 
* To set up BGP an additional IP address has to be assigned to each end of the VPN tunnel. These two IP addresses must be link-local IP addresses. Belonging to the IP address range 169.254.0.0/16. These addresses are not part of IP address space of either network and are used exclusively for establishing a BGP session.
* Instances need to be stopped before you can make changes to their network interfaces.

## 3. Cloud Interconnect and Peering

* let's talk about Cloud Interconnect and Peering services. There are different Cloud Interconnect and Peering services available to connect your infrastructure to Google's network. 
* These services can be split into dedicated versus shared connections and layer two verses layer three connections. The services are Direct Peering, Carrier Peering, Dedicated Interconnect, and Partner Interconnect. 
* Dedicated connections provide a direct connection to Google's network. But, shared connections provide a connection to Google's network through a partner. 
* Layer two connections use a VLAN that pipes directly into your GCP environment, providing connectivity to internal IP addresses in the RFC 1918 address space. 
* Layer three connections provide access to G Suite services, YouTube and Google Cloud APIs using public IP addresses.
* Now as I just explained earlier, Google also offers its own Virtual Private Network service called Cloud VPN. This service uses the public Internet but traffic is encrypted and provides access to internal IP addresses. 
* That's why Cloud VPN is a useful addition to Direct Peering and Carrier Peering. Let me explain the Cloud Interconnect and Peering services separately first and then I'll provide some guidance on choosing the right connection.

## 4. Cloud Interconnect

* Dedicated Interconnect provides direct physical connections between your On-premise network and Google's network. This enables you to transfer a large amount of data between networks which can't be more cost-effective than purchasing additional bandwidth over the public Internet.
* In order to use Dedicated Interconnect, you need to provision a cross-connect between the Google network and your own router in a common co-location facility, as shown in this diagram. To exchange routes between the networks, you configure a BGP session over the interconnect between the Cloud Router and the On-premise router. This will allow user traffic from the on-premise network to reach GCP resources on the VPC network and vice-versa.
* Dedicated Interconnect can be configured to offer a 99.9 percent or a 99.99 percent uptime SLA. See the Dedicated Interconnect documentation for details on how to achieve these SLAs.
* In order to use Dedicated Interconnect, your network must physically meet Google's network in a supported co-location facility. This map shows the location where you can create dedicated connections. 
* That's when you want to consider a Partner Interconnect. Partner Interconnect provides connectivity between your on-premise network and your VPC network through a supported service provider. This is useful if your data center is in the physical location that cannot reach a Dedicated Interconnect co-location facility or if your data needs don't warrant a Dedicated Interconnect. In order to use Partner Interconnect, you work with the supported service provider to connect your VPC and on-premise networks.
* These service providers have existing physical connections to Google's network that they make available for their customers to use. After you establish connectivity with the service provider, you can request a Partner Interconnect connection from your service provider then establish a BGP session between your Cloud Router and On-premise Router to start passing traffic between your networks via the service providers network.
* Partner Interconnect can be configured to offer a 99.9 percent or 99.99 percent uptime SLA between Google and the service provider. See the Partner Interconnect documentation for details on how to achieve these SLAs. Let me compare the Interconnect options that we just discussed. All of these options provide internal IP address access between resources in your On-premise network and in your VPC network. The main differences are the connection capacity and the requirements for using a service. 
* The IPSec VPN tunnels that Cloud VPN offers have a capacity of 1.5 to 3 Gbps per tunnel and require VPN device on your On-premise network. The 1.5 Gbps capacity applies to the traffic that traverses the public Internet and the three Gbps capacity applies to the traffic that is traversing a Direct Peering link. You can configure multiple tunnels if you want to scale this capacity. 
* Dedicated Interconnect has a capacity of 10 Gbps per link and requires you to have a connection in a Google supported co-location facility. You can have up to eight links to achieve multiples of 10 Gbps by 10 Gbps is the minimum capacity. As of this recording, there is a Beta feature that provides 100 Gbps per link with a maximum of two links. Keep in mind that features that are in beta are not covered by any SLA or deprecation policies and might be subject to backward-incompatible changes.
* Partner Interconnect has a capacity of 50 Mbps to 10 Gbps per connection and requirements depend on the service provider. My recommendation is to start with VPN tunnels. When you need enterprise-grade connection to GCP, switch to Dedicated Interconnect or Partner Interconnect depending on your proximity to a co-location facility and your capacity requirements.

## 5. Peering

* Let's talk about the Cloud Peering services which are Direct Peering and Carrier Peering. These services are useful when you require access to Google and Google Cloud properties. Google allows you to establish a direct peering connection between your business network and Google's.
* With this connection, you will be able to exchange internet traffic between your network and Google's at one of the Google's broad-reaching Edge network locations.
* Direct Peering with Google is done by exchanging BGP routes between Google and the peering entity. After a direct peering connection is in place, you can use it to reach all the Google's services including the full suite of Google Cloud Platform products.
* Unlike dedicated interconnect, direct peering does not have an SLA. In order to use direct peering, you need to satisfy the peering requirements in the links section of this video. GCP's Edge points of presence or PoPs are where Google's network connects to the rest of the internet via peering. PoPs are present on over 90 internet exchanges and at over 100 interconnection facilities around the world. 
* If you look at this map and say, "hey, I am nowhere near one of these locations," you will want to consider Carrier Peering. If you require access to Google public infrastructure and cannot satisfy Google's peering requirements, you can connect via a carrier peering partner. Work directly with your service provider to get the connection you need and to understand the partners requirements. 
* Now, just like direct peering, carrier peering also does not have an SLA. Let me compare the peering options that we just discussed. All of these options provide public IP address access to all of Google's services.
* The main differences are capacity and the requirements for using a service. Direct peering has a capacity of 10Gbps per link and requires you to have a connection in a GCP Edge point of presence. Carrier peering's capacity and requirements vary depending on the service provider that you work with.

## 6. Choosing a Connection

* I started this lesson by introducing the five different ways to connect your infrastructure to GCP. I split these sources into dedicated versus shared connections and Layer 2 versus Layer 3 connections. Another way to organize these sources is by interconnect services and by peering services.
* Interconnect services provide direct access to RFC1918 IP addresses in your VPC with an SLA. Peering services in contrast offer access to Google public IP addresses only without an SLA. Another way to choose the right service that meets your needs is with a flow diagram. Let me walk you through this diagram from the top using the assumptions that you want to extend your infrastructure to the Cloud.
* Ask yourself whether you need to extend your network for G Suite services, YouTube or Google Cloud APIs. If you do, choose one of the peering services. If you can meet Google's direct peering requirements, choose Direct Peering. Otherwise, choose Carrier Peering. If you don't need to extend your network for G Suite services or Google Cloud APIs, but want to extend the reach of your network to GCP, you want to pick one of the interconnect services.
* If you cannot meet Google at one of its co-location facilities, choose Cloud VPN or Partner Interconnect. This choice will depend on your bandwidth and encryption requirements along with the purpose of the connection. Specifically, if you have modest bandwidth needs, will use the connection for short durations and trials, and require an encrypted channel, choose Cloud VPN.
* Otherwise, choose Partner Interconnect. If you can meet Google at one of its co-location facilities you, might jump to Dedicated Interconnect. However, if you cannot provide your own encryption mechanism for sensitive traffic, feel that a 10 Gbps connections is too big or won't access to multiple clouds, you will want to consider Cloud VPN or Partner Interconnect instead.

## 7. Shared VPC and VPC Peering

* Let's move our attention from hybrid connectivity to shared VPC networks. In the simplest Cloud environment, a single project might have one VPC network, spanning many regions with VM instances hosting very large and complicated applications. However, many organizations commonly deploy multiple isolated projects with multiple VPC networks and sublets.
* In this lesson, we are going to cover two configurations for sharing VPC networks across GCP projects. First, we will go over shared VPC which allows you to share a network across several projects in your GCP organization.
* Then, we will go over VPC Network Peering which allows you to configure private communication across projects in same or different organizations.
* Shared VPC allows an organization to connect resources from multiple projects to a common VPC network. This allows the resources to communicate with each other securely, and efficiently using internal IPs from that network.
* For example, in this diagram, there is one network that belongs to the web application servers project. This network is shared with three other projects. Namely, the recommendation service, the personalization service, and the analytics service.
* Each of those service projects has instances that are in the same network as the web application server, and allow for private communication to that server using the internal IP addresses. The web application server communicates with clients and on-premises, using the server's external IP address.
* The backend services in contrast can not be reached externally because they only communicate using internal IP addresses. When you shared VPC, you designate a project as a host project, and attach one or more other service projects to it.
* In this case, the web application servers project is the host project. The three other projects are the service projects. The overall VPC network is called the shared VPC network.
* VPC Network Peering in contrast, allows private RFC 1918 connectivity across two VPC networks, regardless of whether they belong to the same project, or the same organization. Now, remember that each VPC network will have firewall rules that define what traffic is allowed or denied between the networks.
* For example, in this diagram, there are two organizations that represent a consumer and a producer respectively. Each organization has its own organization node. VPC network, virtual machine instances, network admin, and instance admin.
* In order for VPC Network Peering to be established successfully, the producer network admin needs to peer the producer network with the consumer network. The consumer network admin needs to peer the consumer network with the producer network.
* When both peering connections are created, the VPC Network Peering session becomes active and routes are exchanged. This allows the virtual machine instances to communicate privately using their internal IP addresses.
* VPC Network Peering is a decentralized or distributed approach to multiproject networking. Because each VPC network, may remain under the control of separate administrator groups, and maintains its own global firewall, and routing tables.
* Historically, such projects would consider external IP addresses or VPNs to facilitate private communication between VPC networks. However, VPC Network Peering does not incur the network latency, security, and cost drawbacks that are present when using external IP addresses or VPNs.
* Now that we've talked about shared VPC, and VPC Network Peering, let me compare both of these configurations to help you decide which is appropriate for a given situation.
* If you want to configure a private communication between VPC networks in different organizations, you have to use VPC Network Peering. Shared VPC only works within the same organization. Somewhat similarly, if you want to configure private communication between VPC networks in the same project, you have to use VPC Network Peering. This doesn't mean that the networks need to be in the same project, but they can be. Shared.
* VPC, only works across projects. In my opinion, the biggest difference between the two configurations is the network administration models. Shared VPC is a centralized approach to multi-project networking because security and network policy occurs in a single designated VPC network.
* In contrast, VPC Network Peering is a decentralized approach because each VPC network can remain under the control of separate administrator groups, and maintains its own global firewall, and routing tables.

## QuizNotes

* What is the purpose of Virtual Private Networking (VPN)?
	* To enable a secure communication method (a tunnel) to connect two trusted environments through an untrusted environment, such as the Internet.
		* VPNs use IPSec tunnels to provide an encapsulated and encrypted path through a hostile or untrusted environment.
* Which GCP Interconnect service requires a connection in a GCP colocation facility and provides 10 Gbps per link?
	* Dedicated Interconnect
		* Dedicated Interconnect requires a connection in a GCP colocation facility and provides 10 Gbps per link.
* If you cannot meet Google’s peering requirements, which network connection service should you choose to connect to G Suite and YouTube?
	* Carrier Peering
		* Carrier Peering allows you to connect to G Suite and YouTube without meeting Google’s peering requirements.
* Which of the following approaches to multi-project networking, uses a centralized network administration model?
	* Shared VPC
		* Shared VPC is a centralized approach to multi-project networking, because security and network policy occurs in a single designated VPC network.

## Resources

[Cloud VPN overview](https://cloud.google.com/vpn/docs/concepts/overview)

[MTU considerations](https://cloud.google.com/vpn/docs/concepts/mtu-considerations)

[Dedicated Interconnect Overview](https://cloud.google.com/interconnect/docs/concepts/dedicated-overview#redundancy)

[Colocation Facility Locations](https://cloud.google.com/interconnect/docs/concepts/colocation-facilities)

[Supported Service Providers](https://cloud.google.com/interconnect/docs/concepts/service-providers)

[Partner Interconnect Overview](https://cloud.google.com/interconnect/docs/concepts/partner-overview#redundancy)

[Google Peering](https://peering.google.com/#/options/peering)

[PeeringDB](https://www.peeringdb.com/asn/15169)

[PeeringDB](https://www.peeringdb.com/net/4319)

[Carrier Peering](https://cloud.google.com/interconnect/docs/how-to/carrier-peering#service_providers)