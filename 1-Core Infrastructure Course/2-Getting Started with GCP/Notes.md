## 1. Module introduction

* When you run your workloads in GCP, you use projects to organize them. You use Google Cloud Identity, and Access Management, also called IM, or IAM to control who can do what.
* GCP customers use IM to implement least privilege. There are four ways to interact with GCP's management layer: through the web-based console, through the SDK and its command-line tools, through the APIs, and through a mobile app.

## 2. The Google Cloud Platform resource hierarchy

* All the resources you use, whether they're virtual machines, cloud storage buckets, tables and big query or anything else in GCP are organized into projects. 
* All the resources you use, whether they're virtual machines, cloud storage buckets, tables and big query or anything else in GCP are organized into projects. 
* policies are inherited downwards in the hierarchy.
* Each project is a separate compartment and each resource belongs to exactly one. Projects can have different owners and users.
* Folders let teams have the ability to delegate administrative rights, so they can work independently. The resources in a folder inherit IAM policies from the folder.
* Resources inherit the policies of their parent resource. if you set a policy at the organization level, it is automatically inherited by all its children projects. And this inheritance is transitive.
* The policies implemented at a higher level in this hierarchy can't take away access that's granted at a lower level.
* 
* Services and APIs are enabled on a per-project basis.
* Google don't manages every aspect of Google Cloud Platform customers' security. Google Cloud Platform manages the lower layers of the security stack, such as physical security, and gives customers tools for managing the higher layers.

## 3. Identity and Access Management (IAM)

* IAM lets administrators authorize who can take action on specific resources. An IAM policy has a "who" part, a "can do what" part, and an "on which resource" part.
* The "who" part names the user or users you're talking about. The "who" part of an IAM policy can be defined either by a Google account, a Google group, a Service account, an entire G Suite, or a Cloud Identity domain.
* The "can do what" part is defined by an IAM role. An IAM role is a collection of permissions. Most of the time, to do any meaningful operations, you need more than one permission.
* to manage instances in a project, you need to create, delete, start, stop, and change an instance. So the permissions are grouped together into a role that makes them easier to manage.
* There are three kinds of roles in Cloud IAM.
	* Primitive roles are broad. You apply them to a GCP project and they affect all resources in that project. These are the owner, editor, and viewer roles.
		* If you're a viewer on a given resource, you can examine it but not change its state.
		* If you're an editor, you can do everything a viewer can do, plus change its state.
		* if you are an owner, you can do everything an editor can do, plus manage roles and permissions on the resource.
		* The owner role on a project also lets you do one more thing: set up billing. 
		* Often, companies want someone to be able to control the billing for a project without the right to change the resources in the project. And that's why you can grant someone the billing administrator role.
	* GCP IAM provides a finer grained types of roles. GCP services offer their own sets of predefined roles and they define where those roles can be applied. 
	* Compute Engine, which offers virtual machines as a service. Compute Engine offers a set of predefined roles, and you can apply them to Compute Engine resources in a given project, a given folder, or in an entire organization.
* GCP resources are always organized into projects, regardless of whether you have an (optional) organization node.
* Organization nodes let you apply policies centrally. Organization nodes are optional, but if you want to define policies that apply to all the projects in your organization, having one is mandatory.
* Organization nodes are optional, but you must have one if you want to define folders.
* Folders require an organization node. Organization nodes are optional, but if you want to create folders, having one is mandatory.

## 4. IAM roles

* Compute Engines InstanceAdmin Role lets whoever has that role perform a certain set of actions on virtual machines. The actions are: listing them, reading and changing their configurations, and starting and stopping them.
* A lot of companies have a least-privileged model in which each person in your organization has the minimum amount of privilege needed to do his or her job.
* define an InstanceOperator Role to allow some users to start and stop Compute Engine and virtual machines, but not reconfigure them. Custom roles allow me to do that. 
* A couple cautions about custom roles. First, you have to decide to use custom roles. You'll need to manage their permissions. Some companies decide they'd rather stick with the predefined roles. Second, custom roles can only be used at the project or organization levels. They can't be used at the folder level.
* you'd create a service account to authenticate your VM to cloud storage. Service accounts are named with an email address. But instead of passwords, they use cryptographic keys to access resources.
* Fortunately, in addition to being an identity, a service account is also a resource. So it can have IAM policies on its own attached to it.
* You can also change the permissions of the service accounts without having to recreate the VMs.

## 5. Interacting with Google Cloud Platform

* four ways you can interact with Google Cloud Platform: the Console, the SDK and Cloud Shell, the Mobile App and the APIs.

## 6. Cloud Marketplace (formerly Cloud Launcher)

* Say you want a quick way to get started with GCP with minimal effort. That's what Google Cloud Launcher provides. It's a tool for quickly deploying functional software packages on Google Cloud Platform. There's no need to manually configure the software, virtual machine instances, storage or network settings.

## 7. Demonstration: Getting Started with Cloud Launcher

## 8. Getting Started with Google Cloud and Qwiklabs

* Qwiklabs allows you to get practical hands-on experience with Google Cloud, and proficiency with Google account credentials, so that you can access the Cloud Console at no cost.

## 9. QuizNotes

* Policies are a union of those applied on resource itself and those inherited from higher levels in the hierarchy. If a parent policy is less restrictive, it overrides a more restrictive policy applied on the resource. If a parent policy is more restrictive, it does not override a less restrictive policy applied on the resource. Therefore, access granted at a higher level in the hierarchy cannot be taken away by policies applied at a lower level in the hierarchy.
* All Google Cloud Platform resources are associated with a project.
* Service accounts are used to provide
	* Authentication between Google Cloud Platform services
	* A way to allow users to act with service account permissions
	* A way to restrict the actions a resource (such as a VM) can perform
* GCP customers and Google Cloud Platform divide responsibility for security
	* Google takes care of the lower parts of the stack, and customers are responsible for the higher parts.
* The Project ID globally unique, permanent, and unchangeable, but chosen by the customer
* Consider a single hierarchy of GCP resources.
	* There is an organization node, and there are no folders.
	* There is an organization node, and there is at least one folder.
	* There is no organization node, and there are no folders.
* difference between IAM primitive roles and IAM predefined roles
	* Primitive roles affect all resources in a GCP project. Predefined roles apply to a particular service in a project.
* billing for solutions deployed using Cloud Marketplace (formerly known as Cloud Launcher)
	* You pay only for the underlying GCP resources you use, with the possible addition of extra fees for commercially licensed software.


## Resources

[Resource Hierarchy](https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy)

[Cloud Identity and Access Management (IAM)](https://cloud.google.com/iam/)

[Understanding roles](https://cloud.google.com/iam/docs/understanding-roles)

[Cloud Console](https://cloud.google.com/cloud-console/)

[Google Cloud SDK documentation](https://cloud.google.com/sdk/docs/)

[Google Cloud Shell documentation](https://cloud.google.com/shell/docs/)

[Cloud APIs](https://cloud.google.com/apis/)

[Cloud Console Mobil Uygulaması](https://cloud.google.com/console-app/)

[What is Google Cloud Marketplace?](https://cloud.google.com/marketplace/docs)






