## 1. Module Overview

* In this module, we cover storage and database services in GCP. Every application needs to store data, whether it's business data, media to be streamed, or sensor data from devices.
* From an application-centered perspective, the technology stores and retrieves the data. Whether it's a database or an object store is less important than whether that service supports the application's requirements for efficiently storing and retrieving the data given it its characteristics.
* Google offers several data storage services to choose from. In this module, we will cover Cloud Storage, Cloud SQL, Cloud Spanner, Cloud Firestore, and Cloud Bigtable. Let me start by giving you a high level overview of these different services. 
* BigQuery is also listed on the right. I'm mentioning the service because it sits on the edge between data storage and data processing. You can store data in BigQuery, but the intended use for BigQuery is big data analysis and interactive querying.
* is your data structured? If it's not, choose Cloud Storage. If your data is structured, does your workload focus on analytics? If it does you will want to choose Cloud Bigtable or BigQuery, depending on your latency and update needs. Otherwise, check whether your data is relational. If it's not relational choose Cloud Firestore.
* If it is relational, you will want to choose Cloud SQL or Cloud Spanner depending on your need for horizontal scalability. Depending on your application, you might use one or several of these services to get the job done.
* If it is relational, you will want to choose Cloud SQL or Cloud Spanner depending on your need for horizontal scalability. Depending on your application, you might use one or several of these services to get the job done.
* I want you to be able to set up and connect to a service without detailed knowledge of how to use a database system. If you want a deeper dive into the design, organizations, structures, schemas, and details on how data can be optimized,served, and stored properly within those different services, I recommend Google Cloud's data engineering courses.
* I'll also provide a quick overview of Cloud Memorystore, which is GCP's fully managed Redis service.

## 2. Cloud Storage  

