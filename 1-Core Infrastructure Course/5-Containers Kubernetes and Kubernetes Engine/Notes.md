## 1. Containers, Kubernetes, and Kubernetes Engine

* Kubernetes Engine. It's like an Infrastructure as a Service offering in that it saves you infrastructure chores. It's also like a platform as a service offering. infrastructure as a service offering let you share compute resources with others by virtualizing the hardware. Each Virtual Machine has its own instance of an operating system, your choice, and you can build and run applications on it with access to memory, file systems, networking interfaces, and the other attributes that physical computers also have. But flexibility comes with a cost. In an environment like this, the smallest unit of compute is a Virtual Machine together with its application.
* From the perspective of someone deploying on App Engine, it feels very different. Instead of getting a blank Virtual Machine, you get access to a family of services that applications need. So all you do is write your code and self-contained workloads that use these services and include any dependent libraries. As demand for your application increases, the platform scales your applications seamlessly and independently by workload and infrastructure. This scales rapidly, but you give up control of the underlying server architecture. 
* The idea of a Container is to give you the independent scalability of workloads like you get in a PaaS environment, and an abstraction layer of the operating system and hardware, like you get in an Infrastructure as a Service environment. 
* All you need on each host is an operating system that supports Containers and a Container run-time. In essence, you're visualizing the operating system rather than the hardware. The environment scales like PaaS but gives you nearly the same flexibility as Infrastructure as a Service. 
* The container abstraction makes your code very portable. You can treat the operating system and hardware as a black box. So you can move your code from development, to staging, to production, or from your laptop to the Cloud without changing or rebuilding anything.
* You'll likely want to build your applications using lots of Containers, each performing their own function, say using the micro-services pattern. The units of code running in these Containers can communicate with each other over a network fabric. If you build this way, you can make applications modular. They deploy it easily and scale independently across a group of hosts. The host can scale up and down, and start and stop Containers as demand for your application changes, or even as hosts fail and are replaced. A tool that helps you do this well is Kubernetes. Kubernetes makes it easy to orchestrate many Containers on many hosts. Scale them, roll out new versions of them, and even roll back to the old version if things go wrong.
* Containers start much faster than virtual machines and use fewer resources, because each container does not have its own instance of the operating system.
* Containers need a lightweight container runtime, which does the plumbing jobs needed to allow that container to launch and run. The container runtime also determines the image format.
* Containers are loosely coupled to their environments. 
	* Deploying a containerized application consumes less resources and is less error-prone than deploying an application in virtual machines.
	* Containers abstract away unimportant details of their environments.
	* Containers are easy to move around.

## 2. Introduction to Kubernetes and GKE

* Kubernetes is an open-source orchestrator for containers so you can better manage and scale your applications. Kubernetes offers an API that lets people, that is authorized people, not just anybody, control its operation through several utilities.
* Kubernetes lets you deploy containers on a set of nodes called a cluster. What's a cluster? It's a set of master components that control the system as a whole and a set of nodes that run containers.
* Kubernetes lets you deploy containers on a set of nodes called a cluster. What's a cluster? It's a set of master components that control the system as a whole and a set of nodes that run containers.
* To use Kubernetes, you can describe a set of applications and how they should interact with each other, and Kubernetes figures out how to make that happen. Kubernetes makes it easy to run containerized applications
* Google Cloud provides Kubernetes Engine, which is Kubernetes as a managed service in the cloud. You can create a Kubernetes cluster with Kubernetes Engine using the GCP console or the g-cloud command that's provided by the Cloud SDK.
* GKE clusters can be customized, and they support different machine types, numbers of nodes and network settings. 
* Whenever Kubernetes deploys a container or a set of related containers, it does so inside an abstraction called a pod. A pod is the smallest deployable unit in Kubernetes. Think of a pod as if it were a running process on your cluster. It could be one component of your application or even an entire application.
* It's common to have only one container per pod. But if you have multiple containers with a hard dependency, you can package them into a single pod. They'll automatically share networking and they can have disk storage volumes in common.
* Each pod in Kubernetes gets a unique IP address and set of ports for your containers. Because containers inside a pod can communicate with each other using the localhost network interface, they don't know or care which nodes they're deployed on. 
* A deployment represents a group of replicas of the same pod. It keeps your pods running even if a node on which some of them run on fails. You can use a deployment to contain a component of your application or even the entire application.
* By default, pods in a deployment or only accessible inside your cluster. To make the pods in your deployment publicly available, you can connect a load balancer to it by running the kubectl expose command.
* Kubernetes then creates a service with a fixed IP address for your pods. A service is the fundamental way Kubernetes represents load balancing. To be specific, you requested Kubernetes to attach an external load balancer with a public IP address to your service so that others outside the cluster can access it. 
* In GKE, this kind of load balancer is created as a network load balancer. This is one of the managed load balancing services that Compute Engine makes available to virtual machines. GKE makes it easy to use it with containers. Any client that hits that IP address will be routed to a pod behind the service.
* A service groups a set of pods together and provides a stable endpoint for them.
* As deployments create and destroy pods, pods get their own IP addresses, but those addresses don't remain stable over time. Services provide that stable endpoint you need.
* To scale a deployment, run the kubectl scale command. Now our deployment has 3 nginx web servers, but they're all behind the service and they're all available through one fixed IP address. You could also use auto scaling with all kinds of useful parameters. 
* When you choose a rolling update for a deployment and then give it a new version of the software that it manages, Kubernetes will create pods of the new version one-by-one, waiting for each new version pod to become available before destroying one of the old version pods. Rolling updates are a quick way to push out a new version of your application while still sparing your users from experiencing downtime.

