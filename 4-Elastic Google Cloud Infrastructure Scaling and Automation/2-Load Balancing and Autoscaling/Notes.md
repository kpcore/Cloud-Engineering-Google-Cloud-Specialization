## 1. Module Overview

* In this module, we focus on load balancing and auto-scaling. Cloud Load Balancing gives you the ability to distribute load balanced computer resources in single or multiple regions to meet your high availability requirements, to put your resources behind a single anycast IP address, and to scale your resources up or down with intelligent autoscaling.
* Using Cloud Load Balancing, you can serve content as close as possible to your users on a system that can respond to over one million queries per second. Cloud Load Balancing is a fully distributed software defined managed service. It is not instance or device based so you do not need to manage a physical load balancing infrastructure.
* GCP offers different types of load balancers that can be divided into two categories, global and regional. The global load balancers are the HTTP, HTTPS, SSL proxy, and TCP proxy load balancers. These load balancers leverage the Google front ends which are software defined, distributed systems that sit in Google's Point-of-Presence and are distributed globally.
* Therefore, you want to use a global load balancer when your users and instances are globally distributed. Your users need access to the same application and content and you want to provide access using a single anycast IP address. 
* The regional load balancers are the internal and network load balancers and they distribute traffic to instances that are in a single GCP region. The internal load balancer uses Andromeda which is GCP's software defined network virtualization stack and the network load balancer uses Maglev which is a large distributed software system.
* There's also another internal load balancer for HTTP, HTTPS traffic, but it's in beta as of this recording. The sixth load balancer is a proxy based regional layer seventh load balancer that enables you to run and scale your services behind a private load balancing IP address that is accessible only in the load balancers' region in your VPC network.
* In this module, we will cover the different types of load balancers that are available in GCP. We will also go over the managed instance groups and their autoscaling configurations which can be used by these load balancing configurations. You will explore many of the covered features and services throughout the two labs of this module. I will wrap things up by helping you determine which GCP load balancer best meets your needs.

## 2. Managed instance groups

* A managed instance group is a collection of identical virtual machine instances that you control as a single entity using an instance template. You can easily update all the instances in the group by specifying a new template in a rolling update.
* Also, when your application requires additional compute resources, managed instance groups can automatically scale the number of instances in the group. Managed instance groups can work with load balancing services to distribute network traffic to old instances in the group.
* If an instance in the groups stops, crashes, or is deleted by an action other than the instance groups command, the managed instance group automatically recreates the instance so it can resume its processing tasks. The recreated instance uses the same name and the same instance template as the previous instance. Managed instance groups can automatically identify and recreate unhealthy instances in a group to ensure that all the instances are running optimally.
* Regional managed instance groups are generally recommended over zonal managed instance groups because they allow you to spread the application load across multiple zones instead of confining your application to a single zone or you're having to manage multiple instance groups across different zones.
* This replication protects against zonal failures and unforeseen scenarios where an entire group of instances in a single zone malfunctions. If that happens, your application can continue serving traffic from instances running in another zone of the same region.
* In order to create a managed instance group, you first need to create an instance template. Next, you are going to create a managed instance group of end specific instances. The instance group manager then automatically populates the instance group based on the instance template. You can easily create instance templates using the GCP console.
* The instance template dialogue looks and works exactly like creating an instance, except that the choices are recorded so that they can be repeated. When you create an instance group, you define the specific rules for the instance group.
* First, decide whether the instance group is going to be single or multi zoned and where those locations will be. Second, choose the ports that you are going to allow and load balance across. Third, select the instance template that you want to use. Fourth, decide whether you want to auto-scale and under what circumstances. 
* Finally, consider creating a health check to determine which instances are healthy and should receive traffic. Essentially, you're still creating virtual machines, but you're applying more rules to that instance group.

## 3. Autoscaling and health checks

