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

* 

## QuizNotes

* 

## Resources

[App Engine](https://cloud.google.com/appengine/)

[The App Engine Standard Environment](https://cloud.google.com/appengine/docs/standard/)

[App Engine Flexible Environment](https://cloud.google.com/appengine/docs/flexible/)

[Cloud Endpoints](https://cloud.google.com/endpoints/)

[What is Apigee Edge?](https://docs.apigee.com/api-platform/get-started/what-apigee-edge)
