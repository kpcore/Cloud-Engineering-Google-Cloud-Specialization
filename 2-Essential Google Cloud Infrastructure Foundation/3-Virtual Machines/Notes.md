## 1. Module Overview

* VMs are the most common infrastructure component and then GCP there provided by Compute Engine. A VM is similar but not identical to a hardware computer. VMs consists of a virtual CPU, some amount of memory, disk storage, and an IP address. Compute Engine is GCP service to create VMS. It is very flexible and offers many options including some that can't exist in physical hardware. 
* we'll start with the basics of Compute Engine followed by a quick little lab to get you more familiar with creating virtual machine. Then, we'll look at the different CPU and memory options that enable you to create different configurations. Next, we'll look at images and the different disk options available with Compute Engine. After that, we will discuss very common Compute Engine actions that you might encounter in your day-to-day job. 

## 2. Compute Engine

* there is a spectrum of different options in GCP for compute and processing. We will focus on the traditional virtual machine instances. Now the difference is Compute Engine gives you the utmost inflexibility. Run whatever language you want, it's your virtual machine. This is purely an Infrastructure as a Service or IaaS model.
* You have a VM and an operating system and you can choose how to manage it and how to handle aspects such as autoscaling, where you'll configure the rules about adding more virtual machines in specific situations. 
* The primary work case of Compute Engine is any general workload, especially an enterprise application that was designed to run on a server infrastructure. This makes Compute Engine very portable and easy to run in the Cloud. Other services like Google Kubernetes Engine, which consist of containers workloads may not be as easily transferable as what you're used to find On-premises. 
* Both predefined and custom machine types allow you to choose how much memory and how much CPU you want. You chose the type of disk you want, what do you want to just use standard hard drives, SSDs, local SSDs, or a mix. You can even configure the networking interfaces and run a combination of Linux and Windows machines. Several different features will be covered throughout this module such as machine rightsizing, startup scripts, metadata, availability policies, and pressing, and usage discounts.
* On Compute Engine, each virtual CPU or vCPU is implemented as a single hardware hyper-thread on one of the available CPU platforms. 
* You have three options, standard, SSD, or local SSD. So basically, do you want the standard spinning hard disk drives or HDDs, or flash memory solid state drives SSDs. Both of these options provide the same amount of capacity in terms of disk size when choosing a persistent disk. Local SSDs have even higher throughput and lower latency than SSD persistent disks because they're attached to the physical hardware. However, the data that you store on local SSDs persists only until you stop or delete the instance. Typically, a local SSD is used as a swap disk just like you would do if you want to create a RAM disc.
* But if you need more capacity, you can store those on a local SSD. You can create instances with up to eight separate 375 gigabytes local SSD partitions for total of three terabytes of local SSD space for each instance. Standard and non-local SSD disks can be sized up to 64 terabytes for each instance.
* You'll also notice that you can do regional HTTPS load balancing and network load balancing. This doesn't require any pre-warming because a load balancer isn't a hardware device that needs to analyze your traffic. A load balancer is essentially a set of traffic engineering rules that are coming into the Google network. VPC is applying the rules destined for your IP address subnet range.

## 3. VM access and lifecycle

