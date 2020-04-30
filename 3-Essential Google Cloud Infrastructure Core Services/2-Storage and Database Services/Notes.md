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


## QuizNotes

* 
		
## Resources

[Cloud Storage](https://cloud.google.com/products/storage)

[Google Cloud Veritabanları](https://cloud.google.com/products/databases/)

[Access control lists (ACLs)](https://cloud.google.com/storage/docs/access-control/lists)



