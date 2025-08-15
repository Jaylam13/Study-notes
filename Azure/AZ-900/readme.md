# AZ-900 - Microsoft Azure Fundermentals

### Storage
* Blob storage is a flat structure used for unstructured data (images, videos etc) and is normally used for large objects.
* Azure file storage and Azure Data Lake storage are hierarchical file storage similar to SMB shares, both of which you can do shares on
* Azure Queue Storage, A data store for queuing and reliably delivering messages between applications
* Azure Table Storage, Table storage is a server that stores non-relational structured data (also known as structured NoSQL data) in the cloud, providing a key/attribute store with schemaless design.
* LRS = Always 3 copies of the data but always in the same building
* ZRS = Always 3 copies of the data in the but in different zones
* GRS = Always 3 copies of the data, 3 in the primary region then 3 in another region
* GZRS = Always 3 copies of the data in the primary region over different zones then the same at the secondary region
* Premium only allows LRS and ZRS
* Azure File Sync allows you to sync on prem servers with an Azure share, the on prem servers never sync with each other, they all sync to the Azure share
* Azure File Sync you can add up to 100 on prem servers
* Azure Storage Explorer is a Windows app which allows you to browse Azure storage
* Azure Storage Browser is a Azure Portal that allows you to browse Azure storage.
* A storage account lives in a specific region
* A storage account comes in Std (general purpose v2) and prem (blobblocks, file shares, page blobs)
* Blob storage unstructured data types are adlgen2, hierarchical, page, page file storage)
* File storage types are smb/nfs shares
* Archive storage is offline, you will need to move the data to cold or hot to interact with it
* BLOB = Binary Large Object

### Connectivity/Networking 
* Azure Express route is more expensive than a site to site VPN
* You can also have a private connection to Azure via a Meet me
* Azure Express route does not traverse the internet, it's a private connection
* One vnet cannot talk to another vnet unless you create a vnet peer.  The peer can span regions and subscriptions.
* For a site to site vpn the "Local Network Gateway" is created in Azure but it refers to the IP address of the on prem router/VPN.  The "Virtual Network Gateway" is also created in Azure but this refers to the Azure side of the VPN
* By default all virtual machines get outbound traffic to the internet
* You can divide a vnet up in to subnets and configure routes between them
* If you want inbound traffic from the internet to a vm you must assign a public IP to the vm
* Azure Load Balancer, balances inbound and outbound connections to applications or service endpoints
* Azure Application Gateway, optimizes app server farm delivery whilst increasing application security
* Policy based VPN does not support point to point VPN
* You always lose 5 IP addresses when you create a submet, Azure uses these for gateways, dns etc
* Subnets/vnets cannot span subscriptions
* Azure Traffic Manager can create copies of a website around the world in different regions so it servers the customer from the closest one to them speeding up response and giving them a better experience.
* Outbound data transfer rates vary slightly based on the zone
* You can only have one local network gateway per vnet
* Point to point VPN only supports route based routing not policy based.
* You can configure access from vnet to vnet via NSG providing there is a peer
* The NSG needs to be in the same subscription and region of the subnet
* NSG is dest/soure, ip, port, protocol allow or deny
* WIth NSG you can create rules based on the service tags I.E Azure storage account as it has multiple IPs you could just use 1 tag
* You can apply a NSG to a subnet or a network interface but at the interface level its harder to manage.

### Subscriptions 
* One subscription can have a max of 980 resource groups
* One subscription can have a max of 50 tags
* A subscription is a collection of resources

### Azure Migrate 
Azure Migrate discovers on prem servers both physical and virtual and also both on Hyper-V and vmWare, it then assess the machine and tells you if its ready to migrate to Azure.

It will tell you how big the vm will be, how much it will cost and any other dependent servers that will also need to be migrated.

It will also help you migrate SQL Servers, WebApps, Desktops and data.

### Azure Container Instance 
Allows you to run a container with a single command.

### Azure Kubernetes 
* Allows you to run multiple containers which is known as a container orchestrator
* Azure Kubernetes Service, Cluster management for VMs that run containerized services.

### Azure Functions 
* This is a serverless event driven offering, allowing for individual functions to run and you only pay for it when it gets used.
* Azure Functions run off code so you will need to write code to create the function
* Azure Functions are stateless

### Billing 
* A billing account is an agreement between you and Mircosoft that you are using Azure Services.
* CAPEX - Purchasing something up front, this normally refers to an on prem solution
* OPPEX - Purchasing resources or services as we use it, this normally refers to a cloud offering
* Azure Cost Management allows for cost analysis, budgets, alerts and recommendations you must have a Enterprise agreement