* Let me provide more details on the autoscaling and health checks of the managed instance group. As I mentioned earlier, managed instance groups offer autoscaling capabilities that allow you to automatically add or remove instances from a managed instance group based on increase or decrease in load.
* Autoscaling helps your applications gracefully handle increase in traffic and reduces cost when the need for resource is lower. You just define the autoscaling policy, and the autoscaler performs automatic scaling based on the measured load.
* Applicable autoscaling policies include scaling based on CPU utilization, load balancing capacity, or monitoring metrics, or by a queue-based workload like Cloud Pub/Sub. For example, let's assume you have two instances that are at 100 percent and 85 percent CPU utilization as shown on this slide. If your target CPU utilization is 75 percent, the autoscaler will add another instance to spread out the CPU load and stay below the 75 percent target CPU utilization.
* Similarly, if the overall load is much lower than the target, the autoscaler will remove instances as long as that keeps the overall utilization below the target. Now, you might ask yourself, how do I monitor the utilization of my instance group?
* When you click on an instance group or even an individual virtual machine, a graph is presented. By default, you will see the CPU utilization over the past hour. But you can't change the timeframe and visualize other metrics like disk and network usage.
* These graphs are very useful for monitoring your instances, utilization, and for determining how best to configure your autoscaling policy to meet changing demands. If you monitor the utilization of your virtual machine instances and Stackdriver monitoring, you can even set up alerts through several notification channels.
* Another important configuration for a managed instance group and load balancer is a health check. A health check is very similar to an Uptime check in Stackdriver. You just define a protocol, port, and health criteria as shown in the screenshot.
* Based on this configuration, GCP computes a health state for each instance. The health criteria defines how often to check whether an instance is healthy. That's the check interval.
* How long to wait for a response? That's the timeout. How many successful attempts are decisive? That's the healthy threshold. How many failed attempts are decisive? That the unhealthy threshold. In the example on this slide, the health check would have to fill twice over a total of 15 seconds before an instance is considered unhealthy.

## 4. Overview of HTTP(S) load balancing

* Now, let's talk about HTTPS Load Balancing which acts at layer seven of the OSI model. This is the application layer which deals with the actual content of each message allowing for routing decisions based on the URL.
* GCP HTTPS load balancing provides global load balancing for HTTPS requests destined for your instances. This means that your applications are available to your customers at a single any cast IP address, which simplifies your DNS setup. HTTPS load balancing balances HTTP and HTTPS traffic across multiple backend instances and across multiple regions.
* HTTP requests are load balanced on port 80 or 8080, and HTTPS requests are load balanced on port 443. This load balancers supports both IPv4 and IPv6 clients, is scalable, requires no pre-warming, and enables content-based and cross-regional load balancing. You can configure your own maps that route some URLs to one set of instances and route other URLs to other instances.
* Requests are generally routed to the instance group that is closest to the user. If the closest instance group does not have sufficient capacity, the request is sent to the next closest instance group that does have the capacity. You will get to explore most of these benefits in the first lab of the module.
* Let me walk through the complete architecture of an HTTPS load balancer by using this diagram. A Global Forwarding Rule direct incoming requests from the Internet to a target HTTP proxy. The target HTTP proxy checks each request against a URL map to determine the appropriate backend service for the request.
* For example, you can send requests for www.example dot com slash audio to one backend service, which contains instances configured to deliver audio files, and the request for www.example dot com slash video to another backend service which contains instances configured to deliver video files.
* The backend service directs each request to an appropriate backend based on solving capacity zone and instance held of its attached backends. The backend services contain a health check, session affinity, a timeout setting, and one or more backends.
* A health check pulls instances attached to the backend service at configured intervals. Instances that pass the health check are allowed to receive new requests. Unhealthy instances are not sent requests until they are healthy again.
* Normally, HTTPS load balancing uses a round robin algorithm to distribute requests among available instances. This can be overridden with session affinity. Session affinity attempts to send all requests from the same client to the same Virtual Machine Instance.
* Backend services also have a timeout setting, which is set to 30 seconds by default. This is the amount of time the backend service will wait on the backend before considering the request a failure. This is a fixed timeout not an idle timeout. If you require longer lived connections, set this value appropriately.
* The backends themselves contain an instance group, a balancing mode, and a capacity scalar. An instance group contains Virtual Machine Instances. The instance group may be a managed instance group with or without autoscaling or an unmanaged instance group.
* A balancing mode tells the load balancing system how to determine when the backend is at full usage. If older backends for the backend service in a region are at the full usage, new requests are automatically routed to the nearest region that can still handle requests.
* The balancing mode can be based on CPU utilization or requests per second. A capacity setting is an additional control that interacts with the balancing mode setting. 
* For example, if you normally want your instances to operate at a maximum of 80 percent CPU utilization, you would set your balancing mode to 80 percent CPU utilization and your capacity to 100 percent. If you want to cut instance utilization in half, you could leave the balancing mode at 80 percent CPU utilization and set capacity to 50 percent.
* Now, any changes to your backend services are not instantaneous. So don't be surprised if it takes several minutes for your changes to propagate throughout the network.

