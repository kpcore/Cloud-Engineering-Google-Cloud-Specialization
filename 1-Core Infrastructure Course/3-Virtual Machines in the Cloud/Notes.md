## 1. Module introduction

* Compute Engine lets you run virtual machines on Google's global infrastructure.
* One of the nice things about virtual machines is that they have the power and generality of a full-fledged operating system in each.

## 3. Virtual Private Cloud (VPC) Network

* VPC networks connect your Google Cloud platform resources to each other and to the internet.
* You can segment your networks, use firewall rules to restrict access to instances, and create static routes to forward traffic to specific destinations.
* The Virtual Private Cloud networks that you define have global scope. They can have subnets in any GCP region worldwide and subnets can span the zones that make up a region.
* You can also have resources in different zones on the same subnet.
* You can dynamically increase the size of a subnet in a custom network by expanding the range of IP addresses allocated to it. Doing that doesn’t affect already configured VMs.
* VPC subnets can span the zones that make up a region. This is beneficial because your solutions can incorporate fault tolerance without complicating your network topology.

## Compute Engine

* no upfront investments.
* fast and to offer consistent performance.
* You can create a virtual machine instance by using the Google Cloud Platform console or the GCloud command line tool.
* It's advantageous to create virtual machines from a command line when you want their configurations to be scripted and repeatable. The gcloud command, provided by Google Cloud as part of the GCP SDK, can create virtual machines with parameters you specify.
* If your application needs high-performance scratch space, you can attach a local SSD, but be sure to store data of permanent value somewhere else because local SSDs content doesn't last past when the VM terminates. 
* A preemptible VM is different from an ordinary Compute Engine VM in only one respect. You've given compute engine permission to terminate it if it's resources are needed elsewhere.
* The per-hour price of preemptible VMs incorporates a substantial discount.
* These huge VMs are great for workloads like in-memory databases and CPU intensive analytics, but most GCP customers start off with scaling out not scaling up.
* Compute Engine has a feature called auto scaling that lets you add and take away VMs from your application based on load metrics. 
* The other part of making that work is balancing the incoming traffic across the VMs, and Google VPC supports several different kinds of load balancing.

## Important VPC capabilities

* VPCs have routing tables. These are used to forward traffic from one instance to another instance within the same network. Even across sub-networks and even between GCP zones without requiring an external IP address. 
* VPCs give you a global distributed firewall. You can control to restrict access to instances, both incoming and outgoing traffic. You can define firewall rules in terms of metadata tags on Compute Engine instances, which is really convenient.
* If you simply want to establish a peering relationship between two VPCs so that they can exchange traffic, that's what VPC Peering does.
* On the other hand, if you want to use the full power of IAM to control who and what in one project can interact with a VPC in another, that's what Shared VPC is for. 
* Cloud Load Balancing is a fully distributed, software-defined managed service for all your traffic. And because the load balancers don't run in VMs you have to manage, you don't have to worry about scaling or managing them.
* It provides cross-region load balancing, including automatic multi-region failover, which gently moves traffic in fractions if backends become unhealthy.
* Cloud Load Balancing reacts quickly to changes in users, traffic, backend health, network conditions, and other related conditions.
* internal load balancer. It accepts traffic on a GCP internal IP address and load balances it across Compute Engine VMs.
* DNS is what translates internet host names to addresses. And as you would imagine, Google has a highly developed DNS infrastructure. 
* Google has a global system of edge caches. You can use this system to accelerate content delivery in your application using Google Cloud CDN. 

## QuizNotes

* Google Cloud Load Balancing allows you to balance HTTP-based traffic across multiple Compute Engine regions. With global Cloud Load Balancing, your application presents a single front-end to the world.
* Google VPC networks and subnets, Networks are global; subnets are regional
* An application running in a Compute Engine virtual machine needs high-performance scratch space. Which type of storage meets this need
	* Local SSD
* be suitable for running in a Preemptible VM
	* A batch job that can be checkpointed and restarted
* How do Compute Engine customers choose between big VMs and many VMs?
	* Use big VMs for in-memory databases and CPU-intensive analytics; use many VMs for fault tolerance and elasticity
* How do VPC routers and firewalls work?
	* They are managed by Google as a built-in feature.
* A GCP customer wants to load-balance traffic among the back-end VMs that form part of a multi-tier application. Which load-balancing option should this customer choose?
	* The regional internal load balancer
* Dedicated Interconnect is a Service Level Agreement available.

## Resources

[Virtual Private Cloud documentation](https://cloud.google.com/vpc/docs/)

[VPC network overview](https://cloud.google.com/vpc/docs/vpc)

[Compute Engine documentation](https://www.coursera.org/learn/gcp-fundamentals/quiz/mB4ui/compute-engine)










