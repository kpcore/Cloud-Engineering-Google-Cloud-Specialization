## 1. Module Overview

* GCP uses a software-defined network that is built on a global fiber infrastructure. This infrastructure makes GCP one of the world's largest and fastest networks. 
* Thinking about resources as services instead of as hardware, will help you understand the options that are available and their behavior.
* we start by introducing virtual private cloud or VPC, which is Google's managed networking functionality for your cloud platform resources. Then we dissect networking into its fundamental components which are projects, networks, subnetworks, IP addresses, routes and firewall rules, along with network pricing. 
* Next, you will explore GCP's network structure in a lab by creating networks of many different varieties and exploring the network of relationships between them. After that, we will look at common network designs. On a high level, GCP consists of regions, points of presence or PoPs, a global private network and services.
* A region is a specific geographical location where you can run your resources. Several regions that are currently operating as well as future regions. The number on each region represents the zones within that region.
* The PoPs are where Google's network is connected to the rest of the Internet. GCP can bring its traffic closer to its peers because it operates an extensive global network of interconnection points. This reduces costs and provides users with a they better experience.
* The network connects regions and PoPs and it's composed of a global network of fiber optic cables with several submarine cable investments.

## QuizNotes

*
	
## Resources

[Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/)

[Google's Netwoking Infastructure](https://peering.google.com/#/infrastructure)