* For accessing a VM, the creator of an instance has four root privileges on that instance. 
* On a Linux instance, the creator has SSH capability and can use the GCP Console to grant SSH capability to other users. 
* On a Windows instance, the creator can use the GCP Console to generate a username and password. After that, anyone who knows the username and password can connect to the instance using a remote desktop protocol or RDP client.
* When you define all the properties of an instance, and click "Create" the instance enters the provisioning state. Here the resources such as CPU, memory, and disk are being reserved for the instance but the instance itself isn't running yet.
* Next, the instant moves to the staging state where resources have been acquired and the instance is prepared for launch. Specifically in this state Compute Engine is adding IP addresses, booting up the system image, and booting up the system. 
* After the instance starts running, it will go through pre-configured startup scripts and enable SSH or RDP access. Now, you can do several things while your instance is running. For example, you can live migrate your virtual machine to another host in the same zone instead of requiring your instance to be rebooted. This allows GCP to perform maintenance that is integral to keeping the infrastructure protected and reliable without interrupting any of your VMs.
* While you're instance is running, you can also move your VM to a different zone. Take a snapshot of the VMs persistent disk, export the system image or reconfigure metadata.
* Some actions require you to stop your virtual machine. For example, if you want to upgrade your machine by adding more CPU. When the instance enters this state, it will go through pre-configured shutdown scripts and end in the terminated state. 
* From this state, you can choose to either restart instance which would bring it back to its provision state or delete it. You also have the option to reset a VM which is similar to pressing the reset button on your computer. This action wipes the memory content of the machine and resets the virtual machine to its initial state. The instance remains in the running state throughout the reset. 
* There are different ways you can change a VM state from running. Some methods involve the GCP Console and the GCloud command while others are performed from the OS such as for a reboot and shut down. It's important to know that if you're restarting, rebooting, stopping, or even deleting an instance, the shutdown process will take about 90 seconds.
* For a preemptible VM, if the instance is not stopped after 30 seconds, Compute Engine sends an ACPI G3 mechanical off signal to the operating system. Remember that when writing shutdown scripts for preemptible VMs. As I mentioned previously, Compute Engine can live migrate your virtual machine to another host due to a maintenance event to prevent your applications from experiencing disruptions.
* The default maintenance behavior for instances is to live migrate, but you can change the behavior to terminate your instance during maintenance events instead. If your VM is terminated due to a crash or other maintenance event, your instance automatically restarts by default but this can also be changed.
* These availability policies can be configured both during the instance creation and while an instance is running by configuring the automatic restart and on host maintenance options.
* When a VM is terminated, you do not pay for memory and CPU resources. However, you are charged for any attached disks and reserved IP addresses. In the terminated state, you can perform any of the actions listed here such as changing the machine type, but you cannot change the image of a stopped VM.
* You can add network tags and allow specific network traffic from the internet through firewalls.
* Some properties of a VM are integral to the VM, are established when the VM is created, and cannot be changed. Other properties can be edited. You can add additional disks and you can also determine whether the boot disk is deleted when the instance is deleted. 
* Normally the boot disk defaults to being deleted automatically when the instance is deleted. But sometimes you will want to override this behavior. This feature is very important because you cannot create an image from a boot disk when it is attached to a running instance. So you would need to disable Delete boot disk when instance is deleted to enable creating a system image from the boot disk.
* You can't convert a non-preemptible instance into a preemptible one. This choice must be made at VM creation. A preemptible instance can be interrupted at any time and is available at a lower cost.
* If a VM is stopped for any reason, (for example an outage or a hardware failure) the automatic restart feature will start it back up. Is this the behavior you want? Are your applications idempotent (written to handle a second startup properly)?
* During host maintenance, the VM is set for live migration. However, you can have the VM terminated instead of migrated.
* RDP is the Remote Desktop Protocol. You would need the RDP client installed on your local machine to connect to the Windows desktop.

## 4. Compute options