### Regions 
* A region that supports availability zones has at least 3 datacenters, each datacenter is known as a zone.
* When viewing the Microsoft datacenter location map, if it has a diamond on it then that means it supports availability zones.
* All regions that support availability zones will see a min of 3 zones
* Zone redundant will distribute whatever you are deploying over zones automatically to ensure it is resilliant

### Cloudshell 
* Cloudshell supports both powershell and bash
* The first time you run CloudShell it will ask you for permission to create a storage account that the CloudShell vm can us

### Microsoft Defender For Cloud 
* Previously known as Azure Security Center

### Azure DataBox 
These are basically a box (nas box) that gets sent to you, you copy your data to it and send it back to Azure and they ingest it in to Azure.

The sizes are:
* Azure Data box Disk = 8tb
* Azure data box = 80tb
* Azure data box heavy = 770tb

### Management 
* Every tennant has a root management level, you can add 6 levels of groups under this
* Management groups help to manage groups of subscriptions
* Multiple subscriptions can be put in a management group

### Azure Monitor 
* Azure Monitor is a collection of monitoring tools to keep an eye on everything.
* You can create alert rules for example when storage is running low then you can use an Action Rule to do something like send an email or sms etc

### Azure Service Health 
* This is in the Portal under Help & Support.  It shows you health issues with Azure, upcoming maint work.  You can also setup alerts to notify you if there are issues with things that will affect things you are running.

### Azure Logic Apps 
* Low or no code required
* These do something based on a trigger.  So for example if a file is uploaded or a web request received it will do something.  No code is required for this, its a logic drag and drop interface.

### Availability Zones 
* When deploying a vm in to an availability zone ensure each vm is in a different zone number

### Azure Devops 
* Helps devops build, test, create environments.
* Azure Pipelines allows you to create continuous workflows to build, test and deploy code.
* Azure dev test labs allows you to spin up dev non prod environments, it allows admins to control costs by setting limits on how many vms can be deployed at once and ensuring vms are shut down when not in use.
* Free private Git repositories, configurable Kanban boards and extensive automated cloud based load testing
* Formally known as Visual Studio Team Services
* Azure DevTest Labs, quickly create on demand Windows and Linux environments to test or demo applications directly from deployment pipelines

### Azure IoT 
* Azure IoT central allows you to connect to thermostats, alarms etc.  It is a fully managed sas solution.  It allows you to create IoT applications without writing any code.  It allows you to connect, monitor and manage IoT.  This also has dashboards that can be customised. 
* IoT Hub allows you to integrate your applications with devices, this is where the IoT devices connect in via.  It provides secure communications between millions of IoT devices.
* Azure Sphere makes your IoT devices more secure.  Which includes certified chips, Azure sphere operating system and Azure sphere security service which adds a layer of security to IoT devices.  Sphere prevents bad things being sent to IoT devices and vice versa.
* IoT Edge is a fully managed service that allows data analysis models to be pushed directly onto IoT devices, which allows them to react quickly to state changes without needing to consult cloud based AI models

### Azure backup 
* Azure backup can backup both Azure and on prem machine

### Azure Advisor 
* Azure Advisor can suggest how to improve, solution and reduce cost on your environment.  For example point out over provisioned machines and suggest a smaller more cost effective machine, it also suggests security recommendations.

### Analytics 
* Azure HDInsight is older, supports haddop, spark, hive and storm)
* Azure DataBricks is more user friendly and easier to manage than HDInsights and Azure Synapse Analytics.  It supports all previously supported version but also Spark
* Azure Synapse Analytics, Fully managed data warehouse with integral security at every level of scale at no extra cost.  This brings all the data factory stuff in to one workplace.  This brings data warehousing and big data analytics together
* Azure data factory is what orchestrates the data lake services.

### Azure CDN 
* Azure CDN caches most freq content around the world so users will get it from the nearest server to them

### Databases 
* Azure Cosmos DB, globally distributed database that supports NoSQL option
* Azure SQL Database, fully managed relational database with auto-scale, integral intelligence and robust security
* Azure Database for MySQL, fully managed and scabled MySQL, relational database with high availability and security
* Azure database for PostgreSQL, fully managed and scalable PostgreSQL relational database with high availability and security
* SQL Server on Azure Virtual machines, service that hosts enterprise SQL server apps in the cloud
* Azure Database Migration Service, a service that migrates database to the cloud with no application code changes
* Azure Database for MariaDB, fully managed and scalable MariaDB relational database with high availability and security
* MongoDB and Cassandra both has a key value pair
* MongoDB and Cassandra can span multiple regions and able to store json docs

### Shared responsibility Model 
* IAAS, storage, network, computer and hypervisor is all looked after by the provider (azure) os runtime and application layer is down to the customer
* PAAS, Customer is just responsible for the application and data
* SAAS, for example something like office365, no exchange servers or exchange just the email service.  This is all down to the provider.