## 5. Example: HTTP load balancer

* Let me work through an HTTP load balancer in action. The project on this slide has single global IP address, but users enter the Google Cloud network from two different locations, one in North America, and one in EMEA.
* First, the global forwarding rule directs incoming requests to the target HTTP proxy. The proxy checks the URL map to determine the appropriate back-end service for the request.
* In this case, we're serving a guestbook application with only one back-end service. The back-end service has two back-ends, one in US Central 1-a, and one in Europe West 1-d. Each of those back-ends consist of a managed instance group.
* Now, when a user request comes in, the load balancing service determines the approximate origin of the request from the source IP address. The load balancing service also knows the locations of the instances owned by the back-end service, their overall capacity and their overall current usage.
* Therefore, if the instances closest to the user has available capacity, the request is forwarded to that closest set of instances. In our example, traffic from the user in North America, would be forwarded to the managed instance group in US Central 1-a, and the traffic from the user in EMEA would be forwarded to the managed instance group in Europe West 1-d.
* If there are several users in each region, the incoming requests to the given region are distributed evenly across all available back-end services, and instances in that region. If there are no healthy instances, with available capacity in a given region, the load balancer instead sends the request to the next closest region with available capacity.
* Therefore, traffic from the EMEA user, could be forwarded to the US Central 1-a back-end, if the Europe West 1-d back-end does not have capacity, or has no healthy instances as determined by the health checker. This is referred to as cross-region load balancing.
* Another example, of an HTTPS load balancer, is a content-based load balancer. In this case there are two separate back-end services that handle either web or video traffic.
* The traffic is split by the load balancer based on the URL header as specified in the URL map, if the user's navigating to slash video, the traffic is sent to the back-end video service and if the user is navigating anywhere else, the traffic is sent to the web service back-end. All of that is achieved with a single global IP address.
* The HTTP load balancer should forward traffic to the region that is closest to you.

## 6. HTTP(S) load balancing 

* An HTTP(S) load balancer has the same basic structure as the HTTP load balancer, but differs in the following ways. An HTTP(s) load balancer uses a target HTTPS proxy instead of a target HTTP proxy.
* An HTTPS load balancer requires at least one signed SSL certificate installed on the target HTTPS proxy for the load balancer. The client SSL session terminates at the load balancer. HTTPS load balancer support the QUIC transport layer protocol.
* QUIC is a transport layer protocol that allows faster client connection initiation, eliminates head of line blocking in multiplexed streams, and supports connection migration when a client's IP address changes.
* To use HTTPS, you must create at least one SSL certificate that can be used by the target proxy for the load balancer. You can configure the target proxy with up to 10 SSL certificates.
* For each SSL certificate, you first create an SSL certificate resource which contains the SSL certificate information. SSL certificate resources are used only with load balancing proxies such as target HTTPS proxy or target SSL proxy
* GCP HTTP(S) load balancing is implemented at the edge of Google's network in Google's points of presence (POP) around the world. User traffic directed to an HTTP(S) load balancer enters the POP closest to the user and is then load-balanced over Google's global network to the closest backend that has sufficient available capacity.

## 7. SSL proxy load balancing