* Speaking of CPU memory options, let's look at all the different machine types that are currently available. A machine type specifies a particular collection of virtual hardware resources available to a VM instance, including the system memory size, vCPU count, and maximum persistent disk capability.
*  GCP offers several machine types that can be grouped into two categories. Predefined machine types. These have fixed collection of resources, are managed by Compute Engine, and are available in multiple different classes. Each class has a predefined ratio of gigabytes of memory per Virtual CPU. These are the standard machine types, high memory, high CPU, memory optimized, Compute optimize, and shared-core machine types. 
* There also the custom machine types. These lets you specify the number of virtual CPUs, and the amount of memory for your instance. 
* Let's explore each of these Machine types. But remember that these Machine types and the available options can change. Standard machine types are suitable for tasks that have a balance of CPU and memory needs. Standard machine types have 3.75 gigabytes of memory per virtual CPU. The virtual CPU configurations come in different intervals from 1vCPU all the way to 96 vCPUs as shown on this table. Each of these machines supports a maximum of 128 persistent disks with a total persistent disk size of 64 terabytes, which is also the case for the high memory, high CPU, memory optimized, and compute optimized machine types.
* High memory machine types are ideal for tasks that require more memory relative to vCPUs. High memory machine types have 6.5 gigabytes of system memory per vCPU. Similar to the stent machine types, the vCPU configurations come in different intervals from 2vCPUs all the way to 96vCPUs, as shown on this table. High CPU machine types are ideal for tasks that require more vCPUs relative to memory. High CPU machine types have 0.9 gigabytes of memory per vCPU.
* Memory optimized machine types are ideal for tasks that require intensive use of memory with higher memory to vCPU ratios than high memory machine types. These machine types are perfectly suited for in-memory databases and in-memory analytics such as SAP HANA and business warehouse workloads, genomic analysis, and SQL Analysis Services. Memory optimized machine types have more than 14 gigabytes of memory per vCPU. These Machines come in four configurations as shown in this table, with only the n1-megamem-96 supporting a local SSD, as of this recording.
* Compute optimized machine types are ideal for compute intensive workloads. These machine types are for the highest performance per core on Compute Engine. Built on the latest generation Intel scalable processors, the casket lake, C2 machine types offer up to 3.8 gigahertz sustained all-core turbo, and provide full transparency into the architecture of the underlying server platforms, enabling advanced performance tuning. C2 machine types offer much more computing power, run on a newer platform, and are generally more robust for compute intensive workloads than the n1 high CPU machine types. 
* Shared-core machine types provide one virtual CPU that is allowed to run for a portion of the time on a single hardware hyper-thread on the host CPU running your instance. Shared-core instances can be more cost effective for running small non resource intensive applications than other machine types. There are only two shared-core machine types to choose from, they're the f1-micro and the g1-small. The f1-micro machine types offer bursting capabilities that allow instances to use additional physical CPU for short periods of time. Bursting happens automatically when your instance requires more physical CPU than you originally allocated. During these spikes, your instance will opportunistically take advantage of available physical CPU in bursts. Note that bursts are not permanent and are only possible periodically. 
* If none of the predefined machine types match your needs, you can independently specify the number of vCPUs and the amount of memory for your instance. Custom machine types are ideal for the following scenarios; when you have workloads that are not a good fit for the predefined machine types that are available to you, or when you have workloads that require more processing power or more memory but you don't need all of the upgrades that are provided by the next larger predefined machine type.
* It cost slightly more to use a custom machine type than equivalent predefined machine type. There are still some limitations in the amount of memory and vCPUs you can select. Only machine types with one virtual CPU or an even number of virtual CPUs can be created. 
* Memory must be between 0.9 gigabytes and 6.5 gigabytes per virtual CPU by default. The total memory of the instance must be a multiple of 256 megabytes. By default, a custom machine can have up to 6.5 gigabytes of memory per virtual CPU. However, this might not be enough memory for your workload. So at an additional cost, you can get more memory per virtual CPU beyond the 6.5 gigabytes limit. 

## 5. Compute Pricing

