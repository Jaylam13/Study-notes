# AZ-104 - Microsoft Azure Administrator

## Manage Azure identities and governance## 
### RBAC Roles### 
* Contributor
  - Full access to manage Azure resources
  - Cannot assign roles in Azure RBAC
* Owner
** Full access to manage Azure resources
** Can assign roles to other users in Azure RBAC
* Reader
** Can view resources but cannot make changes
* User Access Administrator
** Can manage user access to Azure resources
* There is a limit of 2000 custom roles per tenant
* devtest labs user role only lets you connect, start, restart and shutdown virtual machines in azure devtest labs.
* You can assign custom roles to users, groups, and service principals at management group, subscription, and resource group scopes.
* Custom roles can be shared between subscriptions that trust the same Microsoft Entra tenant. 
* There is a limit of 5,000 custom roles per tenant. (For Microsoft Azure operated by 21Vianet, the limit is 2,000 custom roles.) 
* Custom roles can be created using the Azure portal, Azure PowerShell, Azure CLI, or the REST API.

### Azure Policy### 
* Used to ensure Azure resources comply and conform to company standards/requirements.  An example of this would be to set a policy to state that only a certain size vm can be deplyed in to the subscription
* You create a poicy definition and under that conditions under which it is enforced along with an effect that takes place when these confitions are met

### Tags### 
* Each resource or resource group is limited to a max of 15 tag names/value pairs
* Tag names are limited to 512 characters and values limited to 256
* Storage account tag names are limited to 128 characters and values limited to 256 characters
* Virtual machines are limited to 2048 for all tag names and values
* Tags cannot contain special characters

### Resoruce groups### 
* When moving something from one resource group to another both resource groups are locked during the opertaion (write and delete operations are both locked until its finished)
* The location of a resource does not change during a resource group move even if the new resource group is in a different location
* To move a resource to another resource group the source and destination subscriptions must exist within the same Azure Active Directory tenant
* The destination subscription must be registered for the resource provider of the resource being moved when trying to move a resource to another resource group
* The account being used to move the resource must have these permissioned
** Microsoft.Resources/Subscriptions/ResourceGroups/MoveResources/Action
** Microsoft.Resources/Subscriptions/ResourceGroups/Write

### Azure AD### 
* Azure Active Directory Basic, Premium P1 and Premium P2 are not currently supported in China
** Azure AD Free
*** Basic user and group management functionality and on=prem directory sync
*** It offers basic reporting and single sign-on across Office 365, Microsoft Azure and many popular SaaS applications
** Azure AD Basic
*** All the free options 
*** Cloud centric application access as well as group based access management
*** Self service password reset for cloud apps
** Azure Active irectory Premium P1
*** Hybrid user access to both on-prem and cloud resources
*** Support for advanced administration tasks, such as:
**** Self service group management
**** Dynamic groups
**** Intergrates with Microsoft Identity Manager
**** Cloud write back capabilities
** Azure Active Directory Premium P2
*** Active Directory Identity Protection
*** Privileged Identity Management (PIM)
*** Just in time access
* Azure AD is NOT AD in the cloud
* Azure AD can do single sign on and intergration with other apps/services without having to setup a complicated ADFS setup.  It can use OAUTH2, SAMAL etc etc
* Azure AD will only talk to one Azure AD connect
* Azure AD does not speak Kerberos, NTLM or LDAP
* To prevent users from registering custom applications in the tenant, From Users setting, configure the App registrations settings.
* You can set expiration policy only for Office 365 groups in Azure Active directory
* To allow users to reset their AD DS password from the Azure portal:
** Run Azure AD Connect and select Password writeback.
** From Password reset in the Azure portal, configure the Authentication methods settings.

### Azure AD Domain Services### 
* Provides managed domain services such as:
** Domain join
** Group policy
** LDAP
** Kerberos/NTLM authentication
* The domain services are fully compatible with traditional on-prem active directory
* There is no need for deployment/management of domain controllers in the cloud
* The managed domain is a stand-alone domain, it is NOT an extension of the on-prem domain
* This is like te on prem Active Directory

### Privileged Access Management (PIM)### 
* Requires Azure AD P2
* Can right size permissions based on what is used and not used