* SSL proxy is a global load balancing service for encrypted, non-HTTP traffic. This load balancer terminates user SSL connections at the load balancing layer, then balances the connections across your instances using the SSL or TCP protocols.
* These instances can be in multiple regions, and the load balancer automatically directs traffic to the closest region that has capacity. SSL proxy load balancing supports both IPv4 and IPv6 addresses for client traffic and provides intelligent routing, certificate management, security patching, and SSL policies.
* Intelligent routing means that this load balancer can route requests to backend locations where there is capacity. From a certificate management perspective, you only need to update your customer-facing certificate in one place when you need to switch those certificates.
* Also, you can reduce the management overhead for your virtual machine instances by using self-signed certificates on your instances. In addition, if vulnerabilities arise in the SSL or TCP stack, GCP will apply patches at the load balancer automatically in order to keep your instances safe. 
* This network diagram illustrates SSL proxy load balancing. In this example, traffic from users in Iowa and Boston is terminated at the global load balancing layer. From there, a separate connection established to the closest backend instance. In other words, the user in Boston would reach the US East region, and the user in Iowa would reach the US Central region, if there's enough capacity. Now, the traffic between the proxy and the backend can use SSL or TCP. I recommend using SSL.

## 8. TCP proxy load balancing

* TCP proxy is a global load balancing service for unencrypted non-HTTP traffic. This load balancer terminates your customers TCP sessions at the load balancing layer, then forwards the traffic to your virtual machine instances using TCP or SSO.
* These instances can be in multiple regions and the load balancer automatically directs traffic to the closest region that has capacity. TCP proxy load balancing supports both IPv4 and IPv6 addresses for Client Traffic.
* Similar to SSL proxy load balancer, the TCP proxy load balancer provides intelligent routing and security patching.
* This network diagram illustrates TCP proxy load balancing. In this example, traffic from users in Iowa and Boston is terminated at the Global Load Balancing layer. From there, a separate connection is established to the closest backend instance.
* As in the SSL proxy load balancing example, the users in Boston would reach the US East region and the user in Iowa which reach the US central region, if there's enough capacity. Now the traffic between the proxy and the backends can use SSL or TCP and I also recommend using SSL here.

## 9. Network load balancing

* Next let's talk about network load balancing which is a regional load balancing service. Network load balancing is a regional non proxied load balancing service. In other words, all traffic is passed through the load balancer instead of being proxied and traffic can only be balanced between virtual machine instances that are in the same region unlike a global load balancer.
* This load balancing service uses forwarding rules to balance the load on your systems based on incoming IP protocol data such as address, port, and protocol type. You can use it to load balance UDP traffic and to load balance TCP NSSL traffic on ports that are not supported by the TCP proxy and SSL proxy load balancers.
* The back ends of a network load balancer can be a template-based instance group or target pooled resource. But what is the target pool resource? A target pool resource defines a group of instances that receive incoming traffic from forwarding rules.
* When a forwarding rule direct traffic to a target pool, the load balancer picks an instance from these target pools based on hash of the source IP and port, and the destination IP and port. These target pools can only be used with forwarding rules that handled TCP and UDP traffic.
* Now each project can have up to 50 target pools and each target pool can have only one health check. Also, all the instances of a target pool must be in the same region which is the same limitation as for the network load balancer.

## 10. Internal load balancing

* Next, let's talk about internal load balancing. Internal load balancing is a regional, private load balancing service for TCP and UDP based traffic. In other words, this load balancer enables you to run and scale your services behind a private load balancing IP address. This means that it is only accessible through the internal IP address of virtual machine instances that are in the same region.
* Therefore, use internal load balancing to configure an internal load balancing IP address, to act as the front end to your private backend instances. Because you don't need a public IP address for your load balanced service, your internal client requests to stay internal to your VPC network and the region.
* This often results in lower latency, because all your load balanced traffic will stay within Google's network, making your configuration much simpler. Let's talk more about the benefit of using a software-defined internal load balancing service.
* GCP internal load balancing is not based on a device or a virtual machine instance. Instead, it is a software-defined, fully distributed load balancing solution. In the traditional proxy model of internal load balancing as shown on the left, you configure an internal IP address on a load balancing device or instances, and your client instance connects to this IP address.
* Traffic coming to the IP address is terminated at the load balancer, and the load balancer selects a backend to establish a new connection to. Essentially, there are two connections. One between the client and the load balancer, and the one between the load balancer and the backend.
* GCP internal load balancing distributes client instance requests to the backend using a different approach, as shown on the right. It uses lightweight load balancing built on top of Andromeda, Google's network virtualization stack, to provide software-defined load balancing that directly delivers the traffic from the client instance to a backend instance.
* Now, internal load balancing enables you to support use-cases such as the traditional treaty or web service. In this example, the web tier uses an external HTTPS load balancer, that provides a single global IP address for users in San Francisco, Iowa and Singapore, and so on.
* The backends of this load balancer are located in the US-Central1 and Asia-East-1 region, because this is a global load balancer. These backends then access an internal load balancer in each region as the application or internal tier. The backends of this internal tier are located in US-Central1-A, US-Central1-B, and Asia-East1-B. 
* The last tier is the database tier in each of these zones. The benefit of this three-tier approach is that neither the database tier nor the application tier is exposed externally. The simplified security and network pricing. 
* Google Cloud offers Internal Load Balancing for your TCP/UDP-based traffic. Internal Load Balancing enables you to run and scale your services behind a private load balancing IP address that is accessible only to your internal virtual machine instances.

