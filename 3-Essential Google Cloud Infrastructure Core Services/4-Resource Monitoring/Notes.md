## 1. Module Overview

* In this module, we're going to explore the Stackdriver monitoring, logging, error reporting, tracing, and debugging services. You will have the opportunity to apply these services in the two labs of this module. Let me start by giving you a high-level overview of Stackdriver and its features.

## 2. Stackdriver Overview

* Stackdriver dynamically discovers cloud resources in application services based on deep integration with Google Cloud Platform and Amazon Web Services. Because of its smart defaults, you can have core visibility into your cloud platform in minutes. This provides you with access to powerful data and analytics tools. Plus collaboration with many different third-party software providers.
* As I mentioned earlier, Stackdriver has services for monitoring, logging, error reporting, fault tracing, and debugging. You only pay for what you use and there are free usage allotments so that you can get started with no upfront fees or commitments.
* Now, in most other environments these services are handled by completely different packages or by a loosely integrated collection of software. When you see these functions working together in a single comprehensive and integrated service, you'll realize how important that is to creating reliable, stable, and maintainable applications.
* Stackdriver also supports a rich and growing ecosystem of technology partners as shown on this slide. This helps expand the IT ops, security, and compliance capabilities available to GCP customers.

## 3. Monitoring

* Now that you understand Stackdriver from a high-level perspective, let's look at Stackdriver monitoring. Monitoring is important to Google, because it is at the base of Site Reliability Engineering or SRE.
* SRE is a discipline that applies aspects of software engineering to operations whose goals are to create ultra scalable and highly reliable software systems. This discipline has enabled Google to build, deploy, monitor, and maintain some of the largest software systems in the world. If you want to learn more about SRE, I recommend exploring the free book written by members of Google's SRE team.
* Stackdriver dynamically configures monitoring after resources are deployed, and has intelligent defaults that allow you to easily create charts for basic monitoring activities. This allows you to monitor your platform system and application metrics by ingesting data such as metrics, events, and metadata.
* You can then generate insights from this data through dashboards, charts, and alerts. For example, you can configure and measure uptime and health checks, it'll send alerts via e-mail.
* A workspace is the root entity that holds monitoring and configuration information in Stackdriver monitoring. Each workspace can have between 100 monitored projects including one or more GCP projects and any number of AWS accounts.
* You can have as many workspaces as you want, but GCP projects and AWS accounts can be monitored by more than one workspace. A workspace contains the custom dashboards, alerting policies, uptime checks, notification channels, and group definitions that you use with your monitored projects.
* A workspace can access metric data from its monitored projects. But the metric data and log entries remain in the individual projects. The first monitor GCP project in a workspace is called the hosting project. 
* It must be specified when you create the workspace. The name of that project becomes a name of your workspace. To access an AWS account, you must configure a project in GCP to hold the AWS connector. Because workspaces can monitor all of your GCP projects in a single place, a workspace is a single pane of glass through which you can view resources from multiple GCP projects and AWS accounts.
* All Stackdriver users who have access to that workspace have access to all data by default. This means that a Stackdriver role assigned to one person on one project applies equally to all projects monitored by that workspace. In order to give people different roles per project, and to control visibility to data, consider placing the monitoring of those projects in separate workspaces.
* Stackdriver monitoring allows you to create custom dashboards that contain charts of the metrics that you want to monitor. For example, you can create charts that display your instances CPU utilization. The packets are bytes sent, and received by those instances.
* The packets are bytes dropped by the firewall of those instances. In other words, charts provide visibility into the utilization and network traffic of your VM instances as shown on this slide. These charts can be customized with filters to remove noise, groups to reduce the number of time series, and aggregates to group multiple time series together.
* Now, although charts are extremely useful, they can only provide insight when someone is looking at them. Well, what if your server goes down in the middle of the night or over the weekend. Do you expect someone to always look at dashboards to determine whether your servers are available or have enough capacity or bandwidth.
* If not, you want to create alerting policies then notify you when specific conditions are met. For example, as shown on this slide, you can create an alerting policy when the network egress of your VM instance goes above a certain threshold for a specific timeframe.
* When this condition is met, you or someone else can be automatically notified through e-mail, SMS, or other channels in order to troubleshoot this issue. You can also create an alerting policy that monitors your Stackdriver usage, and alerts you when you approach the threshold for billing.
* I recommend alerting on symptoms and not necessarily causes. For example, you want to monitor failing queries of a database and then identify whether the database is down. Next, make sure that you're using multiple notification channels. Like e-mail and SMS.
* This helps avoid a single point of failure in your alerting strategy. I also recommend customizing your alerts to the audiences need by describing what actions need to be taken or what resources need to be examined.
* Finally, avoid noise, because this will cause alerts to be dismissed overtime. Specifically, adjust monitoring alerts so that they are actionable, and don't just set up alerts on everything possible.
* Uptime checks can be configured to test the availability of your public services from locations around the world. As you can see on this slide. The type of uptime check can be set to HTTP, HTTPS or TCP. The resource to be checked can be an app engine application, a computer engine instance, a URL of a host, or an AWS instance or Load Balancer.
* For each uptime check, you can create an alerting policy and view the latency of each global location. Here is an example of an HTTP uptime check. The resources checked every minute with a 10 second timeout. Uptime checks that do not get a response within this timeout period are considered failures. So far there is a 100 percent uptime with no outages.
* Stackdriver monitoring can access some metrics without the monitoring agent. Including CPU utilization, some disk traffic metrics, network traffic, and uptime information. However, to access additional system resources and application services, you should install the monitoring agent.
* The monitoring agent is supported for Compute Engine and EC2 instances. The monitoring agent can be installed with these two simple commands. Which you could include in your startup script. This assumes that you have a VM instance running Linux that is being monitored by a workspace and that your instance has the proper credentials for the agent.
* If the standard metrics provided by Stackdriver monitoring do not fit your needs, you can create custom metrics. For example, imagine a game server that has a capacity of 50 users what metric indicator might you use to trigger scaling events. From an infrastructure perspective, you might consider using CPU load, or perhaps network traffic load, as values that are somewhat correlated with the number of users. But with a custom metric, you could actually pass the current number of users directly from your application into Stackdriver.