* Cloud Storage is GCPs objects Storage Service, and it allows worldwide storage and retrieval of any amount of data at anytime. You can use Cloud Storage for a range of scenarios including serving website content storing data for archival and disaster recovery, or distributing large data objects to users via a direct download.
* Cloud Storage has a couple of key features. It's scalable to exabytes of data. The time to first byte is in milliseconds. It has very high availability across all storage classes, and it has a single API across those storage classes.
* Some like to think of Cloud Storage as files in a file system, but it's not really a file system. Instead, Cloud Storage is a collection of buckets that you place objects into. You can create directories so to speak, but really a directory is just another object that points to different objects in the bucket. You're not going to easily be able to index all of these files like you would in a file system, you just have a specific URL to access objects.
* Cloud Storage has four Storage Classes: regional, multi-regional, nearline, and coldline.
* Regional Storage enables you to store data at lower cost with the trade-off of data being stored in a specific regional location instead of having redundancy distributed over a large geographic area. I recommend using regional storage when storing frequently accessed data in the same region as your compute engine instances. This provides you with better performance for data intensive computations. You should also choose regional storage for data governance reasons. Like if you're data needs to remain in a specific region.
* Multi-regional storage on the other hand is Geo-redundant, which means Cloud Storage stores your data redundantly in at least two geographic locations separated by at least 100 miles within the multi-regional location of the bucket. Multi-regional storage can be placed only in multi-regional locations such as the United States, the European Union, or Asia. Multi-regional storage is appropriate for storing data that is frequently accessed such as serving website content, interactive workloads, or data supporting mobile and gaming applications.
* Nearline storage is a low cost highly durable storage service for storing infrequently accessed data. This storage class is a good choice when you plan to read or modify your data less than once a month because the storage cost is low, but there is an associated retrieval cost. For example, if you want to continuously add files to Cloud Storage and plan to access those files once a month for analysis, nearline storage is a great choice. I also recommend using nearline storage for backups and serving long tail multimedia content.
* Coldline storage is a very low cost, highly durable storage service for data archival, online backup, and disaster recovery. However, unlike other cold storage services, your data is available within milliseconds not hours or days. Coldline storage is the best choice for data that you plan to access at most once a year due to its lower storage costs but higher retrieval cost. You might use coldline storage if you want to archive data or have access in the event of a disaster recovery event.
* Let's focus on durability and availability. All of these storage classes have 11-9's of durability. But what does that mean? Does that mean you have access to your files t all times? No. What that means is that you won't lose data. You may not be able to access the data, which is like going to your bank and saying my money is in there, it's 11-9 durable. But when the bank is closed, I don't have access to it, which is the availability that differs between the storage classes.
* Cloud Storage is broken down into a couple of different items here. First of all, there are buckets which are required to have a globally unique name and cannot be nested. The data that you put into these buckets are objects that inherit the storage class of the bucket, and those objects could be text files, doc files, video files, etc.
* There is no minimum size to those objects, and you can scale this as much as you want as long as your quota allows it. To access the data, you can use the gsutil command or either the JSON or XML APIs. When you upload an object to the bucket, if you don't specify a storage class for the object, the object is assigned the bucket storage class. 
* You can change the default storage class of a bucket, but you can't change a regional bucket to a multi-regional and vice versa. As this slide illustrates, both multi-regional buckets and regional buckets can be changed to coldline or nearline. 
* When you upload an object, you can specify a storage class for it. You can also change the storage class of an object that already exists in your bucket without moving the object to a different bucket or changing the URL to the object. Setting a per object storage class is useful. For example, if you have objects in your bucket that you want to keep, but that you don't expect to access frequently. In this case, you can minimize costs by changing the storage class of those specified objects to nearline storage or coldline storage.
* In order to help manage the classes of objects in your bucket, Cloud Storage offers object life cycle management.
* Let's look at access control for your objects and buckets that are part of a project. We can use IAM for the project to control which individual user or service account and can see the bucket, list the objects in the bucket, view the names of the objects in the bucket, or create new buckets. 
* For most purposes, Cloud IAM is sufficient. Enrolls are inherited from project to bucket to object. Access control list or ACLs offer finer control. For even more detailed control, signed URLs provide a cryptographic key that gives time-limited access to a bucket or object. Finally, assigned policy document further defines the control by determining what kind of file can be uploaded by someone with assigned URL.
*  Let's take a closer look at ACLs and signed URLs. An ACL is a mechanism you can use to define who has access to your buckets and objects as well as what level of access they have. 
* The maximum number of ACL entries you can create for a bucket or object is a 100. Each ACL will consists of one or more entries, and these entries consists of two pieces of information. A scope which defines who can perform the specified actions, for example, a specific user or group of users, and a permission, which defines what actions can be performed, for example, read or write.
* The all users identifier listed on this slide represents anyone who was on the Internet, with or without a Google account. The all authenticated users identifier in contrast represents anyone who is authenticated with a Google account.
* For some applications, it is easier and more efficient to grant limited time access tokens that can be used by any user instead of using account-based authentication for controlling resource access, for example, when you don't want to require users to have Google accounts. Signed URLs allow you to do this for Cloud Storage. You create a URL, the grants reader right access to a specific Cloud storage resource, and specifies when the access expires.
* That URL is signed using a private key associated with the service account. When the request is received, Cloud Storage can verify that the access granting URL was issued on behalf of a trusted security principle.
* In this case, the service account and delegates it's trust of that account to the holder of the URL. After you give out the signed URL, it is out of your control. So you want the signed URL to expire after some reasonable amount of time as shown in this example.

## 3. Cloud Storage Features

