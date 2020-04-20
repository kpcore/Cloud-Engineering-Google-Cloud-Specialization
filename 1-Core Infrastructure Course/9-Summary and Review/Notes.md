## 1. Summary and Review

* The continuum between managed infrastructure and dynamic infrastructure. GCP's Compute Services are arranged along this continuum, and you can choose where you want to be on it.
* Choose Compute Engine if you want to deploy your application in virtual machines that run on Google's infrastructure. 
* Choose Kubernetes Engine if you want instead to deploy your application in containers that run on Google's infrastructure. In a Kubernetes cluster you're defining control. 
* Choose App Engine instead if you just want to focus on your code, leaving most infrastructure and provisioning to Google. App Engine flexible environment lets you use any runtime you want, and gives you full control of the environment in which your application runs. App Engine standard environment lets you choose from a set of standard runtimes and offers finer-grained scaling and scaled to zero. 
* To completely relieve yourself from the chore of managing infrastructure, build or extend your application using Cloud Functions. You supply chunks of code for business logic, and your code get spun up on demand in response to events. 
* GCP offers a variety of ways to load balance inbound traffic. Use Global HTTP(S) load balancing to put your Web application behind a single anycast IP to the entire Internet. It load balances traffic among all your backend instances in regions around the world. And it's integrated with GCP's Content Delivery Network. 
* If your traffic isn't HTTP or HTTPS, you can use the global TCP or SSL Proxy for traffic on many ports. For other ports or for UDP traffic, use the regional load balancer. Finally, to load balance the internal tiers of a multi-tier application, use the internal load balancer.
* GCP also offers a variety of ways for you to interconnect your on-premises or other cloud networks with your Google VPC. It's simple to set up a VPN and you can use Cloud Router to make it dynamic. 
* You can also peer with Google, at its many worldwide points of presence either directly or through a carrier partner. 
* Or if you need a service level agreement and can adopt one of the required network typologies, use Dedicated Interconnect.
* Consider using Cloud Datastore if you need to store structured objects, or if you require support for transactions and SQL-like queries. 
* Consider using Cloud Bigtable if you need to store a large amount of single-keyed data, especially structured objects. 
* Consider using Cloud Storage if you need to store immutable binary objects. 
* Consider using Cloud SQL or Cloud Spanner if you need full SQL support for an online transaction processing system. Cloud SQL provides terabytes of capacity while Cloud Spanner provides petabytes and horizontal scalability. 
* Consider BigQuery if you need interactive querying in an online analytical processing system with petabytes of scale. I'd like to zoom into one of those services we just discussed, Cloud Storage and remind you of its four storage classes.
* Multi-regional and regional are the classes for warm and hot data. Use Multi-regional especially for content that's being served to a global Web audience. And use Regional for working storage for compute operations. 
* Nearline and Coldline are the classes for, as you'd guess, cooler data. Use Nearline for backups and for infrequently accessed content. And use Coldline for archiving and disaster recovery.

## QuizNotes

* Which compute service lets customers run virtual machines that run on Google's infrastructure?
	* Compute Engine
* Which compute service lets customers deploy their applications in containers that run in clusters on Google's infrastructure?
	* Kubbernetes Engine
* Which compute service lets customers focus on their applications, leaving most infrastructure and provisioning to Google, while still offering various choices of runtime?
	* App Engine
* Which compute service lets customers supply chunks of code, which get run on-demand in response to events, on infrastructure wholly managed by Google?
	* Cloud Function
* For what kind of traffic would the regional load balancer be the first choice?
	* UDP Traffic
	* TCP traffic on arbitrary port numbers
* Choose a simple way to let a VPN into your Google VPC continue to work in spite of routing changes,
	* Cloud Router
* Which of these storage needs is best addressed by Cloud Datastore?
	* Structured objects, with transactions and SQL-like queries
* Which of these storage needs is best addressed by Cloud Spanner?
	* A relational database with SQL queries and horizontal scalability
* Which of these storage needs is best addressed by Cloud Bigtable?
	* Structured objects, with lookups based on a single key
* Which of these storage needs is best addressed by Cloud Storage?
	* Immutable binary object