## 4. Logging

* Monitoring is the basis of Stackdriver. But the service also provides logging, error reporting, tracing, and debugging. Let's learn about logging. Stackdriver logging allows you to store, search, analyze, monitor, and alert on logged data and events from GCP and AWS.
* It is a fully managed service that performs at scale, and can ingest application and system log data from thousands of VMs. Logging includes storage for logs, a user-interface called the logs viewer, and an API to manage logs programmatically. The service lets you read and write log entries, search and filter your logs, and create log-based metrics. Logs are only retained for 30 days, but you can export your logs to Cloud Storage buckets, BigQuery datasets, and Cloud Pub/Sub topics.
* Exporting logs to Cloud Storage makes sense for storing logs for more than 30 days. But why would you export to BigQuery or Cloud Pub/Sub? Exploiting logs to BigQuery allows you to analyze logs and even visualize them in Data Studio.
* BigQuery runs extremely fast SQL queries on gigabytes to petabytes of data. This allows you to analyze logs such as your network traffic so that you can better understand traffic growth to forecast capacity, network usage to optimize network traffic expenses, or network forensics to analyze incidence.
* I queried my logs to identify the top IP addresses that have exchange traffic with my web server. Depending on where these IP addresses are and who they belong to, I could relocate part of my infrastructure to save on networking costs, or deny some of these IP addresses if I don't want them to access my web server. If you want to visualize your logs, I recommend connecting your BigQuery tables to Data Studio.
* Data Studio transforms your raw data into the metrics and dimensions that you can use to create easy to understand reports and dashboards. I mentioned that you can also export logs to Cloud Pub/Sub. This enables you to stream logs to applications or endpoints.
* Similar to Stackdriver monitoring agent, it's a best practice to install the logging agent on all of your VM instances. The logging agent can be installed with these two simple commands, which you could include in your startup script. This agent is supported for Compute Engine and EC2 instances.

## 5. Error Reporting

* Let's learn about another feature of Stackdriver, Error Reporting. Stackdriver Error Reporting counts, analyses and aggregates the errors in your running Cloud services.
* A centralized Error Management interface displays the results with sorting and filtering capabilities and you can even set up real-time notifications when new errors are detected.
* As of this recording, Stackdriver Error reporting is generally available for the App Engine standard environment and is a better feature for App Engine flexible environment, Compute Engine and AWS EC2.
* In terms of programming languages, the exception stack trace parser is able to process Go, Java,.NET, Node.js, PHP, Python and Ruby.

## 6. Tracing

