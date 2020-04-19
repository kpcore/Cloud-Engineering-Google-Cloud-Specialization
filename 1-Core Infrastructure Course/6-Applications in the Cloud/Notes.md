## 1. Module introduction; introduction to App Engine

* PaaS. Recall that a PaaS is a platform as a service. The App Engine platform manages the hardware and networking infrastructure required to run your code. To deploy an application on App Engine, you just hand App Engine your code and the App Engine service takes care of the rest.
* App Engine provides you with a built-in services that many web applications need. NoSQL databases, in-memory caching, load balancing, health checks, logging and a way to authenticate users. You code your application to take advantage of these services and App Engine provides them. 
* App engine will scale your application automatically in response to the amount of traffic it receives. So you only pay for those resources you use. There are no servers for you to provision or maintain.
* That's why App Engine is especially suited for applications where the workload is highly variable or unpredictable like web applications and mobile backend. App Engine offers two environments: standard and flexible.
* App Engine will scale your application automatically in response to the amount of traffic it receives. That’s why App Engine is especially suited for applications where the workload is highly variable, like a web application.

## 2. Google App Engine Standard Environment

* Of the two App Engine Environments, Standard is the simpler. It offers a simpler deployment experience than the Flexible environment and fine-grained auto-scale.
* Like the Standard Environment, it also offers a free daily usage quota for the use of some services. What's distinctive about the Standard Environment though, is that low utilization applications might be able to run at no charge.
* Google provides App Engine software development kits in several languages, so that you can test your application locally before you upload it to the real App Engine service. The SDKs also provide simple commands for deployment. 
* App Engine's term for this kind of binary is the runtime. In App Engine Standard Environment, you use a runtime provided by Google. App Engine Standard Environment provides runtimes for specific versions of Java, Python, PHP and Go.  The runtimes also include libraries that support App Engine APIs.
* And for many applications, the Standard Environment runtimes and libraries may be all you need. If you want to code in another language, Standard Environment is not right for you. 
* The Standard Environment also enforces restrictions on your code by making it run in a so-called "Sandbox." That's a software construct that's independent of the hardware, operating system, or physical location of the server it runs on. 
* The Sandbox is one of the reasons why App Engine Standard Environment can scale and manage your application in a very fine-grained way. Like all Sandboxes, it imposes some constraints. 
* Also, all the requests your application receives has a 60-second timeout, and you can't install arbitrary third party software.
* Also, all the requests your application receives has a 60-second timeout, and you can't install arbitrary third party software. If these constraints don't work for you, that would be a reason to choose the Flexible Environment.
* You'll develop your application and run a test version of it locally using the App Engine SDK. Then when you're ready, you'll use the SDK to deploy it. 
* Each App Engine application runs in a GCP project. App Engine automatically provisions server instances and scales and load balances them. Meanwhile, your application can make calls to a variety of services using dedicated APIs. Here are a few examples: a NoSQL data store to make data persistent, caching of that data using Memcache, searching logging, user logging, and the ability to launch actions not triggered by direct user requests, like task queues and a task scheduler.

## 3. Google App Engine Flexible Environment

* App Engine flexible environment is for. Instead of the sandbox, App Engine flexible environment lets you specify the container your App Engine runs in. 
* They're health checked, healed as necessary, and you get to choose which geographical region they run in, and critical backward-compatible updates to their operating systems are automatically applied.
* App Engine flexible environment apps use standard run times, can access App Engine services such as data store, memcached, task queues, and so on.
* Standard environment starts up instances of your application faster, but that you get less access to the infrastructure in which your application runs. Flexible environment lets you SSH into the virtual machines on which your application runs. It lets you use local disk for scratch base, it lets you install third-party software, and it lets your application make calls to the network without going through App Engine. 
* Standard environment's billing can drop to zero for the completely idle application. Because we mentioned App Engine's use of Docker containers. 
* App Engine standard environment is for people who want the service to take maximum control of their application's deployment and scaling. Kubernetes Engine gives the application owner the full flexibility of Kubernetes. App Engine flexible edition is somewhere in between.
* Also, App Engine environment treats containers as a means to an end, but for Kubernetes Engine, containers are a fundamental organizing principle.
* App Engine Flexible Environment applications let their owners control the geographic region where they run.
* At the time of this writing, App Engine Standard Environment supports Java, Python, PHP, and Go, but in the Flexible Environment, you upload your own runtime to run code in a language of your choice.
* App Engine Flexible Environment lets you ssh into the virtual machines in which your application runs.

## 4. Google Cloud Endpoints and Apigee Edge

* A software services implementation can be complex and changeable. What if to use that service, other pieces of software had to know internal details about how they worked? That would be a mess. So instead application developers structure the software they write so that it presents a clean, well-defined interface that abstracts away needless details and then they document that interface. That's an API.
* The underlying implementation can change as long as the interface doesn't and other pieces of software that use the API don't have to know or care.
*  Sometimes you have to change an API, say to add or deprecate a feature. To make this kind of API change cleanly, developers version their APIs. Version two of an API might contain calls that version one does not. Programs that consume the API can specify the API version that they want to use in their calls.
* Supporting an API is a very important task and Google Cloud platform provides two API management tools. They approach related problems in a different way and each has a particular strength.
* Suppose you're developing a software service and one of GCP's backends. You'd like to make it easy to expose this API. You'd like to make sure it's only consumed by other developers whom you trust. You'd like an easy way to monitor and log its use. You'd like for the API to have a single coherent way for it to know which end user is making the call. That's when you use Cloud Endpoints. It implements these capabilities and more using an easy to deploy proxy in front of your software service, and it provides an API console to wrap up those capabilities in an easy-to-manage interface. 
* Cloud Endpoints supports applications running in GCP's compute platforms in your choice of languages and your choice of client technologies. 
* Apigee Edge is also a platform for developing and managing API proxies. It has a different orientation though. It has a focus on business problems like rate limiting, quotas, and analytics. Many users of Apigee Edge are providing a software service to other companies and those features come in handy. Because of the backend services for Apigee Edge need not be in GCP, engineers often use it when they are "taking apart" a legacy application.
* Instead of replacing a monolithic application in one risky move, they can instead use Apigee Edge to peel off its services one by one, standing up microservices to implement each in turn, until the legacy application can be finally retired.	

## QuizNotes

* Which statements are true about App Engine?
	* It is possible for an App Engine application's daily billing to drop to zero.
	* App Engine manages the hardware and networking infrastructure required to run your code. 
* Name 3 advantages of using the App Engine Flexible Environment over App Engine Standard. 
	* You can install third-party binaries
	* You can SSH in to your application
	* Your application can write to local disk
* Name 3 advantages of using the App Engine Standard Environment over App Engine Flexible.
	* Scaling is finer-grained
	* Billing can drop to zero if your application is idle
	* Google provides and maintains runtime binaries
* Apigee Edge: to do business analytics and billing on a customer-facing API. 
* Cloud Endpoint: support developers who are building services in GCP through API logging and monitoring. 
* Apigee Edge: gradually decompose a pre-existing monolithic application, not implemented in GCP, into microservices.

## Resources

[App Engine](https://cloud.google.com/appengine/)

[The App Engine Standard Environment](https://cloud.google.com/appengine/docs/standard/)

[App Engine Flexible Environment](https://cloud.google.com/appengine/docs/flexible/)

[Cloud Endpoints](https://cloud.google.com/endpoints/)

[What is Apigee Edge?](https://docs.apigee.com/api-platform/get-started/what-apigee-edge)
