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

## 4. 

## QuizNotes

* 
		
## Resources

[Cloud Storage](https://cloud.google.com/products/storage)

[Google Cloud Veritabanları](https://cloud.google.com/products/databases/)

[Access control lists (ACLs)](https://cloud.google.com/storage/docs/access-control/lists)

[CLOUD DATA TRANSFER](https://cloud.google.com/storage/docs/offline-media-import-export)

[Storage Transfer Service documentation](https://cloud.google.com/storage-transfer/docs/)

[TRANSFER CİHAZI](https://cloud.google.com/transfer-appliance/)

[Object Lifecycle Management](https://cloud.google.com/storage/docs/lifecycle)

[Object Versioning](https://cloud.google.com/storage/docs/object-versioning)



