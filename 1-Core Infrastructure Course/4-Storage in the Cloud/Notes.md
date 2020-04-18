## 1. Module introduction

* Every application needs to store data, maybe media to be streamed or censor data from devices or customer account balances, or maybe the fact
* Cloud Platform has other storage options to meet your needs for structured, unstructured, transactional and relational data.
* about the core storage options: Cloud Storage, Cloud SQL, Cloud Spanner, Cloud Data Store and Google Big Table.

## 2. Cloud Storage

* object storage means you save to your storage here, you keep this arbitrary bunch of bytes I give you and the storage lets you address it with a unique key.
* Often these unique keys are in the form of URLs which means object storage interacts nicely with Web technologies.
* You can use Cloud Storage for lots of things: serving website content, storing data for archival and disaster recovery, or distributing large data objects to your end users via Direct Download. 
* Cloud Storage is not a file system because each of your objects in Cloud Storage has a URL.
* Cloud Storage is object storage rather than file storage. Compute Engine virtual machines use Persistent Disk storage to contain their file systems.
* Cloud Storage is comprised of buckets you create and configure and use to hold your storage objects. The storage objects are immutable, which means that you do not edit them in place but instead you create new versions. 
* Cloud Storage always encrypts your data on the server side before it is written to disk. Also by default, data in-transit is encrypted using HTTPS.
* Cloud Storage files are organized into buckets. When you create a bucket, you give it a globally unique name. You specify a geographic location where the bucket and its contents are stored and you choose a default storage class. Pick a location that minimizes latency for your users.
* Roles are inherited from project to bucket to object. If you need finer control, you can create access control lists - ACLs - that offer finer control. ACLs define who has access to your buckets and objects as well as what level of access they have.
* Each ACL consists of two pieces of information, 
	* Scope, which defines who can perform the specified actions, for example, a specific user or group of users 
	* Permission which defines what actions can be performed. For example, read or write. 
* You can turn on object versioning on your buckets if you want. If you do, Cloud Storage keeps a history of modifications. That is, it overrides or deletes all of the objects in the bucket.
* If you don't turn on object versioning, new always overrides old.
*  Cloud Storage also offers lifecycle management policies.

## 3. Cloud Storage interactions

* Cloud Storage lets you choose among four different types of storage classes: Regional, Multi-regional, Nearline, and Coldline.
* Multi-regional and Regional are high-performance object storage, whereas Nearline and Coldline are backup and archival storage. 
* Regional storage lets you store your data in a specific GCP region: US Central one, Europe West one or Asia East one.  It's cheaper than Multi-regional storage but it offers less redundancy.
* Multi-regional storage on the other hand, cost a bit more but it's Geo-redundant. That means you pick a broad geographical location like the United States, the European Union, or Asia and cloud storage stores your data in at least two geographic locations separated by at least 160 kilometers. Multi-regional storage is appropriate for storing frequently accessed data. For example, website content, interactive workloads, or data that's part of mobile and gaming applications.
* People use regional storage on the other hand, to store data close to their Compute Engine, virtual machines, or their Kubernetes engine clusters. That gives better performance for data-intensive computations. 
* Nearline storage is a low-cost, highly durable service for storing infrequently accessed data. The storage class is a better choice than Multi-regional storage or Regional storage in scenarios where you plan to read or modify your data once a month or less on average. 
* Coldline storage is a very low cost, highly durable service for data archiving, online backup, and disaster recovery. Coldline storage is the best choice for data that you plan to access -at most - once a year. This is due to its slightly lower availability, 90-day minimum storage duration, costs for data access, and higher per operation costs.
* As for pricing, all storage classes incur a cost per gigabyte of data stored per month, with Multi-regional having the highest storage price and Coldline the lowest storage price. 
* Nearline storage also incurs an access fee per gigabyte of data read and Coldline storage incurs a higher fee per gigabyte of data read.
* Many customers simply use gsutil which is the cloud storage command from this cloud SDK. You can also move data in with a drag and drop in the GCP console, if you use the Google Chrome browser. 
* Google Cloud platform offers the **online storage transfer service** and the offline transfer appliance to help
* **The storage transfer service** lets you schedule and manage batch transfers to cloud storage from another cloud provider from a different cloud storage region or from an HTTPS endpoint. 
* **The transfer appliance** is a rackable, high-capacity storage server that you lease from Google Cloud. You simply connect it to your network, load it with data, and then ship it to an upload facility where the data is uploaded to cloud storage. This service enables you to securely transfer up to a petabyte of data on a single appliance.
* There are other ways of getting your data into cloud storage as this storage option is tightly integrated with many of the Google cloud platform products and services.
* you can import and export tables from and to BigQuery as well as Cloud SQL. You can also store App Engine logs, cloud data store backups, and objects used by App Engine applications like images. Cloud storage can also store instant startup scripts, Compute Engine images, and objects used by Compute Engine applications.
* cloud storage is often the ingestion point for data being moved into the cloud and is frequently the long-term storage location for data.

