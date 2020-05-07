## 1. Module Overview

* Now that we've covered several of the GCP services and features, it makes sense to talk about how to automate the deployment of GCP infrastructure. Calling the Cloud APIs from code is a powerful way to generate infrastructure. But writing code to create infrastructure also has some challenges.
* One issue is that the maintainability of the infrastructure depends directly on the quality of the software. For example, a program could have a dozen locations that call the Cloud APIs to create VMs. Fixing a problem with the definition of one VM would require first identifying which of the dozen calls actually created it. Standards software development best practices will apply and it's important to note that things could change rapidly requiring maintenance on your code.
* Clearly, another level of organization is needed. That's the purpose of deployment manager. Deployment manager uses a system of highly structured templates and configuration files to document the infrastructure in an easily readable and understandable format.
* Deployment manager conceals the actual Cloud API calls. So you don't need to write code and can focus on the definition of the infrastructure. In this module, we cover how to use deployment manager to automate the deployment of infrastructure, and how to use GCP marketplace to launch infrastructure solutions.
* You will use Deployment Manager or Terraform to deploy a VPC network, a firewall rule, and virtual machine instances in the lab of this module. I will also demonstrate how to launch infrastructure solutions using GCP marketplace. Let's start by talking about deployment manager.

## 2. Deployment Manager

* So far you've been creating GCP resources using the GCP Console and Cloud Shell. I recommend the GCP Console when you are new to using a service or if you prefer a UI. Cloud Shell works best when you are comfortable using a specific service and you want to quickly create resources using the command line.
* Deployment Manager takes this one step further. Deployment Manager is an infrastructure deployment service that automates the creation and management of GCP resources for you. You just specify all the resources needed for your application in a declarative format and deploy your configuration.
* This deployment can be repeated over and over with consistent results and you can delete a whole deployment with one command or click. The benefit of a declarative approach is that it allows you to specify what the configuration should be and let the system figure out the steps to take.
* Instead of deploying each resource separately, you specify the set of resources which compose the application or service, allowing you to focus on the application. Unlike Cloud Shell, Deployment Manager will deploy resources in parallel.
* You can even abstract parts of your configuration into individual building blocks or templates that can be used for other configurations. Deployment Manager uses the underlying APIs of each GCP service to deploy your resources.
* This enables you to deploy almost everything we have seen so far from instances, instance templates and groups to VPC networks, firewall rules, VPN tunnels, Cloud routers, and load balancers.
* Before you get into the lab, let me walk you through a quick example that shows how Deployment Manager can be used to set up an auto mode network with an HTTP firewall rule. I could put this whole deployment into one single configuration.
* However, it's useful to parameterize your configuration with templates. Specifically, we're going to create one template for the auto mode network and one for the firewall rule. Therefore, if we want to create either of these resources somewhere else later on, we can use those templates. Let's start with the auto mode network template which we can write in Jinja2 or Python.
* Now, each resource must contain a name, type, and properties. For the name, I'm using an invariant variable to get the name from the top-level configuration which makes this template more flexible. For the type, I'm defining the API for a VPC network which is compute.v1.network.
* You can find all supported types in the documentation or query them within Cloud Shell as you will explore in the upcoming lab. By definition, an auto mode network automatically creates a subnetwork in each region. Therefore, I am setting the auto-create subnetworks property to true.
* Next, let's write the template for the HTTP firewall rule. For the name, I'm again using an invariant variable to get the name from the top-level configuration. For the type, I'm defining the API for a firewall rule which is compute.v1.firewall.
* The properties section contains the network I want to apply this firewall rule to the source IP ranges, and the protocols, and ports that are allowed. Except for the source IP ranges, I'm defining these properties as template properties. I will provide the exact properties from the top-level configuration, which makes this firewall rule extremely flexible.
* Essentially, I can use this firewall rule template for any network and any protocol and port combination. Next, let's write the top-level configuration in YAML syntax. I start by importing the templates that I want to use in this configuration, which are autonetwork.jinja and firewall.jinja. 
* Then I define the auto mode network by giving it the name mynetwork and leveraging the auto network.jinja template. I could create more auto mode networks in this configuration with other names or simply reuse this template in other configurations later on.
* Now I define the firewall rule by giving it a name, leveraging the firewall.jinja template, referencing my network, and defining the IP protocol and port. I can easily add other ports such as 443 for HTTPS or 22 for SSH traffic. Using the self link reference for the network name ensures that the VPC network is created before the firewalled rule.
* This is very important because Deployment Manager creates all the resources in parallel unless you use references. You would get an error without the reference because you cannot create a firewall rule for a non-existing network.
* Now there are other infrastructure automation tools in addition to Deployment Manager that you can use in GCP. You can also use Terraform, CHEF, Puppet, Ansible, or Packer. All of these tools allow you to treat your infrastructure like software, which helps you decrease costs, reduce risk, and deploy faster by capturing infrastructure as code.
* You might recognize some of these tools because they work across many Cloud service providers. I recommend that you provision and manage resources on Google Cloud with the tools you already know. That's why in the upcoming lab, you'll have the choice of using Deployment Manager or Terraform to automate the deployment of Infrastructure.
* Deployment Manager is an infrastructure deployment service that automates the creation and management of Google Cloud resources. Write flexible template and configuration files and use them to create deployments that have a variety of Cloud Platform services, such as Cloud Storage, Compute Engine, and Cloud SQL, configured to work together.
* Terraform enables you to safely and predictably create, change, and improve infrastructure. It is an open-source tool that codifies APIs into declarative configuration files that can be shared among team members, treated as code, edited, reviewed, and versioned.

## 3. GCP Marketplace

* Let's learn a little more about GCP Marketplace. GCP marketplace lets you quickly deploy functional software packages that run on GCP. Essentially, GCP marketplace offers production grade solutions from third-party vendors who have already created their own deployment configurations based on Deployment Manager. 
* These solutions are built together with all of your projects GCP services. If you already have a license for a third party service, you might be able to use a Bring Your Own License solution. You can deploy a software package now and scale that deployment later when your applications require additional capacity.
* GCP even updates the images of these software packages to fix critical issues and vulnerabilities but doesn't update software that you have already deployed. You even get direct access to partner support.

## QuizNotes

* What’s the benefit of writing templates for your Deployment Manager configuration?
	* Allows you to abstract part of your configuration into individual building blocks that you can reuse
		* After you create a template, you can reuse them across deployments as necessary. Similarly, if you find yourself rewriting configurations that share very similar properties, you can abstract the shared parts into templates.
* What does Google Cloud Platform Marketplace offer?
	* Production-grade solutions from third-party vendors who have already created their own deployment configurations based on Deployment Manager
		* Google Cloud Marketplace offers production-grade solutions from third-party vendors who have already created their own deployment configurations based on Deployment Manager.

## Resources

[Supported resource types](https://cloud.google.com/deployment-manager/docs/configuration/supported-resource-types)

[Google Cloud için IaC araçları](https://cloud.google.com/solutions/infrastructure-as-code/#cards)