### Azure DDos Protection 
* Protects Azure hosted application from distributed denial of server attacks
* Everything by default is protected by basic DDoS protection but it's more to protect Azure than you
* Standard DDoS plan can be linked to vnets and uses machine learning to tune to learn your normal interaction, it also gives metrics and reporting
* Rapid response means you can talk to a human in an attack and if it doesnt protect you I.E scaled up vms you can get credits
* Azure standard DDoS cannot be used over multiple subscriptions

### Azure Network Watcher 
* Monitors and diagnoses network issues by using scenario based analysis

### Azure Firewall 
* Implements high security, high availability firewall with unlimited scalability
* Auto scales bas on the demand it needs
* Understands layer 4 and layer 7
* Deploys in to it's own subnet
* All other subnets are configured to go via the firewall as its first hop using user defined routes
* Had app rules like url, fqdn and catagories)
* You can have network rules like NSG
* Premium SKU allows you to do TLS inspection
* It can do DNAT rules
* It uses vm scale sets behind the scenes

### AI 
* Azure Machine Learning Service, allows you to develop, train, test, deploy, manage and track machine learning models.  It can auto generate a model and auto tune it for you.  You can start on your local machine then scale out to the cloud.
* Azure ML Studio, Collaborative visual workspace where you can build and deploy machine learning solutions by using prebuilt machine learning algorithms and data handling models.

### Azure Policy 
* A policy can be created on a resource group to limit things like "You can only deploy stuff in XXX region, budget etc etc"
* You can create initiatives which is a collection of multiple polices, you then apply the initiative to something/

### Azure Blueprints 
* Allows you to deploy an entire environment, a blueprint is a collection of arm templates plus permissions.
* Azure Blueprints allows you to define a repeatable set of governance tools and standard Azure resources that your organisation requires.

A blueprint is a collection of:
* Resource group(s)
* Arm template
* RBAC
* Policy which is assigned to a subscription

### Azure App Service 
* Quickly create powerful cloud web based apps
* App service free and shared means sharing resources with other customers

### Azure Notification Hub 
Send push notifications to any platform from any back end

### Azure API Management 
Publish APIs to developers, partners and employees security and at scale

### Azure Cognitive Search 
* Fully managed search as a service

### Serverless 
* Also known Functions or Logic Apps.  A function could be used to run a scheduled PowerShell script of some other code and you would just pay for when it ran.  A Logic app requires no coding just a user friendly interface with pre made functions.

### AI 
* Azure Cognitive services, pre built AI bots
* Azure Bot Server, build virtual agent

### Scalability vs Elasticity 
Scalable environments only care about increasing capacity to accommodate an increasing workload.
Elastic environments care about being able to meet current demands without under/over provisioning, in an autonomic fashion.

Scalability will scale up if needed but you will be left with the addition resource is load reduces where as Elasticity will both scale up and down based on load.

### Azure Key Vault 
Azure Key Vault supports 3 different types of identity:
* Secrert (read/write) like a password or share signature
* Keys (generate and import but cannot export)
* Cert (life cycle management and distribution)

You can fun all of these on top of HSMs

There are two types of authentication for key vault which are:
* Access policy, specify and user and what permissions they get, it isnt very granular
* Role based, this is more granular, its a managed identity which is tied to a compute resource, the identity will be given permissions so it can authenticate with key vault
* key vault is used to store secrets for server applications

### Azure dedicated hosts 
* You can create a dedicated host instance then add them to a host group and you can plit them over different fault domains (racks) this means only your vms go on these hosts not other vms from other customers.  
* Each dedicated host can only run a certain SKU of vm and you choose which one.
You have to pay for the use of the entire host even if you only use 10% of it.
* If you buy a dedicated host you can specify maint windows

If however you build an isolated vm type (big spec vm) you will be on your own host because your vm will just consume the entire machine.

### Authentication vs Authorization 

* authn (authentication) is the process of identifying a person or service, proving they are who they say they are
* authz (authorization) is what that person or service can do once they have been authenticated.

### SLA 
99.9 - 10 mins downtime a week

99.95 - 5 mins downtime a week

99.99 - 1 min downtime a week

99.999 - 6 seconds downtime a week

### Zero Trust 
* verify explicitly
* Use least privilege access
* Assume breach

### Microsoft Documents 
* Microsoft Privacy statement = What personal information MS collects
* Online Services Terms (OST) = What is the key agreement between client and MS
* Data Protection Addendum = More information about the data processing, handling and security of my services

### Soverinty 
* USA, China and Germany all have sperate Azure cloud for security
* China's Azure for gov is run by 21Vianet