## 11. Choosing a load balancer

* Now, that we have discussed all the different load balancing services within GCP, let me help you determine which load balancer best meets your need. 
* One differentiator between the different GCP load balancers is the support for IPv6 clients. Only the HTTPS, SSL proxy, and TCP proxy load balancing services support IPV6 clients. IPv6 termination for these load balancers enables you to handle IPv6 requests from your users and proxy them over IPv4 to your backend. For example, in this diagram, there is a website,
* www.example[dot]com, that is translated by Cloud DNS to both an IPv4 and IPv6 address. This allows a desktop user in New York and a mobile user in Iowa to access the load balancer through the IPv4 and IPv6 addresses respectively.
* But how does the traffic get to the backends and their IPv4 addresses? Well, the load balancer acts as a reverse proxy, terminates the IPv6 client connection and places the request into an IPv4 connection to a backend. On the reverse path, the load balancer receives the IPv4 response from the backend and places it into the IPv6 connection back to the original client. In other words, configuring IPv6 termination for your load balancers, lets your backend instances appear as IPv6 applications to your IPv6 clients.
* Now, in order to decide which load balancer best suits your implementation of GCP, consider the following aspects of Cloud load balancing. Global versus regional load balancing, external versus internal load balancing, and the traffic type.
* If you need an external load balancing service, start on the top left of this flowchart. First, choose the type of traffic that your load balancer must handle. If that is HTTP or HTTPS traffic, I recommend using the HTTPS load balancing service as a layer seven load balancer. Otherwise, use the TCP and UDP traffic paths of this flowchart to determine whether the SSL proxy, TCP proxy, or network load balancing service meets your needs.
* If you need an internal load balancing service, you have the internal load balancing service available and it supports both TCP and UDP traffic. As I mentioned at the beginning of this module, there's actually another internal load balancer for HTTPS traffic but it's in beta as of this recording.
* The sixth load balancer is for HTTP or HTTPS traffic and it's regional meaning for IPv4 clients. If you prefer a table over a flowchart, I recommend this summary table. This table helps you identify the right load balancer based on the traffic type, the distribution of your backend global or regional, and the type of IP addresses of your backend external or internal. This table also lists the available ports for load balancing and highlights that only the Global Load Balancers support both IPv4 and IPV6 clients.

## QuizNotes

* Which of the following is not a GCP load balancing service?
	* Hardware-defined load balancing
		* Cloud Load Balancing is a fully distributed, software-defined, managed service for all your traffic. It is not an instance or device based solution, so you won’t be locked into physical load balancing infrastructure.
* Which three GCP load balancing services support IPv6 clients?
	* HTTP(S) Load Balancing
	* TCP Proxy Load Balancing
	* SSL Proxy Load Balancing
* Which of the following are applicable autoscaling policies for managed instance groups?
	* Monitoring metrics
	* Queue-based workload
	* CPU Utilization
	* Load balancing capacity

## Resources

[Autoscaling groups of instances](https://cloud.google.com/compute/docs/autoscaler/)

[QUIC, a multiplexed stream transport over UDP](https://www.chromium.org/quic)

[SSL Proxy Load Balancing overview](https://cloud.google.com/load-balancing/docs/ssl/#overview)

[TCP Proxy Load Balancing overview](https://cloud.google.com/load-balancing/docs/tcp/#overview)

[Andromeda](https://cloudplatform.googleblog.com/2014/04/enter-andromeda-zone-google-cloud-platforms-latest-networking-stack.html)