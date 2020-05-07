## 1. Module Overview

* In the last module we discussed how to automate the creation of infrastructure. As an alternative to infrastructure automation you can eliminate the need to create infrastructure by leveraging a managed service. 
* Managed services are partial or complete solutions offered as a service. They exist on a continuum between platform as a service and software as a service depending on how much of the internal methods and controls are exposed.
* Using a managed service allows you to outsource a lot of the administrative and maintenance overhead to Google if your application requirements fits within the service offering. In this module, we give you an overview of BigQuery, Cloud Dataflow, Cloud Dataprep by Trifecta and Cloud Dataproc.
* Now, all of these services are for data analytics purposes. And since that's not the focus of this course series, there won't be any labs on this module. Instead we'll have a quick demo to illustrate how easy it is to use managed services.

## 2. BigQuery

* BigQuery is GCP's serverless, highly scalable, and cost effective Cloud data warehouse. It's a petabyte scale data warehouse that allows for super-fast queries using the processing power of Google's infrastructure. Because there's no infrastructure for you to manage, you can focus on uncovering meaningful insights using familiar SQL, without the need for the database administrator. 
* BigQuery is used by all types of organizations, and there's a free usage tier to help you get started. You can access BigQuery by using the GCP console, by using the command line tool, or by making calls to the BigQuery REST API, using the variety of client libraries such as Java,.NET or Python.
* There are also several third-party tools that you can use to interact with BigQuery, such as visualizing the data, or loading the data. Here's an example of a query on the table with over 100 billion rows. This query processes over 4.1 terabyte, but takes less than a minute to execute. The same query would take hours if not days through a serial execution.

## 3. Cloud Dataflow

* Let's learn a little bit about Cloud Dataflow. Cloud Dataflow is a managed service for executing a wide variety of data processing patterns. It is essentially a fully managed service for transforming and enriching data in stream and batch modes with equal reliability and expressiveness.
* With Cloud Dataflow, a lot of the complexity of infrastructure setup and maintenance is handled for you. It's build on Google Cloud Infrastructure and auto-scaled to meet the demands of your data pipeline, allowing you to intelligently scale to millions of queries per second.
* Cloud Dataflow supports fast, simplified pipeline development via expressive SQL, Java, and Python APIs in the Apache Beam SDK which provides a rich set of windowing, and session analysis primitives as well as an ecosystem of source and sync connectors.
* Cloud Dataflow, is also tightly coupled with other GCP services like Stackdriver, so you can set a priority alerts and notifications to monitor your pipeline and the quality of data coming in and out. 
* This diagram shows some example use cases of Cloud Dataflow. As I just mentioned, Cloud Dataflow processes stream and batch data. This data could come from other GCP services like Cloud Datastore or Cloud Pub Sub which is Google's messaging and publishing service.
* The data could also be ingested from third party services like Apache Avro and Apache Kafka. After you transform the data with Cloud Dataflow, you can analyze it in BigQuery, AI platform, or even Cloud Bigtable. Using Data Studio, you can even build real-time dashboards for IoT devices

## 4. Cloud Dataprep

* Let's learn a little bit about Cloud Dataprep. Cloud Dataprep is an Intelligent Data Service for visually exploring, cleaning, and preparing structured and unstructured data for analysis reporting and Machine Learning. Because Cloud Dataprep is serverless and works at any skill, there's no infrastructure to deploy are manage.
* Your next ideal data transformation is suggested and predicted with each UI input so you don't have to write code. With automatic schema, data types, possible joins and anomaly detection, you can skip time-consuming Data Profiling and focus on Data Analysis.
* Cloud Dataprep is an integrated partner service operated by Trifacta and based on their industry leading Data Preparation Solution Trifacta Wrangler. Google works closely with Trifacta to provide a seamless user experience that removes the need for upfront software installation, separate licensing costs or ongoing operational overhead.
* Cloud Dataprep is fully-managed and scales on demand to meet your growing data preparation needs so you can stay focused on analysis. Here's an example of a Cloud Dataprep architecture. As you can see, Cloud Dataprep can be leveraged to prepare raw data from BigQuery, Cloud Storage, or a file upload before ingesting it into a transformational pipeline like Cloud Data flow. The refined data can then be exported to BigQuery or Cloud Storage for analysis and machine learning.

## 5. Cloud Dataproc