## 3. Introduction to Hybrid and Multi-Cloud Computing (Anthos)

* Most enterprise scale applications are designed as distributed systems. Spreading the computing workload required to provide services over two or more network servers. Over the past few years, containers have become a popular way to break these workloads down into microservices, so they can be more easily maintained and expanded. 
* Traditionally, these Enterprise systems and their workloads, containerized or not, have been housed on-premises, which means they're housed on a set of high-capacity servers running somewhere within the company's network or within a company own data center. When an application's computing needs begin to outstrip its available computing resources, a company using on-premises systems would need to procure more powerful servers.
* What if your company wants to begin to relocate some workloads away from on-premises to the Cloud to take advantage of lower cost and higher availability, but is unwilling or unable to move the enterprise application from the on-premises network? 
* What if you want to use specialized products and services that only available in the Cloud? This is where a modern hybrid or multi-cloud architecture can help. To summarize, it allows you to keep parts of your systems infrastructure on-premises while moving other parts to the Cloud, creating an environment that is uniquely suited to your company's needs.
* Take advantage of the flexibility, scalability, and lower computing costs offered by cloud services for running the workloads you decide to migrate. Add specialized services such as machine learning, content caching, data analysis, long-term storage, and IoT to your computing resources tool kit. 
* modern hybrid and multi-cloud distributed systems and service management called Anthos. Anthos is a hybrid and multi-cloud solution powered by the latest innovations in distributed systems, and service management software from Google. The Anthos framework rests on Kubernetes and Google Kubernetes engine deployed on-prem.
* Which provides the foundation for an architecture that is fully integrated with centralized management through a central control plane that supports policy based application lifecycle delivery across hybrid and multi-cloud environments. Anthos also provides a rich set of tools for monitoring and maintaining the consistency of your applications across all of your network, whether on-premises, in the Cloud, or in multiple clouds.
* Google Kubernetes Engine on the Cloud site of your hybrid network. Google Kubernetes Engine is a managed production-ready environment for deploying containerized applications. Operates seamlessly with high availability and an SLA. Runs certified Kubernetes ensuring portability across clouds and on-premises. Includes auto-node repair, and auto-upgrade, and auto-scaling. Uses regional clusters for high availability with multiple masters. Node storage replication across multiple zones.
* Provides access to container services on Google Cloud platform, such as Cloud build, container registry, audit logging, and more. It also integrates with Istio, Knative and Marketplace Solutions. Ensures a consistent Kubernetes version and experience across Cloud and on-premises environments.
* Enterprise applications may use hundreds of microservices to handle computing workloads. Keeping track of all of these services and monitoring their health can quickly become a challenge. Anthos, an Istio Open Source service mesh take all of these guesswork out of managing and securing your microservices. These service mesh layers communicate across the hybrid network using Cloud interconnect, as shown to sync and pass their data.
* Stackdriver is the built-in logging and monitoring solution for Google Cloud. Stackdriver offers a fully managed logging, metrics collection, monitoring dashboarding, and alerting solution that watches all sides of your hybrid on multi-cloud network. Stackdriver is the ideal solution for customers wanting a single easy to configure powerful cloud-based observability solution, that also gives you a single pane of glass dashboard to monitor all of your environments. 
* Anthos Configuration Management provides a single source of truth for your clusters configuration. That source of truth is kept in the policy repository, which is actually a git repository. The Anthos Configuration Management agents use the policy repository to enforce configurations locally in each environment, managing the complexity of owning clusters across environments. Anthos Configuration Management also provides administrators and developers the ability to deploy code changes with a single repository commit. And the option to implement configuration inheritance, by using namespaces.

## QuizNotes

* In Kubernetes, a group of one or more containers is called a pod. Containers in a pod are deployed together. They are started, stopped, and replicated as a group. The simplest workload that Kubernetes can deploy is a pod that consists only of a single container.
* A Kubernetes cluster is a group of machines where Kubernetes can schedule containers in pods. The machines in the cluster are called “nodes.”
* The Kubernetes Engine team periodically performs automatic upgrades of your cluster master to newer stable versions of Kubernetes, and you can enable automatic node upgrades too.
* the resources used to build Kubernetes Engine clusters come from Compute Engine, Kubernetes Engine gets to take advantage of Compute Engine’s and Google VPC’s capabilities.
* Identify two reasons for deploying applications using containers.
	* Consistency across development, testing, production environments
	* Simpler to migrate workloads
* Kubernetes allows you to manage container clusters in multiple cloud providers.
* Google Cloud Platform provides a secure, high-speed container image storage service for use with Kubernetes Engine.
* In Kubernetes, what does "pod" refer to?
	* A group of containers that work together
*  Kubernetes Engine workloads run in clusters built from Compute Engine virtual machines
* Does Google Cloud Platform offer its own tool for building containers (other than the ordinary docker command)?
	* Yes; the GCP-provided tool is an option, but customers may choose not use it.

## Resources

[Google Kubernetes Engine documentation](https://cloud.google.com/kubernetes-engine/docs/)

[Kubernetes Website](https://kubernetes.io/)