* Tracing is another Stackdriver feature integrated into GCP. Stackdriver Trace is a distributed tracing system that collects latency data from your applications and displays it in the GCP console.
* You can track how request propagate through your application and receive detailed, near real-time performance insights. Stackdriver Trace automatically analyzes all of your application's traces to generate in-depth latency reports that surface performance degradations and can capture traces from App Engine, HTTP load balancers, and applications instrumented with the Stackdriver Trace API.
* Managing the amount of time it takes for your application to handle incoming requests and perform operations is an important part of managing overall application performance. Stackdriver Trace is actually based on the tools used at Google to keep our services running at extreme scale.

## 7. Debugging

* Finally, let's cover the last Stackdriver feature of this module, which is the Debugger. Stackdriver Debugger is a feature of GCP that lets you inspect the state of a running application in real time, without stopping or slowing it.
* Specifically, the Debugger adds less than 10 milliseconds to the request latency when the application state is captured. In most cases, this is not noticeable by users. These features allow you to understand the behavior of your code in production and analyze it state to locate those hard to find bugs.
* With just a few mouse clicks, you can take a snapshot of your running application state or inject a new logging statement. Stackdriver Debugger supports multiple languages including; Java, Python, Go, Node.js and Ruby.

## QuizNotes

* Why is monitoring important to Google?
	* It is at the base of site reliability which incorporates aspects of software engineering and applies that to operations whose goals are to create ultra-scalable and highly reliable software systems.
* What is not a recommended best practice for alerts?
	* Report all noise to ensure all data points are presented.
* What is recommended best practice for alerts?
	* Use multiple notification channels so you avoid a single point of failure.
	* Customize your alerts to the audience need.
	* Configure alerting on symptoms and not necessarily causes.
* Select all valid targets for Cloud Monitoring uptime alert notifications.
	* webhook
	* SMS
	* Email
	* 3rd part service
* Which service requires a logging agent installed to collect and send logs to Cloud Operations?
	* Compute Engine
* Which service(s) are currently supported by Cloud Error Reporting?
	* Compute Engine
	* App Engine Flexible
	* Kubernetes
	* App Engine Standard
* What would not be considered a benefit of Cloud Operations?
	* Boosts all network performance
* What would be considered a benefit of Cloud Operations?
	* Faster problem resolution
	* Multi-cloud monitoring
	* Reduces monitoring overhead
* What is the foundational process at the base of Google's Site Reliability Engineering (SRE) ?
	* Monitoring
		* Before you can take any of the other actions, you must first be monitoring the system.
* What is the purpose of the Stackdriver Trace service?
	* Reporting on latency as part of managing performance.
		* Stackdriver Trace provides latency sampling and reporting for Google App Engine, Google HTTP(S) load balancers, and applications instrumented with the Stackdriver Trace SDKs. Reporting includes per-URL statistics and latency distributions.
* Stackdriver integrates several technologies, including monitoring, logging, error reporting, and debugging that are commonly implemented in other environments as separate solutions using separate products. What are key benefits of integration of these services?
	* Reduces overhead, reduces noise, streamlines use, and fixes problems faster
		* Stackdriver integration streamlines and unifies these traditionally independent services, making it much easier to establish procedures around them and to use them in continuous ways.

## Resources

[Stackdriver Pricing](https://cloud.google.com/stackdriver/pricing)

[Stackdriver Integrations](https://cloud.google.com/stackdriver/integrations)

[Google Books](https://landing.google.com/sre/books/)

[Google Cloud metrics](https://cloud.google.com/monitoring/api/metrics_gcp)

[Stackdriver Pricing Alert Usage](https://cloud.google.com/stackdriver/pricing#alert-usage)

[Creating custom metrics](https://cloud.google.com/monitoring/custom-metrics/creating-metrics#monitoring-create-metric-python)

## Course Overview

* I recommend enrolling in the Elastic Cloud Infrastructure: Scaling and Automation course, which enhances your study of architecting with Compute Engine. In that course, we start by going over the different options to interconnect networks to enable you to connect your infrastructure to GCP. Next, we’ll go over GCP’s load balancing and autoscaling services, which you will get to explore directly. Then, we’ll cover infrastructure automation services like Deployment Manager and Terraform, so that you can automate the deployment of GCP infrastructure services. Lastly, we’ll talk about other managed services that you might want to leverage in GCP. Here are the modules of the course:

	1. Interconnecting Networks
	2. Load Balancing and Autoscaling
	3. Infrastructure Automation
	4. Managed Services