## 4. Google Cloud Bigtable

* Cloud Bigtable is Google's NoSQL, big data database service. 
* Your databases in Bigtable are sparsely populated tables that can scale to billions of rows and thousands of columns allowing you to store petabytes of data.
* GCP fully manages the surface, so you don't have to configure and tune it. 
* Cloud Bigtable is ideal for storing large amounts of data with very low latency. 
* It supports high throughput, both read and write, so it's a great choice for both operational and analytical applications including Internet of Things, user analytics and financial data analysis.
* Cloud Bigtable is offered through the same open source API as HBase, which is the native database for the Apache Hadoop project.
* scalability. If you manage your own Hbase installation, scaling past a certain rate of queries per second is going to be tough, but with Bigtable you can just increase your machine count which doesn't even require downtime.
* Cloud Bigtable handles administration tasks like upgrades and restarts transparently. All data in Cloud Bigtable is encrypted in both in-flight and at rest. You can even use IAM permissions to control who has access to Bigtable data. 
* Data can also be streamed in through a variety of popular stream processing frameworks, like Cloud Dataflow Streaming, Spark Streaming and Storm.
*  If streaming is not an option, data can also be read from and written to Cloud Bigtable through batch processes like Hadoop map reduce, Dataflow or Spark. 

## 5. Google Cloud SQL and Google Cloud Spanner

* relational databases are a lot of work to set up, maintain, manage, and administer.
* Cloud SQL offers both MySQL and PostgreSQL databases that are capable of handling terabytes of storage.
* Cloud SQL provides several replica services like read, failover, and external replicas. This means that if an outage occurs, Cloud SQL can replicate data between multiple zones with automatic failover.
* Cloud SQL also helps you backup your data with either on-demand or scheduled backups. It can also scale both vertically by changing the machine type, and horizontally via read replicas.
* Cloud SQL instances, is they are accessible by other GCP services and even external services. You can authorize Compute Engine instances for access Cloud SQL instances and configure the Cloud SQL instance to be in the same zone as your virtual machine. 
* Each Cloud SQL database is configured at creation time for either MySQL or PostgreSQL. Cloud Spanner uses ANSI SQL 2011 with extensions.
* If Cloud SQL does not fit your requirements because you need horizontal scaleability, consider using Cloud Spanner. It offers transactional consistency at a global scale, schemas, SQL, and automatic synchronous replication for high availability.
* Cloud Spanner have outgrown any relational database, or sharding your databases for throughput high performance, need transactional consistency, global data and strong consistency, or just want to consolidate your database. 
* Cloud Spanner can scale to petabyte database sizes, while Cloud SQL is limited by the size of the database instances you choose. At the time this quiz was created, the maximum was 10,230 GB.
* Cloud Spanner offers transactional consistency at global scale.

## 6. Google Cloud Datastore