### Locks### 
* Read only and delete locks still allow moves

### Dynamic Membership Rules for groups### 
* Dynamic group membership adds and removes group members automatically using membership rules based on member attributes.
* If a user or device satisfies a rule on a group, they're added as a member of that group. If they no longer satisfy the rule, they're removed. You can't manually add or remove a member of a dynamic group.
* You can create a dynamic group for devices or for users, but you can't create a rule that contains both users and devices.
* You can't create a device group based on the user attributes of the device owner. Device membership rules can reference only device attributes.

### Administrative units### 
* An administrative unit is a Microsoft Entra resource that can be a container for other Microsoft Entra resources. An administrative unit can contain only users, groups, or devices
* Administrative units restrict permissions in a role to any portion of your organization that you define. You could, for example, use administrative units to delegate the Helpdesk Administrator role to regional support specialists, so they can manage users only in the region that they support.
* Users can be members of multiple administrative units. For example, you might add users to administrative units by geography and division; Megan Bowen might be in the "Seattle" and "Marketing" administrative units.
* Administrative units can't be nested.
* Administrative units are currently not available in Microsoft Entra ID Governance.
* You need to be a Global Administrator or Privileged Role Administrator to create administrative units

## Implement and manage storage## 

### Azure blobs### 
* Provides object storage for the cloud
* Optimised to support massive amounts of unstructured data
* Unstructured data is data that does not fit a specific model e.g. text and binary data
* Typically used for images/videos , documents which could be used on websites.
* Also good for streaming videos/audio
* Storing of log files, archive or backup data
* Can be accessed using HTTP or HTTPS
* Can be accessed using Azture Storage, PowerShell, Azure CLI, JAJA, PHP, .NET
* The storage account creates a unique namespace that you use to access the data, like http://mystorage.blob.core.windows.net
* Containers in the blob storage are used to organise the blobs within the account (think of them like directories).  You can create a unlimited number of containers and a container can store an unlimited number of blobs
* Container names muust be lowercase
* Blobs are the files, so image001.jpg would be considered a blob
* There are 3 types of blobs that are supported:
** Block blobs
*** These can contain up to about 190.7TiB of text and dinary data
*** They are called block bloba as they can be managed individually
** Append blobs
*** Similar to block bloba however they are optimised for append operations
*** This makes append blobs a good choice for logging data from virtaul machines
** Page blobs
*** Used to storage random access files up to 8TiB in size
*** You would typically use page blobks to store VHD files which would serve as disks for Azure virtual machines
* LRS = Locally Redundant Storage.  3 Copies of the data but always within the same storage stamp which means all 3 copies will be in the same zone within the same region
* ZRS = Zone Redundant Storage.  3 Copies of the data but spread over the zones in a region
* GRS = Global Redundant Storage.  3 Copies of the data in the same storage stamp (so same zone, same region) then itsd Async replicated to the region pair in its same zone within its region
* GZRS = Global Zone Redundant Storage.  3 copies spread over the zones within its region then replicated to the region pair and copied to a single zone within a region
* On GRS and GZRS you can enable read access so it can be read on the other replicated side but not written to until its promoted
* Object replication can be used to replicate blobs between storage accounts. Before configuring object replication, you must enable blob versioning for both storage accounts, and you must enable the change feed for the source account.
* Azure import service supports blob and file storage
* Azure export supports blob
* Both azure active dir and shared access signatures is supported by blob
* Blobs cannot be backed up to service vaults
* Blockblobsstorage can only be used with premium performance kind
* ZRS currently supports standard general purpose v2, filestorage and blockblobs
* A timed-based retention policy or legal hold policies can be applied to block deletion. Immutability policies can be scoped to a blob version or to a container.