* we already talked a little bit about customer-supplied encryption keys when attaching persistent disks to Virtual Machines. This allows you to supply your own encryption keys instead of the Google-managed keys which is also available for Cloud Storage. Cloud Storage also provides Object Lifecycle Management, which lets you automatically delete or archive objects.
* Another feature is object versioning, which allows you to maintain multiple versions of objects in your buckets. You are charged for the versions as if they were multiple files, which is something to keep in mind.
* Cloud Storage also offers directory synchronization so that you can sink a VM directory with a bucket. We will discuss object change notification, data import, and strong consistency in more detail after going into object versioning and Object Lifecycle Management. 
* In Cloud Storage, objects are immutable, which means that an uploaded object cannot change through its storage lifetime. To support the retrieval of objects that are deleted or overwritten, Cloud Storage offers the object versioning feature. Object versioning can be enabled for a bucket. Once enabled, Cloud Storage creates an archived version of an object each time the live version of the object is overwritten or deleted.
* The archived version retains the name of the object, but is uniquely identified by a generation number as illustrated on this slide by g1. When object versioning is enabled, you can list archived versions of an object, restore the live version of an object to an older state, or permanently delete an archived version as needed. 
* You can turn versioning on or off for a bucket at anytime. Turning versioning off leaves existing object versions in place, and causes the bucket to stop accumulating new archived object versions.
* To support common use cases like setting a time to live for objects, archiving older versions of objects, or downgrading storage classes of objects to help manage costs, Cloud Storage offers Object Lifecycle Management. 
* You can assign a lifecycle management configuration to a bucket. The configuration is a set of rules that apply to all of the objects in the bucket. So when an object meets the criteria of one of the rules, Cloud Storage automatically performs a specified action on the object. Here are some example use cases.
* Downgrade the storage class of objects older than a year to coldline storage. Delete objects created before a specific date. For example, January 1st, 2017. Keep only the three most recent versions of each object in a bucket with versioning enabled. 
* Object inspection occurs in asynchronous batches. So rules may not be applied immediately. Also updates to your lifecycle configuration may take up to 24 hours to go into effect. This means that when you change your lifecycle configuration, object lifecycle management may still perform actions based on the old configuration for up to 24 hours. So keep that in mind.
* Object change notification can be used to notify an application when an object is updated or added to a bucket through a watch request. Completing a watch request creates a new notification channel. The notification channel is the means by which a notification message is sent to an application watching a bucket. As of this recording, the only type of notification channels supported is a WebHook. 
* After a notification channel is initiated, Cloud Storage notifies the application anytime an object is added, updated, or removed from the bucket. when you add a new picture to a bucket, an application can be notified to create a thumbnail.
* However, Cloud Pub/Sub notifications are the recommended way to track changes to objects in your Cloud Storage buckets because they're faster, more flexible, easier to set up, and more cost-effective. Cloud Pub/Sub is Google's distributed real-time messaging service, which is covered in the developing applications track. 
* The GCP console allows you to upload individual files to your bucket. What if you have to upload terabytes or even petabytes of data? There are three services that address this. Transfer Appliance, Storage Transfer Service, and Offline Media Import. 
* Transfer appliance is a hardware appliance you can use to securely migrate large volumes of data from hundreds of terabytes up to one petabyte to GCP without disrupting business operations. The images on this slide are transfer appliances.
* The Storage transfer service enables high-performance imports of online data. That data source can be another Cloud Storage bucket in Amazon S3 bucket or an HTTP, HTTPS location. 
* Finally, offline media import is a third-party service where physical media such as storage arrays, hard-disk drives, tapes, and USB flash drives is sent to a provider who uploads the data. 
* When you upload an object to Cloud Storage and you receive a successor response, the object is immediately available for download and metadata operations from any location where Google offers service. This is true whether you create a new object or overwrite an existing object. Because uploads are strongly consistent, you will never receive a 404 Not Found response or stale data for a read after write or read after metadata update operation.
* Strong global consistency also extends to deletion operations on objects. If a deletion requests succeeds, an immediate attempt to download the object or its metadata will result in a 404 Not Found status code. You get the 404 error because the object no longer exists after the delete operation succeeds. 
* Bucket listing is strongly consistent. For example, if you create a bucket then immediately perform a list buckets operation, the new bucket appears in the returned list of buckets.
* Finally, object listing is also strongly consistent. For example, if you upload an object to a bucket and then immediately perform a list objects operation, the new object appears in the returned list of objects.
* Let's explore the decision tree to help you find the appropriate storage class in Cloud Storage.. If you will read your data less than once a year, you should consider using coldline storage.
* If you will read your data less than once a month, you should consider using Nearline storage, and if you'll be doing reads and writes more often than that, you should consider choosing multi-regional or regional depending on your locality needs. 

## 4. Cloud SQL