* Let's learn a little bit about Cloud Dataproc. Cloud Dataproc is a fast easy to use fully managed Cloud service for running Apache Spark and Apache Hadoop clusters in a simpler way.
* You only pay for the resources you use with per second billing. If you leverage preemptible instances in your cluster, you can reduce your costs even further. Without using Cloud Dataproc, it can take from five to 30 minutes to create Spark and Hadoop clusters On-premise or through other infrastructure as a service providers.
* Cloud Dataproc clusters are quick to start, scale, and shut down with each of these operations taking 90 seconds or less on average. This means you can spend less time waiting for clusters and more hands-on time working with your data.
* Cloud Dataproc has built-in integration with other GCP services such as BigQuery, Cloud Storage, Cloud Bigtable, Stackdriver Logging, and Stackdriver monitoring. This provides you with the complete data platform rather than just a Spark or Hadoop cluster.
* As a managed service, you can create clusters quickly, manage them easily, and save money by turning clusters off when you don't need them. With less time and money spent on administration, you can focus on your jobs and your data.
* If you're already using Spark, Hadoop, Pig or Hive you don't even need to learn new tools or API's is to use Cloud Dataproc. This makes it easy to move existing projects into Cloud Dataproc without redevelopment.
* Now, Cloud Dataproc and Cloud Dataflow can both be used for data processing, and there's overlap in their batch and streaming capabilities. So how do you decide which product is a better fit for your environment?
* But first ask yourself whether you have dependencies on specific tools or packages in the Apache Hadoop or Spark ecosystem. If that's the case, you'll obviously want to use Cloud Dataproc. If not, ask yourself whether you prefer a hands-on or DevOps approach to Operations or a hands-off or serverless approach. If you opt for the DevOps approach, you want to use Cloud Dataproc. Otherwise, use Cloud Dataflow.

## QuizNotes

* How are Managed Services useful?
	* Managed Services may be an alternative to creating and managing infrastructure solutions.
		* Managed Services are presented as a possible alternative to building your own infrastructure data processing solution.
* Which of the following is a feature of Cloud Dataproc?
	* It typically takes less than 90 seconds to start a cluster.

## Resources

[Google Cloud Platform Ücretsiz Katmanı](https://cloud.google.com/free/)


## What’s Next? Get Certified

Validate your hands-on GCP skills and advance your career with the Associate Cloud Engineer certification. Certification can help you gain credibility and give you an advantage in today’s highly competitive market. The Associate Cloud Engineer certification is for individuals who want to demonstrate their ability to deploy applications, monitor operations, and maintain cloud projects on Google Cloud Platform. It is recommended that you have at least 6 months of hands-on experience working with GCP. The exam will assess your ability to:

	- Set up a cloud solution environment
	- Plan and configure a cloud solution
	- Deploy and implement a cloud solution
	- Ensure successful operation of a cloud solution
	- Configure access and security

I recommend broadening your knowledge by completing the following Qwiklabs Self-Paced Labs, which are single-topic hands-on activities; and Qwiklabs Quests, which are groups of self-paced labs on a focused theme:

 - [Quest: Kubernetes in the Google Cloud](https://google.qwiklabs.com/quests/29)
 - [Quest: Google Kubernetes Engine Best Practices](https://google.qwiklabs.com/quests/63)
 - Self-Paced Lab: [Cloud Functions - Qwik Start](https://google.qwiklabs.com/focuses/1763?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=3434733)
 - Self-Paced Lab: [Deploying the Application into App Engine Flexible Environment - Java](https://google.qwiklabs.com/focuses/1060?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=3434791) OR [Deploying the Application into App Engine Flexible Environment - Python](https://google.qwiklabs.com/)

To help you structure your preparation for the Associate Cloud Engineer exam, we recommend the [Preparing for the Associate Cloud Engineer Examination](https://google.qwiklabs.com/courses/903) course.

You can also prepare using the [Official Google Cloud Certified Associate Cloud Engineer Study Guide](https://www.wiley.com/en-us/Official+Google+Cloud+Certified+Associate+Cloud+Engineer+Study+Guide-p-9781119564416), published by Wiley. Visit the [Google Cloud Certification website](https://cloud.google.com/certification/cloud-engineer?utm_source=coursera&utm_medium=email&utm_campaign=spec_congrats) for more information and to register.