### Azure files### 
* Fully managed file share system available in the cloud
* You can access Azure files through SMB protocol
* You can mount file shares from Windows, Linux and MacOS machines that reside both on-prem and in the cloud
* You can cache file shares on Windows servers, using the Azure file sync service
* Azure File AD Authentication allows Azure file share permissions to be controlled through on-prem active directories
* You can create as many file shares as required
* You can use PowerShell, Azure CLI, Azure portal and storage explorer to create, mount and manage Azure File shares
* Azure file share names have to be lowercase letters, numbers and hyphens
* Shares can either be SMB or NFS, it cannot offer both at the same time
** If SMB it will be version 2.13.x
** If NFS it will be version 4.1
* Only shared access signature token supported by file storage
* Max size of an azure file resource file share is 5tb
* To enable large file support:
** Set-AzStorageAccount -ResourceGroupName RG1 -Name Storage1 -EnableLargeFileShare
* Premium file shares are hosted in a special purpose storage account kind called FileStorage account
* A Azure sync group must contain one cloud endpoint which represents an azure file share and one or more server endpoint

### Azure NetApp Files### 
* Shares can use both SMB and NFS at the same time unlike Azure files

### Azure queue storage### 
* Designed for storing large numbers of messages used in communications between the different components of the distributed application.  These messages can be accessed from anywhere in the world through authenticated calls via HTTP or HTTPS.
* Each queue message can be up to 64KB in size
* A typical queue can contain millions of messages
* A queue name must be lowercase letters, number or hyphens
* A queue URL will be as follows https://<storage_account>.queue.core.windows.net/<queue_name>

### Azure table storage### 
* This is intended for the storage of structured NoSQL data
* It offers a key/attribute store and a schema-less design
* Schema-less design allows you to more easily adapt data to the needs of your business or application
* You can have as many tables you need up to the limit of the storage itself
* Ideal for large amounts of data that does not contain complex joins, foreign keys or stored procedures.  Non relational.
* The URL to access it will be as follows https://<storage_account>.table.core.windows.net/<table>
* A table is just entities, it doesnt enforce a schema on these entities within it
* Entities are basically like a database ROW
* Each entity can be up to 1MB in size
* You can have up to 252 properties for each entity
* There are 3 system properties for each entity as well which are:
** A partition key
** A row key
** A timestamp
* Premium table experience is offered via Azure Cosmos DB which is a globally distributed database service

### Azure managed disks### 
* Block level storage volumes
* These are used to provide storage capabilities for virtual machines
* A managed disk is much like a disk that you would see in an on-prem server only virtualised
* Available disk types are ultra disks, premium SSD disks, standard SSD disks and standard HDD disks
* Azure backup supports disk sizes up to 32TB
* You can use direct upload to transfer local VHD files to Azure managed disks
* There are two stypes of encryption you can use with managed disks:
** Server-side encryption (SS)
*** This performed by the Azure storage service and is enabled by default for all managed disks
*** This provides encryption at rest for your data
*** This is also enabled by default for snapshots and images in regions where managed disks are available
** Azure disk encryption (ADE)
*** Enabled on the OS and data disks of the VM
*** On Windows vms disks are encrypted by BitLocker
*** On Linux vms disks are encrypted using DM-crypt
* There are 3 disk roles in Azure:
** Data
*** Manage disks attached to a vm, used to store applications and other data
*** When you attach the disk its registered as a SCSI drive
*** Data disks have a max capacity as 32TB
*** The number of managed disks you can attach to a vm depends on the size of the vm
** OS
*** Simply hosts the vms operating system and boot volume
*** Max capacity of an OS disk is 4TB
** Temp
*** Every vm contains a temp disk
*** Not a managed disk
*** Host page files, swap files
*** Data on these disks are lost in maint or if the vm is re deployed
*** Temp disks are given the D:
*** On Linux vms the temp disk is /dev/sdb/
* You can detach a disk from a running virtual machine (hot removal)

### Storage accounts### 
* A container that houses all of your storage data objects
* All storage is encrypted
* Virtual machines using Premium SSDs for ALL of their disks qualify for a 99.9% SLA
* Zone redundant storage and Geo zone redundant storage are only available for:
** General-Purpose V2
** Block Blob Storage
** File Storage
* To grant access to storage account ensure ip range is selected and selected networks from the networking blade of storage account