* GCP offers a variety of different options to keep the prices low for compute engine resources. All of these vCPUs, GPUs and gigabyte of memory are charged a minimum of one minute. For example if you've run your virtual machine for 30 seconds, you will bill it for one minute of usage. After one minute, instances are charged in one second increments.
* Compute Engine uses a resource-based pricing model where each virtual CPU and each gigabyte of memory on Compute Engine is built separately rather than as part of a single machine type. You still create instances using predefined machine types, but your bill reports them as individual vCPUs and memory used. 
* There are several discounts available but the disk on types cannot be combined. There are research-based pricing which allows Compute Engine to apply sustained use discounts to all of your predefined machine types usage in a region collectively rather than to individual machine types. 
* If you're workload is stable and predictable, you can purchase a specific amount of vCPU and memory for a discount off of normal prices in return for committing to a usage term of one or three years. The discount is up to 57 percent for most machine types or custom machine types. The discount is up to 70 percent for memory optimized machine types. 
* A preemptible VM is instance that you can create and run at much lower price than normal instances. However, Compute Engine might terminate or preempt these instances if it requires access to those resources for other tasks. Preemptible instances are access Compute Engine capacity, so their availability varies with usage. 
* The ability to customize the amount of memory in CPU through custom machine types allows for further pricing customization. Speaking of sizing your Machine, Compute Engine provides VM sizing recommendations to help you optimize the resource use of your virtual machine instances. When you create a new instance, recommendations for the new instance will appear 24 hours after the instance has been created.
* Sustained use discounts are automatic discounts that you get for running specific Compute Engine resources, be it CPUs, memory, and GPU devices for a significant portion of the billing month.
* The discount increases with usage, and you can get up to 30 percent net discount for instances that run the entire month. 
* To take advantage of the full 30 percent discount, create your VM instances on the first day of the month because discounts reset at the beginning of each month. 
* you have two instances that are in the same region but have different machine types, and run at different times of the month. Compute Engine breaks down the number of vCPUs and amount of memory used across all instances that use predefined machine types, and combines the resources to qualify for the largest sustained usage discounts possible.

## 6. Special compute configurations

* As I mentioned earlier a preemptible VM is an instance that you can create and run at much lower prices than normal instances. See whether you can make your application function completely on preemptible VMs, because an 80 percent discount is a significant investment in your application.
* these VMs might be preempted at any time, and there is no charge if that happens within the first 10 minutes. Also, preemptible VMs are only going to live for up to 24 hours, and you only get a 30-second notification before the machine is preempted. 
* It's also worth noting that there are no life migrations, no automatic resorts in preemptible VMs. But something that we will highlight is that you can actually create monitoring and load balances then can startup new preemptible VMs in case of a failure. there are external ways to keep restarting preemptible VMs if you need to. 
* One major use case of preemptible VMs is running a batch processing job. If some of those instances terminate during processing, the job slows down but does not completely stop. Therefore preemptible instances complete your batch processing tasks without placing additional workload on your existing instances and without requiring you to pay full price for additional normal instances.
* If you have workloads that require physical isolation from other workloads, or virtual machines in order to meet compliance requirements, you want to consider sole-tenant nodes. A sole-tenant node is a physical Compute Engine server that is dedicated to hosting VM instances only for your specific project. Use sole-tenant nodes to keep your instances physically separated from instances in other projects, or to group your instances together in the same host hardware. 
* Also if you have existing operating system licenses, you can bring them to Compute Engine using sole-tenant nodes while minimizing Physical Core usage with the in-place restart feature. 
* Another Compute option is to create shielded VMs. Shielded VMs offer verifiable integrity of your VM instances. So you can be confident that you're instances haven't been compromised by boot or kernel level of malware or rootkits.
* Shielded VMs verifiable integrity is achieved through the use of secure boot, Virtual Trusted Platform Module or VTPM enabled measured boot and integrity monitoring. Shield VMs is the first offering in the shielded Cloud initiative. The shielded Cloud initiative is meant to provide an even more secure foundation for all of GCP by providing verifiable integrity, and offering features like VTPM shielding or ceiling that help prevent data exfiltration.

## 7. Images

* When creating a virtual machine, you can choose the boot disk image. This image includes the boot loader, the operating system, the file system structure, any pre-configured software, and any other customizations.
* Premium image prices vary with the machine type. However, these prices are global and do not vary by region or zone. 
* You can also use custom images. For example, you can create and use a custom image by pre installing software that's been authorized for your particular organization.
* You also have the option of importing images from your on-premises or workstation, or from another cloud provider. This is a no cost service that is as simple as installing an agent. You can also share custom images with anybody in your project or among other projects too.

## 8. Disk options