* Let's dive into the structured or relational database services. First step is Cloud SQL. Why would you use a GCP service for SQL, when you can install a SQL Server application image on a VM using Compute Engine? The question really is, should you build your own database solution or use a managed service? There are benefits to using a managed service. So let's learn about why you'd use Cloud SQL as a managed service inside of GCP.
* Cloud SQL is a fully managed service of either MySQL or PostgreSQL databases. This means that patches and updates are automatically applied, but you still have to administer MySQL users with the native authentication tools that come with these databases.
* Cloud SQL supports many clients such as Cloud Shell, App Engine, and G-Suite scripts. It also supports other applications and tools that you might be used to using like SQL Workbench, Toad, and other external applications using standard MySQL drivers.
* Cloud SQL delivers high performance and scalability with up to 30 terabytes of storage capacity, 40,000 IOPS, and 416 gigabytes of RAM per instance. You can easily scale up to 64 processor cores, and scale out with read replicas. 
* Let's focus on some other services provided by Cloud SQL. There is a replica service that can replicate data between multiple zones as shown on the right. This is useful for automatic failover if an outage occurs. Cloud SQL also provides automated and on-demand backups with point-in-time recovery. You can import and export databases using MySQL dump, or import and export CSV files. Cloud SQL can also scale up which does require a machine restart or scale out using read replicas. That being said, if you are concerned about horizontal scalability, you'll want to consider Cloud Spanner
* Choosing a connection type to your Cloud SQL instance, will influence how secure, performance, and automated it will be. If you are connecting an application that is hosted within the same GCP project as your Cloud SQL instance, and it is co-located in the same region, choosing the private IP connection will provide you with the most performance and secure connection using private connectivity.
* In other words, traffic is never exposed to the public Internet. If the application is hosted in another region or project, or if you are trying to connect to your Cloud SQL instance from outside of GCP, you have three options.
* In this case, I recommend using Cloud Proxy which handles authentication, encryption, and key rotation for you. If you need manual control over the SSL connection, you can generate and periodically rotate the certificates yourself. Otherwise, you can use an unencrypted connection by authorizing a specific IP address, to connect to your SQL server, over its external IP address.
* To summarize, let's explore this decision tree to help you find the right data storage service with full relational capability.
* If you need more than 30 terabytes of storage space, or over 4,000 concurrent connections to your database, or if you want your application designed to be responsible for scaling, availability, and location management when scaling up globally, then consider using Cloud Spanner which we will cover later in this module. If you have no concerns with these constraints, ask yourself whether you have specific OS requirements, custom database configuration requirements, or special backup requirements. If you do, consider hosting your own database on a VM using Compute Engine.
* Otherwise, I strongly recommend using Cloud SQL as a fully managed service for your relational databases. 
* Private IP is an internal connection, unlike external IP, which egresses to the internet.

## 5. Cloud Spanner

* If Cloud SQL does not fit your requirements because you need horizontal scalability, consider using Cloud Spanner. Cloud Spanner is a service built for the Cloud, specifically to combine the benefits of relational database structure with non-relational horizontal scale. 
* This service can provide petabytes of capacity and offers transactional consistency at global scale, schemas, SQL, and automatic synchronous replication for high availability. Use cases include financial applications and inventory applications, traditionally served by relational database technology. 
* Let's compare Cloud Spanner with both relational and non-relational databases. Like a relational database, Cloud Spanner has schema, SQL, and strong consistency. Also like a non-relational database, Cloud Spanner offers high availability, horizontal scalability, and configurable replication. As mentioned, Cloud Spanner offers the best of the relational and non-relational worlds.
* These features allow for mission-critical use cases such as building consistent systems for transactions and inventory management in the financial services in retail industries. To better understand how all of it works, let's look at the architecture of Cloud Spanner.
* Cloud Spanner instance replicates data in n Cloud zones, which can be within one region or across several regions. The database placement is configurable. Meaning, you can choose which region to put your database in. This architecture allows for high availability and global placement.
* The replication of data, will be synchronized across zones using Google's global fiber network. Using atomic clocks, ensures atomicity whenever you are updating your data. That's as far as we're going to go with Cloud Spanner. Because the focus of this module, is to understand the circumstances when you would use Cloud Spanner. 
* Let's look at a decision tree. If you have outgrown any relational database or sharding your databases for throughput high-performance, need transactional consistency, global data, and strong consistency, or just want to consolidate your database. Consider using Cloud Spanner. If you don't need any of these nor full relational capabilities, consider a NoSQL service such as Cloud fire store which we will cover next. 

## 6. Cloud Firestore