* Storage account types:
** General-Purpose V2
*** Basic account that can be used to host blobs, files, queues and tables
*** Microsoft recommends using this account for more scenarios
** General-Purpose V1
*** Can host blobs, files, queues and tables
*** Can do the same as V2 but Microsoft recommend using V2, this means this V1 is probably going to go away in the near future
** Block Blob Storage
*** Offers premium performance for block blobs and append blobs
*** Typically used for situations where high transaction rates are in play
*** Also good if the requirement is for low storage latency
** File Storage
*** Files only storage accounts
*** Feature high performance characteristics
*** Microsoft recommends using for enterprise applications or high-performing applications
** Blob Storage
*** A legacy account used for blob-storage only
*** Microsoft recommend instead of using blob storage accounts to use General-Purpose V2
***
* SAS= Shared Access Signature.  This gives access to resources in a storage account for a limited amount of time
* All storage accounts and encrypted at rest now
* Live migration of storage accounts is only supported for storage accounts that use LRS replication.  If it doesnt you will need to convert back to LRS before proceeding.
* Only standard account types support live migration, Premium accounts must be migrated manually
* Storage accounts:
** Kind = storagev2, storage or blobstorage
** SKU = standard_grs, lrs etc etc

### Azure Storage Tiers### 
* Hot:
** Frequently accessed data
** Storage costs are highest but access costs lowest
* Cool
** Infrequently accessed data
** Storage costs are lower but access costs are higher.  
** You must also leave data in here for 30 days, if you remove it before then you will be charged a "early removal penalty"
** Minimum storage duration 30 days
* Archive 
** For data that doesnt need to be accessed much like long term backups 
** Storage costs lowest but highest access costs.  
** To avoid early deletion penalty data must remain in this tier for 180 days.  
** You also cannot access data right away, its offline storage meaning the data has to be redydrated before you can get to it.  This process can take up to 15 hours.
** Minimum storage duration 180 days

### Life Cycle Management### 
This is used to move data between tiers.  An example would be to move data from hot to cool if it has not been accessed in XX days, then to move it from cool to achive if it then has not been access for another XX days.
* Life Cycle Management only works for General Purpose V2 accounts and blob storage accounts
* Life Cycle Management policies only run once a day, so it could take 24hrs from when you create the policy before anything happens
* A lifecycle management rule can be used to move or delete blobs automatically. The rule can be based on the time the blob was last modified or the time the blob was last accessed (read or write). To perform an action based on the access time, access tracking must be enabled. This can incur additional storage costs.

### Shared Access Signature### 
* You secure an account SAS by using a storage account key. When you create an account SAS, your client application must possess the account key.
* Possible values are both HTTPS and HTTP (https,http) or HTTPS only (https). The default value is https,http. Note that HTTP only isn't a permitted value.
* As of version 2015-04-05, Azure Storage supports creating a new type of shared access signature (SAS) at the level of the storage account. By creating an account SAS, you can:
** Delegate access to service-level operations that aren't currently available with a service-specific SAS, such as the Get/Set Service Properties and Get Service Stats operations.
** Delegate access to more than one service in a storage account at a time. For example, you can delegate access to resources in both Azure Blob Storage and Azure Files by using an account SAS.
** Delegate access to write and delete operations for containers, queues, tables, and file shares, which are not available with an object-specific SAS.
** Specify an IP address or a range of IP addresses from which to accept requests.
** Specify the HTTP protocol from which to accept requests (either HTTPS or HTTP/HTTPS).
** Stored access policies are currently not supported for an account SAS.

## Deploy and manage Azure compute resources## 
### Virtual Machines### 
* If a vm is using unmanaged disks a storage account will be required
* If the vm is using managed disks a storage account is not required
* Reserved instances can be 1 or 3 years, this can get you 72% cheaper than pay-as-you-go
* Spot pricing uses unused compute capacity, can be up to 90% cheaper than pay-as-you-go however these can be shutdown, rebooted etc at short notice by Azure when that unused compute is needed
** Virtual machine options
*** General purpose - Balanced CPU to MEM ratio
*** Compute optimized - High CPU to MEM ratio
*** Memory optimized - High MEM to core ratio
*** Storage optimized - High disk throughput and IO
*** GPU - Intended for heavy graphic and video rendering.  Has dedicated GPUs
*** High performance compute - Fastest and most powerfull CPU
* VM must be stopped to resize
* Deallocated vms still contribute to CPU counts when using quotas
* A public and a private IP address can be assigned to a single network interface
* Virutal machines in azure will resolve like vm.internal.cloudapp.net
* vms should use managed disks if you want to move them to an availability zone using site recovery

