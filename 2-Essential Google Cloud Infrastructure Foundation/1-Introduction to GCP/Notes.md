## 1. Module Overview

* We will be covering virtual networks. GCP uses a software-defined network that is built on a global fiber infrastructure. This infrastructure makes GCP one of the world's largest and fastest networks. Thinking about resources as services instead of as hardware, will help you understand the options that are available and their behavior.
* In this module, we start by introducing virtual private cloud or VPC, which is Google's managed networking functionality for your cloud platform resources. Then we dissect networking into its fundamental components which are projects, networks, subnetworks, IP addresses, routes and firewall rules, along with network pricing.
* Next, you will explore GCP's network structure in a lab by creating networks of many different varieties and exploring the network of relationships between them
* On a high level, GCP consists of regions, points of presence or PoPs, a global private network, and services. A region is a specific geographical location where you can run your resources. The number on each region represents the zones within that region.
* The PoPs are where Google's network is connected to the rest of the Internet. GCP can bring its traffic closer to its peers because it operates an extensive global network of interconnection points.
* This reduces costs and provides users with a they better experience. The network connects regions and PoPs and it's composed of a global network of fiber optic cables with several submarine cable investments.

## 2. Using GCP

* Four ways you can interact with GCP. There's the Google Cloud Platform console or GCP console, Cloud Shell and the Cloud SDK, the APIs and the Cloud mobile app.
* The GCP console provides a web-based graphical User Interface that you access through console. If you prefer to work in a terminal window, the Cloud SDK provides the gcloud command line tool.
* GCP, also provides Cloud Shell which is a browser-based interactive shell environment for GCP that you can access from the GCP console. Cloud Shell is a temporary Virtual Machine with five gigabytes of persistent disk storage that has the Cloud SDK pre-installed.
* GCP Client Libraries expose APIs for two main purposes. App APIs provide access to services, and they're optimized for supported languages such as Node. js or Python. Admin APIs offer functionality for resource management. The Cloud mobile app is another way to interact with GCP.

## 3. Console and Cloud Shell

* You become familiar with the Google Cloud web-based interface. There are two integrated environments: a GUI (graphical user interface) environment called the Cloud Console, and a CLI (command-line interface) called Cloud Shell.
* The Cloud Console is under continuous development, so occasionally the graphical layout changes. This is most often to accommodate new Google Cloud features or changes in the technology, resulting in a slightly different workflow.
* You can perform most common Google Cloud actions in the Cloud Console, but not all actions. In particular, very new technologies or sometimes detailed API or command options are not implemented (or not yet implemented) in the Cloud Console. In these cases, the command line or the API is the best alternative.
* The Cloud Console is extremely fast for some activities. The Cloud Console can perform multiple actions on your behalf that might require many CLI commands. It can also perform repetitive actions. In a few clicks you can accomplish activities that would require a great deal of typing and would be prone to typing errors.
* The Cloud Console is able to reduce errors by only offering up through its menus valid options. It is able to leverage access to the platform "behind the scenes" through the SDK to validate configuration before submitting changes. A command line can't do this kind of dynamic validation
* Cloud shell provides the following:
	* Temporary Compute Engine VM
	* Command-line access to the instance via a browser
	* 5 GB of persistent disk storage ($HOME dir)
	* Pre-installed Cloud SDK and other tools
	* gcloud: for working with Google Compute Engine and many Google Cloud services
	* gsutil: for working with Cloud Storage
	* kubectl: for working with Google Container Engine and Kubernetes
	* bq: for working with BigQuery
	* Language support for Java, Go, Python, Node.js, PHP, and Ruby
	* Web preview functionality
	* Built-in authorization for access to resources and instances
* The Console:
	* Provides a fast way to get things done
	* Presents options to you, instead of requiring you to know them
	* Performs behind-the-scenes validation before submitting the commands
* Cloud Shell provides:
	* Detailed control
	* Complete range of options and features
	* A path to automation through scripting

## 4. Infastructure Preview

* Google Cloud Marketplace lets you quickly deploy functional software packages by providing pre-defined templates with which Google Cloud service?
	* Deployment Manager


## QuizNotes

 
	
## Resources