* Every single VM comes with a single root persistent disk because you're choosing a base image to have that loaded on. This image is bootable and that you can attach it to VM and boot from it.
* It's durable and that it can survive, if the VM terminates. To have a boot disks survive a VM deletion, you need to disable the delete boot disk when instance is deleted option in the instances properties.
* there are different types of disks. Let's explore these in more detail. The first is that we create, is what we call a persistent disk.
* That means it's going to be attached to the VM through the network interface. Even though it's persistent, it's not physically attached to the machine. The separation of disk and compute, allows a disk to survive if the VM terminates. You can also perform snapshots of these disks which are incremental backups. The choice between HDD and SSD disk comes down to cost and performance.
* Another cool feature of persistent disks, is that you can dynamically resize them, even while they are running and attached to a VM. You can also attach a disk in read only mode to multiple VMs. This allows you to share static data between multiple instances, which is cheaper than replicating your data to unique disks for individual instances.
* computer engine encrypts all data at rest. GCP handles and manages this encryption for you, without any additional actions on your part. However, if you wanted to control and manage this encryption yourself, you can either use Cloud key management service, to create and manage key encryption keys, which is known as customer managed encryption keys. Or you can create and manage your own key encryption keys known as customer supplied encryption keys.
* Now, local SSDs are different from persistent disks and that they're physically attached to the virtual machine. Therefore, these disk are ephemeral, but provide very high IOPS. For up to date numbers, I recommend referring to the documentation. Currently, you can attach up to eight local SSD disks with 375 gigabytes each, resulting in a total of three terabytes. Data on these disks will survive a reset, but not a VM stop or terminate. Because these disks can't be reattached to a different VM.
* You also have the option of using a RAM disk. You can simply use TM PFS if you want to store data in memory. This will be the fastest type of performance available if you need small data structures. I recommend a high memory virtual machine if you need to take advantage of such features, along with a persistent disk to backup the RAM disk data.
* Persistent disk can be rebooted and snapshotted, but local SSDs and RAM disks are ephemeral. 
* I recommend choosing a persistent HDD disk when you don't need performance but just need capacity. 
* If you have high-performance needs, start looking at the SSD options. 
* The persistent disk offer data redundancy because the data on each persistent disk is distributed across several physical disks. 
* Local SSDs provide even higher performance but without the data redundancy. 
* Finally, RAM disks are very volatile, but they provide the highest performance.
* Now, just as there is a limit on how many local SSDs you can attach to VM, there's also a limit on how many persistent disks you can attach to VM.
* this limit depends on the machine type. For the shared core machine type, you can attach up to 16 disks. For the standard high CPU memory optimized and compute-optimized machine types, you can attach up to 128 disks. So you can create massive amounts of capacity for a single host.
* That throughput also shares the same bandwidth with disk IO. So if you plan on having a large amount of disk IO throughput, you will also compete with any network egress or ingress throughput. So remember that, especially if you'll be increasing the number of drives attached to a virtual machine.
* There are many differences between a physical hard disk in a computer and a persistent disk, which is essentially a Virtual Network device. First of all, if you remember with normal computer hardware disks, you have to partition them. 
* Essentially, you have a drive and you're carving up a section for the operating system to get its own capacity. If you want to grow it, you have to repartition it and if you want to make changes you might even have to reformat. If you want redundancy, you might create a redundant disk array and if you want encryption, you need to encrypt files before writing them to the disk. 
* With Cloud persistent disks, things are very different because all that management is handled for you on the back-end. You can simply grow disks and resize a file system because disks are Virtual Network devices. 
* Redundancy and snapshots services are built-in and disks are automatically encrypted. You can even use your own keys and that will ensure that no party can get to the data except you.

## 9. Common Compute Engine actions

