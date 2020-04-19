## 1. Introduction to Big Data and Machine Learning

* Google believes that in the future, every company will be a data company. Because making the fastest and best use of data is a critical source of competitive advantage.
* Google Cloud provides a way for everybody to take advantage of Google's investments in infrastructure and data processing innovation. Google Cloud has automated out the complexity of building and maintaining data and analytics systems. 
* Google's technologies for getting the most out of data fastest. Whether it's real time analytics or machine learning. These tools are intended to be simple and practical for you to embed in your applications so that you can put data into the hands of your domain experts and get insights faster.

## 2. Google Cloud Big Data Platform

* Google Cloud Big Data Solutions are designed to help you transform your business and user experiences with meaningful data insights.
* We like to call it an Integrated Serverless Platform. What does that mean? Serverless means you don't have to worry about provisioning Compute Instances to run your jobs. 
* The services are fully managed, and you pay only for the resources you consume. The platform is integrated, so that GCP data services work together to help you create custom solutions.
* Apache Hadoop is an open source framework for big data. It is based on the MapReduce programming model which Google invented and published.
* The MapReduce model is, at its simplest, means that one function, traditionally called the "Map function," runs in parallel with a massive dataset to produce intermediate results. And another function, traditionally called the "Reduce function," builds a final result set based on all those intermediate results.
* The term "Hadoop" is often used informally to encompass Apache Hadoop itself, and related projects such as Apache Spark, Apache Pig, and Apache Hive. 
* Cloud Dataproc is a fast, easy, managed way to run Hadoop, Spark, Hive, and Pig on Google Cloud Platform. All you have to do is request a Hadoop cluster. It will be built for you in 90 seconds or less, on top of Compute Engine virtual machines whose number and type you control. If you need more or less processing power while your cluster is running, you can scale it up or down. 
* You can use the default configuration for the Hadoop software in your cluster or you can customize it. And you can monitor your cluster using Stackdriver. Running on-premises, Hadoop jobs requires a capital hardware investment. Running these jobs in Cloud Dataproc, allows you to only pay for hardware resources used during the life of the cluster you create.
* Although the rate for pricing is based on the hour, Cloud Dataproc is billed by the second. Our Cloud Dataproc clusters are billed in one-second clock-time increments, subject to a one minute minimum billing. So, when you're done with your cluster, you can delete it, and billing stops. This is much more agile use of resources than on-premise hardware assets. You can also save money, by telling Cloud Dataproc to use preemptible Compute Engine instances for your batch processing.
* Be aware that the costs of the Compute Engine instances isn't the only component of the cost of a Dataproc cluster, but it's a significant one. Once your data is in a cluster, you can use Spark and Spark SQL to do data mining. And you can use MLib, which is Apache Spark's machine learning libraries to discover patterns through machine learning.

## QuizNotes

* 
	
## Resources

[Smart Analytics-Big Data](https://cloud.google.com/products/big-data/)



