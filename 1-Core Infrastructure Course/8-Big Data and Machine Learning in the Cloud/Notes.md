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

## 3. Cloud Dataflow

* Cloud Dataproc is great when you have a data set of known size or when you want to manage your cluster size yourself. It's both a unified programming model and a managed service and it lets you develop and execute a big range of data processing patterns: extract, transform, and load batch computation and continuous computation.
* You use Dataflow to build data pipelines. And the same pipelines work for both batch and streaming data. There's no need to spin up a cluster or to size instances. Cloud Dataflow fully automates the management of whatever processing resources are required. Cloud Dataflow frees you from operational tasks like resource management and performance optimization. 
* Dataflow pipeline reads data from a big query table, the Source, processes it in a variety of ways, the Transforms, and writes its output to a cloud storage, the Sink. Some of those transforms you see here are map operations and some are reduce operations. You can build really expressive pipelines.
* People use Dataflow in a variety of use cases. As we've discussed, it's a general purpose ETL tool and its use case as a data analysis engine comes in handy in things like fraud detection and financial services, IoT analytics and manufacturing, healthcare and logistics and click stream, point of sale and segmentation analysis in retail.
* And because those pipelines, we saw can orchestrate multiple services even external services. It can be used in real time applications such as personalizing gaming user experiences.

## 4. BigQuery

* Suppose, instead of a dynamic pipeline, your data needs to run more in the way of exploring a vast sea of data. You want to do ad-hoc SQL queries on a massive data set. That's what BigQuery is for. 
* It's Google's fully-managed, petabyte-scale, low-cost analytics data warehouse. Because there's no infrastructure to manage, you can focus on analyzing data to find meaningful insights, use familiar SQL and take advantage of our pay-as-you-go model. It's easy to get data into BigQuery. 
* You can load it from cloud storage or cloud data store, or stream it into BigQuery at up to 100,000 rows per second. Once it's in there, you can run super-fast SQL queries against multiple terabytes of data in seconds using the processing power of Google's infrastructure. 
* SQL queries, you can easily read and write data in BigQuery via Cloud Dataflow, Hadoop, and Spark. BigQuery is used by all types of organizations from startups to Fortune 500 companies - smaller organizations like Big Query's free monthly quotas, bigger organizations like its seamless scale
* BigQuery lets you specify the region where your data will be kept. So, for example, if you want to keep data in Europe, you don't have to go set up a cluster in Europe. Just specify the EU location where you create your data set. US and Asia locations are also available. Because BigQuery separates storage and computation, you pay for your data storage separately from queries. That means, you pay for queries only when they are actually running.
* You have full control over who has access to the data stored in BigQuery, including sharing data sets with people in different projects. If you share data sets that won't impact your cost or performance. People you share with pay for their own queries, not you. 
* Long-term storage pricing is an automatic discount for data residing in BigQuery for extended periods of time. When the age of your data reaches 90 days in BigQuery, Google will automatically drop the price of storage.

## 5. Cloud Pub/Sub and Cloud Datalab

* Whenever you're working with events in real time, it helps to have a messaging service. That's what Cloud Pub/Sub is. It's meant to serve as a simple, reliable, scalable foundation for stream analytics. You can use it to let independent applications you build send and receive messages. 
* That way they're decoupled, so they scale independently. The Pub in Pub/Sub is short for publishers and Sub is short for subscribers. Applications can publish messages in Pub/Sub and one or more subscribers receive them. 
* Receiving messages doesn't have to be synchronous. That's what makes Pub/Sub great for decoupling systems. It's designed to provide "at least once" delivery at low latency. When we say "at least once delivery," we mean that there is a small chance some messages might be delivered more than once. So, keep this in mind when you write your application.
* Cloud Pub/Sub offers on-demand scalability to one million messages per second and beyond. You just choose the quota you want. Cloud Pub/Sub builds on the same technology Google uses internally. It's an important building block for applications where data arrives at high and unpredictable rates, like Internet of Things systems. If you're analyzing streaming data, Cloud Dataflow is a natural pairing with Pub/Sub. Pub/Sub also works well with applications built on GCP's Compute Platforms.
* You can configure your subscribers to receive messages on a push or pull basis. In other words, subscribers can get notified when new messages arrive for them or they can check for new messages at intervals. 
* 	Scientists have long used lab notebooks to organize their thoughts and explore their data. For data science, the lab notebook metaphor works really well, because it feels natural to intersperse data analysis with comments about their results.
* A popular environment for hosting those is Project Jupyter. It lets you create and maintain web-based notebooks containing Python code and you can run that code interactively and view the results. And Cloud Datalab takes the management work out of this natural technique. It runs in a Compute Engine virtual machine. To get started, you specify the virtual machine type you want and what GCP region it should run in. When it launches, it presents an interactive Python environment that's ready to use. And it orchestrates multiple GCP services automatically, so you can focus on exploring your data.
* You only pay for the resources you use. There is no additional charge for Datalab itself. It's integrated with BigQuery, Compute Engine, and Cloud Storage, so accessing your data doesn't run into authentication hassles. 
* When you're up and running, you can visualize your data with Google Charts or map plot line and because there's a vibrant interactive Python community, you can learn from published notebooks. There are many existing packages for statistics, machine learning, and so on.

## 6. Google Cloud Machine Learning Platform