* Now that we have covered all the different compute image and disk options, let's look at some common actions that you can perform with Compute Engine. 
* Every VM instance stores its metadata on a metadata server. The metadata server is particularly useful in combination with startup and shutdown scripts because you can use the metadata server to programmatically get unique information about an instance without additional authorization. 
* For example, you can write a startup script that gets the metadata key value pair for an instance's external IP address and use that IP address new script to setup a database. Because the default metadata keys are the same on every instance, you can reuse your script without having to update it for each instance, this helps you create less brittle code for your applications. Storing and retrieving instance metadata is a very common Compute Engine action. I recommend storing these startup and shutdown scripts in Cloud Storage
* Another common action is to move an instance to a new zone. For example, you might do so for geographical reasons or because a zone is being deprecated. If you move your instance within the same region, you can automate the move by using the gcloud compute instances move command. If we move your instance to a different region, you need to manually do so by following the process outlined here. This involves making a snapshot of all persistent disks and creating new disks in the destination zone from that snapshot.
* Next, you create a new VM in the destination zone and attach the new persistent disks, assign a static IP, and update any references to the VM. Finally, you delete the original VM, its disks and the snapshot.
* Speaking of snapshots, let's take a closer look at these. Snapshots have many use cases. For example, they can be used to backup critical data into a durable storage solution to meet application, availability, and recovery requirements. These snapshots are stored in Cloud Storage, which is covered later. Snapshots can also be used to micro data between zones. I just discussed this when going over the manual process of moving an instance between two regions, but this can also be used to simply transfer data from one zone to another.
* For example, you might want to minimize latency by migrating data to a drive that can be locally attached in the zone where it is used. Which brings me to another snapshot use case of transferring data to a different disk type. For example, if you want to improve disk performance, you could use a snapshot to transfer data from a standard ECD persistent disk to a SSD persistent disk.
* Now that I've covered some of these snapshot use cases, let's explore the concept of a disk snapshot. First of all, this slide is titled persistent disk snapshots because snapshots are available only to persistent disks and not to local SSDs. Snapshots are different from public images and custom images which are used primarily to create instances or configure instance templates, in that snapshots are useful for periodic backup of the data on your persistent disks. 
* Snapshots are incremental and automatically compressed, so you can create regular snapshots on a persistent disk faster and at a much lower cost than if you regularly created a full image of the disk. As we saw with the previous examples, snapshots can be restored to a new persistent disk, allowing for a move to a new zone. 
* Another common Compute Engine action is to resize your persistent disk. The added benefit of increasing storage capacity is to improve I/O performance. This can be achieved while the disk is attached to a running VM without having to create a snapshot. Now, while you can grow disk and size, you can never shrink them. So keep this in mind.


## Review

* I recommend enrolling in the Essential Cloud Infrastructure: Core Services course, which enhances your study of architecting with Compute Engine. In that course, we start by talking about Cloud IAM, and you will administer Identity and Access Management for resources. Next, we’ll cover the different data storage services in GCP, and you will implement some of those services. Then, we’ll go over resource management, where you will manage and examine billing of GCP resources. Lastly, we’ll talk about resource monitoring, and you will monitor GCP resources using Stackdriver services. Here are the modules of the course:

	1. Cloud IAM
	2. Data Storage Services
	3. Resource Management
	4. Resource Monitoring


## QuizNotes

* 

## Resources

[CPU platforms](https://cloud.google.com/compute/docs/cpu-platforms)

[Managing SSH keys in metadata](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys)

[Creating Passwords for Windows Instances](https://cloud.google.com/compute/docs/instances/windows/creating-passwords-for-windows-instances)

[Live Migration](https://cloud.google.com/compute/docs/instances/live-migration)

[Connecting to instances](https://cloud.google.com/compute/docs/instances/connecting-to-instance#rdp)

[Google Cloud Ücretsiz Katmanı](https://cloud.google.com/free/docs/gcp-free-tier#always-free-usage-limits)

[Ağ fiyatlandırması](https://cloud.google.com/compute/network-pricing#ipaddress)

[Machine types](https://cloud.google.com/compute/docs/machine-types)

[Creating a VM Instance with a custom machine type](https://cloud.google.com/compute/docs/instances/creating-instance-with-custom-machine-type#extendedmemory)

[Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/#available)

[Provisioning VMs on sole-tenant nodes](https://cloud.google.com/compute/docs/nodes/create-nodes)

[Block storage performance](https://cloud.google.com/compute/docs/disks/performance)

[Creating persistent disk snapshots](https://cloud.google.com/compute/docs/disks/create-snapshots)