### Reservations 
* You can get big discounts on vms if you agree to a reserved instance, I.E.  I will agree to run this vm for XX years.  This means you get a massive discount BUT if you turn the machine off after a year you still have to pay the agreed rates for the rest of the term.

### Azure Service Trust Portal 
* This has compliance and audit reports for things like sox, iso etc

### Azure Trust Center 
* Security, privacy, compliance, transparency, trust, GDPR etc standards and how it is auditied.  Regulatory documents.  It shows all the compliance offerings MS has.

### Defence in Depth 
CIA = Confidentiality, integrity and availability

### Sentinel 
This is a SIEM (Security Information Event Management).  It is also a SOAR (Security, orchastraction, Automation, Response).  Sentinel sits on top of log analytics workspace where all the logs get ingested. 

### Azure AD Identity Protection 
Identity Protection allows organizations to accomplish three key tasks:

* Automate the detection and remediation of identity-based risks.
* Investigate risks using data in the portal.
* Export risk detection data to other tools.

Identity Protection detects risks of many types, including:

* Anonymous IP address use
* Atypical travel
* Malware linked IP address
* Unfamiliar sign-in properties
* Leaked credentials
* Password spray

### Support plans 
The support plans are as follows:
* Basic - can request 24/7 support for billing only
* Developer - can request support but only get response in working hours
* Standard - can request support 24/7 and have phone support
* Professional direct - can request support 24/7 and have phone support along with architectural support

All the above can do the same with the exception of Standard and Professional Direct which both have 24/7 access to technical support by email and phone after a support request is submitted.

### Azure Site Recovery 
* Can protect Azure vms and on prem
* You only pay for what you spin up in DR
* You can test DR plans with no impact

### Service Trust Portal 
* This is where it shows how MS has been audited against things
* Had trust documents
* Has results of MS test's and audits
* This is where you would point your compliance officer for reports

### Misc 
* Azure resource locks can prevent accidental deletion or modification of an Azure resource.  Even an administrator cannot delete it if the lock is in place, the lock will need to be deleted first then the resource deleted.  They can be applied to subscriptions, resource groups or resources.
* Microsoft has Azur datacenters in every continent apart from Antarctica
* If a virtual machine has a public IP address, if the vm is stopped/deallocated it will release the public ip address
* Availability set = Services spread over different racks in the same zone
* Availability zone = Services spread over different zones (dc's) in the same region
* Something can only be in 1 resource group
* You cannot put a resource group in another resource group
* AKS = Azure Kubernetes Service is for management, automation and orchestration of containers
* A Azure spot instance is something (vm) you can run at very low cost but it can be shutdown by Microsoft in 30 seconds is resource is needed.  So you should not run anything critical on it.
* Azure Cache for Redis, fully managed service which caches frequently used and static data to reduce data and application latency
* Permissions or roles applied to a resource group will get pushed down to everything in it
* A subscription trust 1 and only 1 tenant, a tenant is when on prem AD syncs with Azure AD to create a subscription and the tennant is seperate from this subscription
* ARM = Azure Resource Manager
* VMSS = Virtual Machine Scale Set.  You specify in a template how much it can scale up or down then create some conditions, I.E.  If the CPU goes over 80% for 5 mins then Azure Batch will queue the job to build and add more vms
* azcopy can be used to copy from local machine to Azure and also from cloud to cloud, it is also server side so does not have to go to you machine then the destination
* ARM templates you can update and change the template and it will go off and make the change, so if you change LRS to GRS it will just make the change
* Bicep is more user friendly than ARM templates
* If you apply a resource lock to a resource group, all the resources get this lock.  If there are two or multiple locks applied the most restrictive one will apply.  You need to delete the locks before being able to change/delete the resource.
* You can apply tags to resource groups but they do not get pushed down to the resources in the group
* If you delete a resource group, all the resources in the group will be deleted as well
* Tags are not inherited but this can be done via Azure Policy
* Tags can also be enforced using Azure Policy
* Scale Sets can have a max of 1000 vms if you use the Azure vm images but only 600 if you use a custom image
* Azure AD free you can only use the Microsoft authenticator app, premium allows you to do conditional access which allows conditions like only allow logins from Windows 10 and if the user tries to login from an unknown location etc.
* Some things deployed are zone redundant (spanned over multiple zones) some are zonal meaning its deployed to a specific zone
* Azure Hybrid Benefit allows you to bring Windows and SQL licensing if they are covered under a MS assurance plan to Azure to save cost on licensing.
* Buying an Azure subscription directly through the Azure website is referred to as Web Direct
* Azure repos provides a set of version control tools
* AZ Commands will work in powershell