### Availability Sets### 
* When you deploy at least 2 machines in to an Availability set you qualify for a 99.95% uptime
* If you deploy a single vm in to an Availability set you still qualify for 99.95% uptime providing you use a premium SSD or ultra-disk for all the OS disks and data disks attached to the vm
* An Availability set contains 5 update domains by default, this can be increased to 20 in resource manager deployments
* An update domain is a group of hosts that can be updated and rebooted at the same time
* When updates or maint is performed by MS, only 1 update domain is rebooted at a time
* A fault domain is a group of hosts that share a common power source and network switch
* When virtual machines are added to a Availability set they are distributed across up to 3 different fault domains in a resource manage deplyment or across 2 domains in classic deployments
* Availability sets offer improved VM to VM latencies compared to availability zones
* Availability sets are still susceptible to certain shared infrastructure failures, like datacenter network failures, which can affect multiple fault domains
* When more than five virtual machines are configured within a single availability set with five update domains, the sixth virtual machine is placed into the same update domain as the first virtual machine, the seventh in the same update domain as the second virtual machine, and so on.
* A rebooted update domain is given 30 minutes to recover before maintenance is initiated on a different update domain.
* Only VMs with managed disks can be created in a managed availability set. The number of managed disk fault domains varies by region - either two or three managed disk fault domains per region.

###  Availability Zones### 
* When you deploy a vm to an availability zone they will be covered by a 99.99% uptime
* Availability zones offer the highest reliability since each VM is deployed in multiple datacenters, protecting you from loss of either power, networking, or cooling in an individual datacenter

###  Scale sets ### 
* A scale set it a group of identical virtual machines
* It can be configured to automatically increase or decrease the vms instances
* A load balancer is generally used to point to the scale set and distribute the worklod to the nodes in the scale set
* In a scale set all virtual machines os is all created from the one base config meaning you can update/manage the virtual machines in the scaleset easily
* A scale set with load balancer allows you to do layer 4 traffic rules
* A scale set with Azure Application Gateway allows you to do layer 7 traffic rules with SSL termination
* A scale set can support 1000 virtual machines if you use Azure images if you use your own or custom images then its 600
* You can use Azure Monitor For VMs to monitor the vms in the scale set and Application Insights to collection information and monitor the application
### Kubernetes### 
* The "Control Plane" is what manages the nodes and pods
* The standard way to perform authentication is Azure Active Directory
* You can manage Kubernetes using the kubectl command
* Min number of nodes recommended for a prod cluster is 3
### Autoscaling### 
* If two rules conflict, i.e CPU has reduced to scale down and IO is high so scale out.  Scale out aleways wins over scale in.
* Autoscaling uses Azure monitor for its metrics
### Bastion### 
* To use bastion you must have a AzureBastionSubnet created and an ipspace which is a /27 like 10.10.10.0/27
### Azure Container Instance### 
* An Azure container instance (Docker container) can mount Azure File Storage shares as directories and use them as persistent storage. 
* An Azure container instance cannot mount and use as persistent storage blob containers, queues and tables.
### Logic Apps### 
* The Logic app contributor roles lets you manage logic apps but not access to them.  it provides access to view, edit and update logic app.
### Application Service Plan### 
* You can move an app to another app service plan as long as the source plan and the target plan are in the same resource group and geographical region.
* The region in which your app runs is the region of the app service plan is in, however, you cannot change an app service plans region.
* App service plans must be running in a standard, premium or isolated tier in order to be enable multiple deployment slots, if not in this config you will need to scale up the app service plan.
* Scaling up allows for more CPU, memory, disk space and extra features like dedicated virtual machines, custom domains and certs, staging slots and autoscaling

## Configure and manage virtual networking## 
### Virtual Networks### 
* A vnet must have an address spaces that conforms to the RFC 1918 standard
* A vnet is scoped to a specific location and subscription
* A vnet can connect to another vnet using peering
* You should never create a subnet that encompasses the entire address space of the vnet network
* Fewer larger subnets is recommended over lots of smaller subnets
* It is recommended each subnet has a NSG on it so you can controller access to and from it
* Outbound communication to the inetnet is enabled by default
* VNET's can move resource groups
* You cannot just move a vm from vnet to vnet but what we can do is delete the vm but retain the disk, then re create the vm from the disk and attach a network card to the new network
* Before you can create a network interface you must first have a vnet, so the interface will need to be created in the same location as the vnet