* If you are looking for a highly scalable NoSQL database for your applications, consider using Cloud Firestore. Cloud Firestore is a fast, fully managed, serverless Cloud native, NoSQL document database, that simplifies storing, sinking, and querying data for your mobile, web, and IoT apps at global scale. 
* It's client libraries provide live synchronization and offline support, and it's security features and integrations with Firebase and GCP accelerate building truly serverless apps. Cloud Firestore also supports ACID transactions. So if any of the operations in the transaction fail and cannot be retried, the whole transaction will fail. Also with automatic multi-region replication and strong consistency, your data is safe and available even when disasters strike. 
* Cloud Firestore also supports ACID transactions. So if any of the operations in the transaction fail and cannot be retried, the whole transaction will fail. Also with automatic multi-region replication and strong consistency, your data is safe and available even when disasters strike.
* Cloud Firestore even allows you to run sophisticated queries against your NoSQL data, without any degradation in performance, this gives you more flexibility in the way you structure your data. 
* Cloud Firestore is actually the next generation of Cloud Datastore. Cloud Firestore can operate in Datastore mode, making it backwards compatible with Cloud Datastore. By creating a Cloud Firestore database in Datastore mode, you can access Cloud Firestore improved storage layer, while keeping Cloud Datastore system behavior. 
* This removes the following Cloud Datastore limitations. Queries are no longer eventually consistent. Instead they are all strongly consistent. Transactions are no longer limited to 25 entity groups, rights to an entity group are no longer limited to one per second. Cloud Firestore in native mode, introduces new features such as a new strongly consistent storage layer. A collection and document data model, real-time updates, mobile and web client libraries.
* Cloud Firestore is backward compatible with Cloud Datastore, but the new data mode, real-time updates in mobile and web client library features are not. To access all of the new Cloud Firestore features, you must use Cloud Firestore in native mode. A general guideline is to use Cloud Firestore in Datastore mode for new server projects and native mode for new mobile and web apps. As the next generation of Cloud Datastore, Cloud Firestore is compatible with all Cloud Datastore APIs and client libraries.
* To summarize, let's explore this decision tree, to help you determine whether Cloud Firestore is the right storage service for your data. If your schema might change and you need an adaptable database, you need to scale to zero or you want low maintenance overhead scaling up to terabytes, consider using Cloud Firestore. Also, if you don't require transactional consistency, you might want to consider Cloud Bigtable, depending on the cost or size.

## 7. Cloud Bigtable

* If you don't require transactional consistency, you might want to consider Cloud Bigtable. Cloud Bigtable is a fully managed NoSQL database with petabyte-scale and very low latency. It seamlessly scales for throughput, and it learns to adjust to specific access patterns.
* Cloud Bigtable is actually the same database that powers many of Google's core services including Search, Analytics, Maps, and Gmail. Cloud Bigtable is a great choice for both operational and analytical applications including IoT, user analytics, and financial data analysis because it supports high read and write throughput at low latency. It's also a great storage engine for machine learning applications.
* Cloud Bigtable integrates easily with popular big data tools like Hadoop, Cloud Dataflow, and Cloud Dataproc, plus Cloud Bigtable supports the open-source industry standard HBase API, which makes it easy for your development teams to get started.
* Cloud Bigtable stores data in massively scalable tables, each of which is a sorted key value map. The table is composed of rows, each of which typically describes a single entity, and columns which contain individual values for each row. Each row is indexed by a single row key. 
* Columns that are related to one another are typically grouped together into a column family. Each column is identified by a combination of the column family and a column qualifier which is a unique name within the column family. Each row column intersection can contain multiple cells or versions at different timestamps, providing a record of how the stored data has been altered over time. Cloud Bigtable tables are sparse. If a cell does not contain any data, it does not take up any space.  
* The example shown here is for a hypothetical social network for United States presidents, where each president can follow posts from other presidents. Let me highlight some things. The table contains one column family, the follows family. This family contains multiple column qualifiers.
* Column qualifiers are used as data. This design choice takes advantage of the sparseness of Cloud Bigtable tables and the fact that new column qualifiers can be added as your data changes. The username is used as the row key. Assuming usernames are evenly spread across the alphabet, data access will be reasonably uniform across the entire table. 
* This diagram shows a simplified version of Cloud Bigtables overall architecture. It illustrates that processing which is done through a front end server pool and nodes is handled separately from the storage. 
* A Cloud Bigtable table is sharded into blocks of contiguous rows called tablets, to help balance the workload of queries. Tablets are similar to HBase regions, for those of you who might have used the HBase API.
* Tablets are stored on Colossus which is Google's file system in SSTable format. An SSTable provides a persistent, ordered, immutable map from keys to values where both keys and values are arbitrary byte strings. As I mentioned earlier, Cloud Bigtable learns to adjust to specific access patterns.
*  If a certain Bigtable node is frequently accessing a certain subset of data, Cloud Bigtable will update the indexes so that other nodes can distribute that workload evenly as shown here. That throughput scales linearly, so for every single node that you do add, you're going to see a linear scale of throughput performance up to hundreds of nodes.
* In summary, if you need to store more than one terabyte of structured data, have very high volumes of writes. Need read write latency of less than 10 milliseconds along with strong consistency or need a storage service that is compatible with the HBase API. Consider using Cloud Bigtable. If you don't need any of these and are looking for a storage service that scales down well, consider using Cloud Firestore. 
* Speaking of Scaling, the smallest Cloud Bigtable cluster you can create has three nodes and can handle 30,000 operations per second. Remember that you pay for those nodes while they are operational, whether your application is using them or not.

