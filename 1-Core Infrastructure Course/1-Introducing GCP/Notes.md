## 1. GCP offers four main kinds of services

* Compute
* Storage
* Big Data
* Machine Learning

## 2. Cloud Computing Services

* The cloud provider has a pool of resources and lets you use more or less on demand.
* Cloud computing resources are available on-demand and self-service. (An exception: cloud computing providers typically set some limits on the amount of resources a customer can consume by default, to help customers avoid accidental runaway resource usage and charges. These limits can be raised by the cloud provider.)

## 3. GCP computing architectures

* Virtualized data centers brought you Infrastructure as a Service, IaaS, and Platform as a Service, PaaS offerings. 
* IaaS offerings provide raw compute, storage, and network organized in ways that are familiar from data centers. 
* PaaS offerings, on the other hand, bind application code you write to libraries that give access to the infrastructure your application needs. 
* Google's popular applications like, Search, Gmail, Docs and Drive are Software as a Service applications in that they're consumed directly over the internet by end users.

## 4. The Google network

* It's designed to give its users the highest possible throughput and the lowest possible latencies for their applications.	
* The network interconnects at more than 90 Internet exchanges and more than 100 points of presence worldwide.
* When an Internet user sends traffic to a Google resource, Google responds to the user's request from an edge network location that will provide the lowest latency. Google's Edge-caching network cites content close to end users to minimize latency.

## 5. GCP regions and zones

* A zone is a deployment area for Google Cloud Platform Resources.
* A zone doesn't always correspond to a single physical building.
* Zones are grouped into regions, independent geographic areas.
* All the zones within a region have fast network connectivity among them. Locations within regions usually have round trip network latencies of under five milliseconds.
* Think of a zone as a single failure domain within a region. As part of building a fault tolerant application, you can spread their resources across multiple zones in a region. That helps protect against unexpected failures.
* As part of building a fault-tolerant application, you can spread your resources across multiple zones in a region.

## 6. Multi-layered security approach

* Both the server boards and the networking equipment in Google data centers are custom designed by Google. Google also designs custom chips, including a hardware security chip called Titan that's currently being deployed on both servers and peripherals.
* Google's infrastructure provides cryptographic privacy and integrity for remote procedure called data-on-the-network, which is how Google services communicate with each other.
* Google Central Identity Service, which usually manifests to end users as the Google log-in page, goes beyond asking for a simple username and password.
* Users can also use second factors when signing in, including devices based on the universal second factor U2F open standard.
* Google services that want to make themselves available on the Internet register themselves with an infrastructure service called the Google Front End, which checks incoming network connections for correct certificates and best practices. 
* Google also has multi-tier, multi-layer denial of service protections that further reduce the risk of any denial of service impact. 

## Resources

[The NIST Definition of Cloud Computing](https://www.nist.gov/publications/nist-definition-cloud-computing)

[Google Cloud'da Uygulama Barındırma](https://cloud.google.com/hosting-options)

[Expanding our global infrastructure with new regions and subsea cables](https://blog.google/topics/google-cloud/expanding-our-global-infrastructure-new-regions-and-subsea-cables/)

[Geography and regions](https://cloud.google.com/docs/geography-and-regions)

[Google Cloud Sürdürülebilirliği](https://cloud.google.com/sustainability)

[Daha az ödeyerek daha fazlasını yapın](https://cloud.google.com/pricing)

[Google Infrastructure Security Design Overview](https://cloud.google.com/security/infrastructure/design/)