### Application Security Groups### 
* You can logically group all the nics from several virtual machines and apply rules to them
* Running on vm you are limited to 30,000 security groups that can live in a subscription

### Network virtual appliance### 
* These can be a firewall or a WAN optimisation applicance 
### Route tables/BGP routes### 
* Route tables are custom tables that allow you to define custom routes that control how traffic is routed for each of your subnets
* BGP Routes are typically used to connect and Azure virtual network to an op-prem network via Express  Route or Azure VPN Gateway
### VPN Gateways### 
* You can only have 1 VPN Gateway per vnet but the gateway supports multiple connections to it, meaning you can connect multiple vnets to it
* When you deploy a vpn gateway 2 hidden vms are deployed and they are deployed to the vpn subnet you supplied when setting it up.  These vms contain routing tables and gateway services
* You can create a vnet to vnet vpn gateway, site to site or point to site
** Site to site vpn
*** Can be an ipsec or ike vpn tunnel
*** You must have a vpn gateway subnet on the vnet before creating the gateway
*** The local network gateway represents the on prem vpn device
*** Once the vpn gateway and local network gateway is configured you can creat a VPN Connection which links the two sites
*** Policy based only supported
** Point to site
*** Route based only supported
*** Protocols supported:
**** OpenVPN (SSL/TLS based) can be used through a firewall, can be used with Windows, Mac, Linux and Android
**** SSTP (TLS based) only supports Windows devices
**** IKEv2, can be used from MacOSX devices
*** Supported authentication:
**** Native Azure certificate authentication
**** Native Azure AD authenticated
**** Traditional Active Directory Domain Server
### Expressroute### 
* Can establish connectibity from:
** An any to any network
** A point to point ethernet network
** A virtual cross connection through a connectivity provider at a colocation facility
* Expressroute connections to NOT traverse the internet
* Dynamoc routing between your on prem network and microsoft via BGP
* Connection uptime SLA for Expressroute is 99.95%
* Expressroute can be used to access Azure and Office365 services
### Vnet Peering### 
* Vitual Network Peering
** Allows you to connect virtual networks that are in the same Azure regio
* Global Virtual Network Peering
** Allows you to connect virtual networks that are in different regions
* You cannot add address ranges to or delete address ranges from a virtual networks address space once a virtual network is peered with another virtual network.  To add or remove address ranges you need to break peering, add it then re peer

### Load Balancers### 
* Basic Load Balacner
** Supports 300 instances
** No availability zones supported
** Health probes TCP, HTTP
** Transport layer, IP and port to IP and port
** Can only point to Azure services
** Vms must be in same availibility or scale set

* Standard Load Balancer
** Supports 1000 instances
** Availability zones supported
** Health probes TCP, HTTP, HTTPS
** Can do outbound NAT
** 99.99% SLA
** Transport layer, IP and port to IP and port
** Can only point to Azure services
** Standard load balancer vms must be connected to the same virtual network
** A backend pool configured by IP address can only be done by a standard load balancer

* Azure Application Gateway
** Create rules based on host headers
** Route traffic to specific servers based on URL
** Used to load balance web traffic to web applications
** Application layer routing (layer 7)
** Can do SSL termination
** Autoscaling, auto scale up or down based on traffic load (only supported in standard v2)
** Web application firewall, protects against many common expliots, SQL injections, wordpress hacks etc
** Zone redundancy, standard v2 application gateway can span availability zones
** Application gateway must be deployed to an empty subnet
** You have host and protect up to 40 websites on a single instance of web application firewall on 1 application gateway
** Can point to Azure, non Azure cloud and on prem services

* Azure Front door
** Load balance applications and microservices
** Can failover over different regions and clouds
** Can ensure users of an application connect to the nearest point of presence to them
** Supports TLS termination
** Can point to Azure, non Azure cloud and on prem services

* Traffic manager
** DNS Specific load balancing solution
** Can point to Azure, non Azure cloud and on prem services