* Machine learning is one branch of the field of artificial intelligence. It's a way of solving problems without explicitly coding the solution. Instead, human coders build systems that improve themselves over time through repeated exposure to sample data, which we call training data. 
* Major Google applications use machine learning like YouTube, Photos, the Google Mobile App and Google Translate. The Google Machine Learning Platform is now available as a cloud service so that you can add innovative capabilities to your own applications. 
* Cloud Machine Learning Platform provides modern machine learning services with pre-trained models and a platform to generate your own tailored models. As with other GCP products, there's a range of services that stretches from the highly general to the pre-customized.
* TensorFlow is an open source software library that's exceptionally well suited for machine learning applications like neural networks. It was developed by Google Brain for Google's internal use and then open source so that the world could benefit. You can run TensorFlow wherever you like but GCP is an ideal place for it because machine learning models need lots of on-demand compute resources and lots of training data. 
* TensorFlow can also take advantage of Tensor Processing Units, which are hardware devices designed to accelerate machine learning workloads with TensorFlow. GCP makes them available in the cloud with Compute Engine virtual machines. Each cloud TPU provides up to 180 teraflops of performance. And because you pay for only what you use, there's no upfront capital investment required. Suppose you want a more managed service.
* Google Cloud Machine Learning Engine lets you easily build machine learning models that work on any type of data of any size. It can take any TensorFlow model and perform large-scale training on a managed cluster. Finally, suppose you want to add various machine learning capabilities to your applications without having to worry about the details of how they are provided.
* People use the Cloud Machine Learning Platform for lots of applications. Generally, they fall into two categories, depending on whether the data they work on is structured or unstructured. Based on structured data, you can use ML for various kinds of classification and regression tasks like customer churn analysis, product diagnostics and forecasting. It can be the heart of a recommendation engine for content personalization and cross-sells and up-sells. You can use ML to detect anomalies, as in fraud detection, sensor diagnostics or log metrics. 
* Based on unstructured data, you can use ML for image analytics such as identifying damaged shipment, identifying styles and flagging content. You can do text analytics too, like a call center, blog analysis, language identification, topic classification and sentiment analysis. In many of the most innovative applications for machine learning, several of these kinds of applications are combined.

## 7. Machine learning APIs

* The Cloud Vision API enables developers to understand the content of an image. It quickly classifies images into thousands of categories detects individual objects within images, and finds and reads printed words contained within images. Like the other APIs I'm describing here, encapsulates powerful machine learning models behind an easy-to-use API. You can use it to build metadata on your image catalog, moderate offensive content or even do image sentiment analysis.
* The Cloud Speech API enables developers to convert audio to text. Because you have an increasingly global user base, The API recognizes over 80 languages and variants. You can transcribe the text of users, dictating in an applications' microphone, enable command and control through voice or transcribe audio files. 
* The Cloud Natural Language API offers a variety of natural language understanding technologies to developers. It can do syntax analysis, breaking down sentences supplied by our users into tokens, identify the nouns, verbs, adjectives, and other parts of speech and figure out the relationships among the words. It can do entity recognition. In other words, it can parse text and flag mentions of people, organizations, locations, events, products and media. It can understand the overall sentiment expressed in a block of text. It has these capabilities in multiple language, including English, Spanish, and Japanese.
* Cloud Translation API provides a simple, programmatic interface for translating an arbitrary string into a supported language. When you don't know the source language, the API can detect it. 
* The Cloud Video Intelligence API lets you annotate videos in a variety of formats. It helps you identify key entities - that is, nouns - within your video and when they occur. You can use it to make video content searchable and discoverable.

## QuizNotes

* Name two use cases for Google Cloud Dataproc
	* Data mining and analysis in datasets of known size
	* Manage data that arrives in realtime
* Name two use cases for Google Cloud Dataflow
	* Orchestration
	* Extract, Transform and Load (ETL)
* Name three use cases for the Google Cloud Machine Learning Platform
	* Sentiment analysis
	* Fraud detection
	* Content personalization
* Which statements are true about BigQuery? Choose all that are true
	* BigQuery is a good choice for data analytics warehousing.
	* BigQuery lets you run fast SQL queries against large databases.
* Name three use cases for Cloud Pub/Sub
	* Analyzing stream data
	* IoT applications
	* Decoupling systems
* What is TensorFlow?
	* An open-source software library that’s useful for building machine learning applications
* What does the Cloud Natural Language API do?
	* It analyzes text to reveal its structure and meaning.
	
## Resources

[Smart Analytics-Big Data](https://cloud.google.com/products/big-data/)

[Dataflow documentation](https://cloud.google.com/dataflow/docs/)

[BigQuery documentation](https://cloud.google.com/bigquery/docs/)

[Cloud Pub/Sub](https://cloud.google.com/pubsub/)

[Cloud Datalab](https://cloud.google.com/datalab/)

[AI ve makine öğrenimi ürünleri](https://cloud.google.com/products/ai/)

[Vision AI](https://cloud.google.com/vision/)

[Cloud Speech-to-Text](https://cloud.google.com/speech-to-text/)

[Natural Language](https://cloud.google.com/natural-language/)

[Translate](https://cloud.google.com/translate/)

[Video AI](https://cloud.google.com/video-intelligence/)

[Google Cloud Platform](https://cloud.google.com/products/#big-data)