* Another highly scalable NoSQL database choice for your applications is Cloud Datastore.
* One of its main use cases is to store structured data from App Engine apps.
* You can also build solutions that span App Engine and Compute Engine with Cloud Datastore as the integration point.
* As you would expect from a fully-managed service, Cloud Datastore automatically handles sharding and replication, providing you with a highly available and durable database that scales automatically to handle load.
* Unlike Cloud Bigtable, it also offers transactions that affect multiple database rows, and it lets you do SQL-like queries.
* Cloud Datastore has a free daily quota that provides storage, reads, writes, deletes and small operations

## 7. Comparing Storage Options

* Consider using Cloud Datastore if you need to store unstructured objects or if you require support for transactions and SQL-like queries. This storage service provides terabytes of capacity with a maximum unit size of one megabyte per entity.
* Consider using Cloud Bigtable if you need to store a large amount of structured objects. Cloud Bigtable does not support SQL's queries nor does it support multi-row transactions. This storage service provides petabytes of capacity with a maximum unit size of 10 megabytes per cell and 100 megabytes per row. 
* Consider using Cloud Storage if you need to store immutable blobs larger than 10 megabytes such as large images or movies. This storage service provides petabytes of capacity with a maximum unit size of five terabytes per object.
* Consider using Cloud SQL or Cloud Spanner if you need full SQL support for an online transaction processing system. Cloud SQL provides terabytes of capacity, while Cloud Spanner provides petabytes. If Cloud SQL does not fit your requirements because you need horizontal scalability not just through read replicas, consider using Cloud Spanner.
* The usual reason to store data in BigQuery is to use its big data analysis and interactive query and capabilities.
* Cloud Datastore is the best for semi-structured application data that is used in app engines' applications.
* Bigtable is best for analytical data with heavy read/write events like AdTech, Financial or IoT data.
* Cloud Storage is best for structured and unstructured, binary or object data like images, large media files and backups.
* SQL is best for web frameworks and in existing applications like storing user credentials and customer orders. 
* Cloud Spanner is best for large scale database applications that are larger than two terabytes


## QuizNotes

* You are developing an application that transcodes large video files. Which storage option is the best choice for your application?
	* Cloud Storage
* You manufacture devices with sensors and need to stream huge amounts of data from these devices to a storage option in the cloud. Which Google Cloud Platform storage option is the best choice for your application?
	* Cloud BBigtable
* Which statement is true about objects in Cloud Storage?
	* They are immutable, and new versions overwrite old unless you turn on versioning.
* You are building a small application. If possible, you'd like this application's data storage to be at no additional charge. Which service has a free daily quota, separate from any free trials?
	* Cloud Datastore
* How do the Nearline and Coldline storage classes differ from Multi-regional and Regional? Choose all that are correct
	* Nearline and Coldline assess lower storage fees.
	* Nearline and Coldline assess additional retrieval fees. 
* Your application needs a relational database, and it expects to talk to MySQL. Which storage option is the best choice for your application?
	* Cloud SQL
* Your application needs to store data with strong transactional consistency, and you want seamless scaling up. Which storage option is the best choice for your application?
	* Cloud Spanner
* Which GCP storage service is often the ingestion point for data being moved into the cloud, and is frequently the long-term storage location for data?
	* Cloud Storage

## Resources

[Cloud Storage](https://cloud.google.com/storage/)

[Integration with Google Cloud services and tools](https://cloud.google.com/storage/docs/google-integration)

[Cloud Bigtable documentation](https://cloud.google.com/bigtable/docs/)

[Cloud SQL](https://cloud.google.com/sql/docs/)

[Cloud Spanner documentation](https://cloud.google.com/spanner/docs/)

[Firestore in Datastore mode documentation](https://cloud.google.com/datastore/docs/)

[Cloud Storage ürünleri](https://cloud.google.com/storage-options)

[DevBytes - File Storage in the Cloud](https://www.youtube.com/watch?v=vyIap827rHs)

[Quickstart for Cloud SQL for MySQL](https://cloud.google.com/sql/docs/mysql/quickstart)

[]