## 8. Cloud Memorystore

* Let me give you a quick overview of Cloud Memorystore. Cloud Memorystore for Redis provides a fully managed in-memory data store service built on scalable, secure, and highly available infrastructure managed by Google. Applications running on GCP can achieve extreme performance by leveraging the highly scalable available secure Redis service without the burden of managing complex reddest deployments. 
* This allows you to spend more time writing code, so that you can focus on building great apps. Cloud Memorystore also automates complex tasks like enabling high availability, failover, patching, and monitoring. High availability instances are replicated across two zones and provide a 99.9 percent availability SLA.
* You can easily achieve this sub-millisecond latency and throughput your applications need. Start with the lowest tier and smallest size and then grow your instance effortlessly with minimal impact to application availability.
* Cloud Memorystore can support instances of up to 300 gigabytes and network throughput of 12 gigabytes per second. Because Cloud Memorystore for Redis is fully compatible with the Redis protocol, you can lift-and-shift your applications from open-source Redis to Cloud Memorystore without any code changes by using the import export feature. There is no need to learn new tools because all existing tools in Client Libraries just work.

## 9. Module Review

* In this module, we covered the different storage and database services that GCP offers.
* Cloud Storage, a fully managed object store; 
* Cloud SQL, a fully managed MySQL and PostgreSQL database service; 
* Cloud Spanner, a relational database service with transactional consistency, global scale and high availability; 
* Cloud Fire Store, a fully managed NoSQL document database; 
* Cloud Bigtable, a fully managed NoSQL wide column database 
* Cloud Memorystore, a fully managed in-memory data store service for Redis.  
*  From an infrastructure perspective, the goal was to understand what services are available and how they are used in different circumstances. 

## QuizNotes

* What data storage service might you select if you just needed to migrate a standard relational database running on a single machine in a datacenter to the cloud?
	* Cloud SQL
		* Cloud SQL offers a PostgreSQL server or a MySQL server as a managed service.
* Which data storage service provides data warehouse services for storing data but also offers an interactive SQL interface for querying the data?
	* BigQuery
		* BigQuery is a data warehousing service that allows the storage of huge data sets while making them immediately processable without having to extract or run the processing in a separate service.
* Which GCP data storage service offers ACID transactions and can scale globally?
	* Cloud Spanner
		* Cloud Spanner provides ACID (Atomicity, Consistency, Isolation, Durability) properties that enable transactional reads and writes on the database. It can also scale globally.

## Resources

[Cloud Storage](https://cloud.google.com/products/storage)

[Google Cloud Veritabanları](https://cloud.google.com/products/databases/)

[Access control lists (ACLs)](https://cloud.google.com/storage/docs/access-control/lists)

[CLOUD DATA TRANSFER](https://cloud.google.com/storage/docs/offline-media-import-export)

[Storage Transfer Service documentation](https://cloud.google.com/storage-transfer/docs/)

[TRANSFER CİHAZI](https://cloud.google.com/transfer-appliance/)

[Object Lifecycle Management](https://cloud.google.com/storage/docs/lifecycle)

[Object Versioning](https://cloud.google.com/storage/docs/object-versioning)

[Private IP](https://cloud.google.com/sql/docs/mysql/private-ip)

[Migration from MySQL to Cloud SQL](https://cloud.google.com/solutions/migrating-mysql-to-cloudsql-concept)

[Cloud Spanner Service Level Agreement (SLA)](https://cloud.google.com/spanner/sla)

[Migrating from MySQL to Cloud Spanner](https://cloud.google.com/solutions/migrating-mysql-to-spanner)

[Choosing between Native Mode and Datastore Mode](https://cloud.google.com/datastore/docs/firestore-or-datastore)

[Automatic Upgrade to Firestore](https://cloud.google.com/datastore/docs/upgrade-to-firestore)

[Apache HBase](https://hbase.apache.org/)


