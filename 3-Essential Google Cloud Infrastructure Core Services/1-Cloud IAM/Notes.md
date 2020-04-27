## 1. Module Overview

* Cloud IAM is a sophisticated system built on top of email-like address names, job type roles in granular permissions.
* I will start by introducing Cloud IAM from a high-level perspective. We will then dive into each of the components within Cloud IAM which are organizations, roles, members and service accounts. 

## 2. Cloud IAM

* So what is identity access management? It is a way of identifying who can do what, on which resource. The who can be a person, group, or application. The what refers to specific privileges or actions, and the resource could be any GCP service.
* Google Cloud Platform resources are organized hierarchically as shown in this tree structure. The organization node is the root node in this hierarchy. Folders are the children of the organization. Projects are the children of the folders, and the individual resources are the children of projects. Each resource has exactly one parent.
* Cloud IAM allows you to set policies at all of these levels. Where a policy contains a set of roles, and role members. Let me go through each of the levels from top to bottom, because resources inherit policies from their parent.
* The organization resource represents your company. Cloud IAM roles granted at this level are inherited by all resources under the organization. The folder resource could represent your department. Cloud IAM roles granted at this level are inherited by all resources that the folder contains.
* Projects represent a trust boundary within your company. Services within the same project have a default level of trust. 
* The Cloud IAM policy hierarchy always follows the same path as the GCP resource hierarchy, which means that if you change the resource hierarchy the policy hierarchy also changes. For example, moving a project into a different organization will update the projects Cloud IAM policy to inherit from the new organizations Cloud IAM policy.
* child policies cannot restrict access granted at the parent level. For example, if I grant you that editor role for department X, and I grant you the viewer role at the Bookshelf project level, you still have the editor role for that project. Therefore, it is a best practice to follow the principle of least privilege. The principle applies to identities, roles, and resources. Always select the smallest scope that's necessary for the task in order to reduce your exposure to risk. 

## 3. Organization

* the organization resource is the root node in the GCP resource hierarchy. This node has many roles like the organization admin. The organization admin provides a user like Bob with access to administer all resources belonging to his organization, which is useful for auditing.
* here is also a project creator role, which allows a user like Alice to create projects within her organization. I am showing the project creator role here because it can also be applied at the organization level which would then be inherited by all the projects within the organization.
* The organization resource is closely associated with a G Suite or Cloud Identity account. When a user with a G Suite or Cloud Identity account creates a GCP project, an organization resource is automatically provisioned for them. Then Google Cloud communicates its availability to the G Suite or Cloud Identity super admins. These super admin accounts should be used very carefully because they have a lot of control over your organization and all the resources underneath it. 
* The G Suite or Cloud Identity super administrators and the GCP organization admin are key roles during the setup process and for lifecycle control for the organization resource. The two roles are generally assigned to different users or groups, although this depends on the organization's structure and needs.
* In the context of GCP organization setup, the G Suite or Cloud Identity super administrator responsibilities are; assign the organization admin role to some users, be a point of contact in case of recovery issues, control the lifecycle of the G Suite or Cloud Identity account and organization resource. 
* The responsibilities of the organization admin role are; define IAM policies, determined the structure of the resource hierarchy, delegate responsibility over critical components such as networking, billing, and resource hierarchy through IAM roles. Following the principle of least privilege, this role does not include the permission to perform other actions such as creating folders. To get these permissions, an organization admin must assign additional roles to their account for. 
* Folders can be viewed as sub organizations within the organization. Folders provide an additional grouping mechanism and isolation boundary between projects. Folders can be used to model different legal entities, departments, and teams within a company. 
* For example, a first level of folders can be used to represent the main departments in your organization like departments X and Y. Because folders can contain projects and other folders, each folder could then include other sub folders to represent different teams like teams A and B. Each team folder could contain additional sub folders to represent different applications like products 1 and 2. Folders allow delegation of administration rights
* each head of a department can be granted full ownership of all GCP resources that belong to their department. Similarly, access to resources can be limited by folder. So users in one department can only access and create GCP resources within that folder. Let's look at some other resource manager roles while remembering that policies are inherited from top to bottom.
* The organization node also has a viewer role that grants view access to all resources within an organization. The folder node has multiple roles that mimic the organizational roles but are applied to resources within a folder.
* There is an Admin role that provides full control over folders, a creator role to browse the hierarchy and create folders, and a viewer role to view folders and projects below a resource. 
* Similarly, for projects, there is a creator role that allows a user to create new projects making that user automatically the owner. There is also a project deleter role that grants deletion privileges for projects.

## 4. Roles

* There are three types of roles in Cloud IAM; Primitive roles, predefined roles, and custom roles. 
* Primitive roles are the original roles that were available in the GCP console, but they are broad. You apply them to a GCP project and they affect all resources in that project. In other words, IAM primitive roles are for fixed, coarse-grained levels of access.
* The permanent roles are the owner, editor, and viewer roles. The owner has full administrative access. This includes the ability to add and remove members and delete projects. The editor role has modify and delete access. This allows a developer to deploy applications and modify it or configure its resources. The viewer role has read only access. All of these roles are concentric. 
* That is, the owner role includes the permissions of the editor role, and the editor role includes the permissions of the viewer role. There is also a billing administrator role to manage billing an add or remove administrators without the right to change the resources in the project.
* Each project can have multiple owners, editors, viewers, and billing administrators. GCP services offer their own set of predefined roles and they define where those roles can be applied.
* This provides members with granular access to specific GCP resources and prevents unwanted access to other resources. These roles are collections of permissions because to do any meaningful operations, you usually need more than one permission. For example, as shown here a group of users is granted the instance admin role on Project A. This provides the users of that group with all the Compute Engine permissions listed on the right and more. Grouping these permissions into a role makes them easier to manage.
* The permissions themselves are classes and methods in the APIs. For example, compute.instances.start can be broken down into the service, resource, and verb. That means that this permission is used to start and stop Compute Engine instance. These permissions usually align with the actions corresponding REST API. 
* Compute Engine has several predefined IAM roles. Let's look at three of those. The Compute Admin role provides full control of all Compute Engine resources. This includes all permissions that start with Compute which means that every action for any type of Compute Engine resource is permitted. 
* The Network Admin role contains permissions to create, modify, and delete networking resources except for firewall rules and SSL certificates. In other words, the network admin role allows read-only access to firewall rules, SSL certificates, and instances to view their ephemeral IP addresses. 
* The Storage Admin role contains permissions to create, modify, and delete disks, images and snapshots. Or example, if your company has someone who manages project images and you don't want them to have the editor role on the project, grant their account the Storage Admin role on the project. 
* Now, roles are meant to represent abstract functions and are customized to align with real jobs. But what if one of those roles does not have enough permissions or you need something even finer-grained?
* That's what Custom Roles permit. A lot of companies use the least privileged model in which each person in your organization is given the minimal amount of privilege needed to do their job. 
* Let's say you want to define an instance operator role to allow some users to start and stop Compute Engine virtual machines, but not reconfigure them. Custom Roles allow you to do that.

## 5. Members

* 

## QuizNotes

* 
	
## Resources

[Creating and Managing Organizations](https://cloud.google.com/resource-manager/docs/creating-managing-organization#adding_an_organization_admin)

[Compute Engine IAM roles](https://cloud.google.com/compute/docs/access/iam#iam_roles])
