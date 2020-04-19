## 1. Development in the cloud

* Popular tools for development, deployment and monitoring just work in GCP. You also have options for tools that are tightly integrated with GCP and in this module
* Cloud Source Repositories is. It provides Git version control to support your team's development of any application or service, including those that run on App Engine, Compute Engine, and Kubernetes Engine. 
* With Cloud Source Repositories, you can have any number of private Git repositories, which allows you to organize the code associated with your cloud project in whatever way works best for you. Cloud Source Repositories also contains a source viewer so that you can browse and view repository files from within the GCP console.
* Cloud Source Repositories is a managed service. It provisions and maintains the hosting infrastructure for you.
* Cloud Source Repositories manages the hosting infrastructure for you.
* Cloud Source Repositories integrates with Google Cloud IAM.
* Many applications contain event-driven parts. For example, maybe you have an application that lets users upload images. Whenever that happens, you need to process that image in various ways: convert it to a standard image format, thumbnail into various sizes, and store each in a repository.  
* You just pay whenever your functions run, in 100 millisecond intervals. Cloud Functions can trigger on events in Cloud Storage, Cloud Pub/Sub, or in HTTP call. You choose which events you care about. For each event type, you tell Cloud Functions you're interested in it. These declarations are called triggers. Then you attach JavaScript functions to your triggers. From now on, your functions will respond whenever the events happen.
* Some applications, especially those that have microservices architecture, can be implemented entirely in Cloud Functions. People also use Cloud Functions to enhance existing applications without having to worry about scaling.
* Your code executes whenever an event triggers it, no matter whether it happens rarely or many times per second. That means you don't have to provision compute resources to handle these operations.
* What is the advantage of putting event-driven components of your application into Cloud Functions?
	* Cloud Functions handles scaling these components seamlessly.

## 2. Deployment: Infrastructure as code

* Setting up your environment in GCP can entail many steps: setting up compute network and storage resources, and keeping track of their configurations. You can do it all by hand if you want to, taking an imperative approach.
* It's more efficient to use a template. That means a specification of what the environment should look like. It's declarative rather than imperative.
* GCP provides Deployment Manager to let you do just that. It's an Infrastructure Management Service that automates the creation and management of your Google Cloud Platform resources for you. 
* you create a template file using either the YAML markup language or Python that describes what you want the components of your environment to look like.  Then, you give the template to Deployment Manager, which figures out and does the actions needed to create the environment your template describes.
* If you need to change your environment, edit your template and then tell Deployment Manager to update the environment to match the change.
* you can store and version control your Deployment Manager templates in Cloud Source repositories.

## 3. Monitoring: Proactive instrumentation

* You can't run an application stably without monitoring. Monitoring lets you figure out whether the changes you made were good or bad. It lets you respond with information rather than with panic, when one of your end users complains that your application is down.
* Stackdriver is GCP's tool for monitoring, logging and diagnostics. Stackdriver gives you access to many different kinds of signals from your infrastructure platforms, virtual machines, containers, middleware and application tier, logs, metrics and traces. 
* It gives you insight into your application's health, performance and availability. So if issues occur, you can fix them faster. Here are the core components of Stackdriver: Monitoring, Logging, Trace, Error Reporting and Debugging. Stackdriver Monitoring checks the endpoints of web applications and other Internet accessible services running on your cloud environment. 
* You can configure uptime checks associated with URLs, groups or resources such as Instances and load balancers. You can set up alerts on interesting criteria, like when health check results or uptimes fall into levels that need action. 
* You can use Monitoring with a lot of popular notification tools. And you can create dashboards to help you visualize the state of your application. 
* Stackdriver Logging lets you view logs from your applications and filter and search on them. Logging also lets you define metrics, based on log contents that are incorporated into dashboards and alerts. You can also export logs to BigQuery, Cloud Storage and Cloud PubSub. 
* Stackdriver Error Reporting tracks and groups the errors in your cloud applications. And it notifies you when new errors are detected.
* Stackdriver Trace, you can sample the latency of app engine applications and report Per-URL statistics.
* A painful way to debug an existing application is to go back into it and add lots of logging statements. Stackdriver Debugger offers a different way. It connects your applications production data to your source code. So you can inspect the state of your application at any code location in production. That means you can view the application stage without adding logging statements. Stackdriver Debugger works best when your application source code is available, such as in Cloud Source repositories. 


## QuizNotes

* Why might a GCP customer choose to use Cloud Source Repositories?
	* They don't want to host their own git instance, and they want to integrate with IAM permissions.
* Why might a GCP customer choose to use Cloud Functions?
	* Their application contains event-driven code that they don't want to have to provision compute resources for.
* Why might a GCP customer choose to use Deployment Manager?
	* Deployment Manager is an infrastructure management system for GCP resources.
* You want to define alerts on your GCP resources, such as when health checks fail. Which is the best GCP product to use?
	* Stackdriver Monitoring
* Which statements are true about Stackdriver Logging?
	* Stackdriver Logging lets you view logs from your applications, and filter and search on them.
	* Stackdriver Logging lets you define metrics based on your logs.
	
## Resources

[Cloud Source Repositories](https://cloud.google.com/source-repositories/)

[Cloud Deployment Manager](https://cloud.google.com/deployment-manager/)

[Stackdriver](https://cloud.google.com/stackdriver/)