### Azure DNS### 
* Does not work across peered vnets
* Each DNS zone can be linked to up to 1000 vnets
* The Azure DNS Virtual Server IP address is 168.63.129.16
* txt and mx records can be used to verify domain

### Network Security Groups### 
* Priorty numbers are between 100-4096.  Rules with lower numbers are processed before those with higher numbers
* Protocols in NSG rules are TCP, UDP, ICMP or ANY

### Azure Firewall### 
* HA Built in
* Stateful
* Unrestricted cloud scalability
* Can work across subscriptions and networks
* Availability zone spanning

### Network Watcher### 
* IP Flow Verify - This tests if packets are allowed to flow between a vm and an endpoint.  It checks the NSG and tells you which rule either allows or denies the connection
* Next Hop - Enter the source and destination and it shows you the next hope.  Good for troubleshooting routing issues
* Connection Troubleshoot 
** This requires an extension installing on the vm that is having the connection problem.
** This give more information than Next Hop as it shows all the hops and latency

### Accelerated Networking### 
* Bypasses te Hyper-V switch stack and talks directly to the nic, this means less latency and increases performance.  Not all vms support it.

### Virtual WAN### 
* To connect a site to site using Azure virtual wan you must:
** Create a virtual wan resource
** Create a virtual hub
** Create vpn sites
** Connect the vpn sites to the hub

## Monitor and back up Azure resources## 

### Dashboard### 
* The maximum number of days for which data can be pinned as a chart on the dashboard is 14

### Azure Monitor### 
* Microsoft recommends registering these resource providers before you configure Azure Monitor
** Microsoft.insights
** Microsoft.AlertsManagement
* To monitor metrics of linux machine you use Linux Diagnotics Extension (LAD) 3.0
* A closed alert in Azure Monitor means an administrator manually changed the state of the alert.
* You must install the Microsoft Monitoring Agent on vms to monitor and dump data in Lod Analytics NOT the Microsoft Monitoring Agent VM extension

### Backup### 
* RPO (Recovery Point Objective) = How much can I loose?
* RTO (Recovery Time Objective) = How long until I have to be back up and running?
* The default retention period for virtual machines is 30 days
* "Allow trusted microsoft services to access this storage account" needs to be ticked to allow azure backup to access the storage

### Azure AD Logs### 
* Logs are kept for default as 7 days or 30 days if you have the Premium Azure AD P1 license

### Alerts### 
* A maximum of one SMS message can be sent every five minutes. Therefore, a maximum of 12 messages will be sent per hour.
* Voice no more than 1 voice call every 5 mins
* Email no more than 100 emails in an hour

### Azure Import/Export Service### 
* You can create two files to prepare the drives and these can be a "dataset csv file" and a "Driveset csv" file
* Azure import/export service is used to securly import large amounts of data to azure blob storage or azure files

## Misc## 
* If you want to run a Docker container as an Azure web service, you must configure the Publish option and select Docker container.
* If you want to deploy a Docker container as web app, the runtime stack option is unavailable.
* Continuous deployment is a strategy for software releases. This option is unavailable when you publish a Docker container as an Azure web app.
* An Azure container instance (Docker container) can mount Azure File Storage shares as directories and use them as persistent storage. 
* An Azure container instance cannot mount and use as persistent storage blob containers, queues and tables.
* The Cost blade allows you to optimize and reduce your overall Azure spending. You can use this to identify the virtual machines that are underutilized. 
* The Performance blade allows you to improve the speed of your applications. High availability is unavailable via Azure Advisor. Operational Excellence helps you achieve process and workflow efficiency, resource manageability, and deployment best practices.
* Kusto Query Language (KQL) is a powerful tool to explore your data and discover patterns, identify anomalies and outliers, create statistical modeling, and more. KQL is a simple yet powerful language to query structured, semi-structured, and unstructured data
* To access an Azure file share remotely you need to allow port 445. Port 5671 is used to send health information to Azure AD. It is recommended, but not required, in the latest versions. Port 80 is used to download certificate revocation lists (CRLs) to verify TLS/SSL certificates. Port 443 is used to sync with Azure AD.
* To enable Traffic analytics you must have one of the following roles.  Owner, Contributor, Network Contributor or Monitoring Contributor.
