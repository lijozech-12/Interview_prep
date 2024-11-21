# Azure Management Infrastructure

### Azure resources and resource groups.

resource groups are simply groupings of resources. when you create a resource, you're required to place it into a resource group.

a singlre resource can only be in one resource group at a time. 
If you move one resource to another group it won't be associated with the former group.
When you do an action to the resource it will be applied to all the resources in the group. 
If you delete a resource group all resources will be delted.
If you grant or denies access it happens the same.

If you want a temp dev environment grouping all the resource together means you can deprovision all of the associated resources at once by deleting the resource group.

### Azure subscriptions

subscriptions are a unit of management, billing, and scale. It will allow to logically organize your resource groups and faciliate billing.

A subscription provides you with authenticated and authorized access to Azure products and services.

`billing boundary:` azure generates separate billing reporst and invoices for each subscription so that you can organize and manage costs

`Access control boundary:` you create different departments and add distince Azure subscription polices. This billing model allows you to manage and control access to the resources that users provision with specific subscriptions.

##### Create additional Azure subscriptions

`Environments:` We can create separate environments for development and testing, security, ot to isolate data for compliance reasons

`Organizational structures:` Create subscriptions to reflect different organizational structures. We can limit one team to lower-cost resources, while allowing the IT department a full range. This design allows you to manage and control access to the resources that users provision within each subscription

`Billing:` Help to create subscriptions to manage and track costs based on your needs. For instance, you might want to create one subscription for your production workload and another subscription for your development and testing workloads.


### Azure management groups.

Resources are gathered into resource groups, and resource groups are gathers into subscriptions
Azure management groups provide a level of scope above subscriptions.
You organize subscriptions into containers called management groups and apply governance conditions to the management group, the same way that resource groups inherit settings from subscriptions and resouces inherit from resource groups.


# Describe Azure compute and networking services.

### Describe Azure virtual machines

* Total control over the operating system (OS)
* The ability to run custom software
* To use custom hosting configurations.

### Scale VMs in Azure

You can run single VMs for testing, development, or minor tasks. Or you can group VMs together to provide high availability, scalability and redundancy.

### Virtual machine scale sets

It will let you create and manage a group of identical, load-balanced VMs. 

If you simply created multiple VMs with the same purpose, you'd need to ensure they were all configured identically and then set up network routing parameters to ensure efficiency.

Here Zaure to the most of the works. The numbe of VM instances can automatically increase or decrease in response to demand, or you can set it to scale based on a defined schedule.

The no of VM can automatically increase or decrease in response to demand, or you can set it to scale based on a defined schedule. Virtual machine scale sets also automaticaly deploy a load balancer to make sure that your resources are being used efficiently.


### Virtual machine availability sets

Helps you to build a more resilient, highly available environment. Availability sets are designed to ensure that VMs stagger updates and have varied power and network connectivity.

Availability accomplish these objectives by grouping VMs in 2 ways: update domain and fault domain

`update domain:` Groups VMs that can be rebooted at the same time. This setup allows you to apply updates while knowing that only one update domain grouping is offline at a time. All of the machines in one update domain update. An update group going through the update process is given a 30-minute time to recover before maintenance on the next update domain starts.

`Fault domain:` Groups VMs by common power source and network switch, By default, an availability set splits your VMs across up to 3 fault domains.

### Examples of when to use VMs

* During testing and development
* When Running appplications in the cloud.
* When extending your datacenter to the cloud.
* During disaster recovery.


`Create a Linux virtual machine and install Nginx`

```bash
az vm create --resource-group "learn-471489a1-c558-4c8a-8d6d-0bcd20eb5019" --name my-vm --public-ip-sku Standard --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys
```
`Create a Linux virtual machine and install Nginx`

```bash
az vm extension set --resource-group "learn-471489a1-c558-4c8a-8d6d-0bcd20eb5019" --vm-name my-vm --name customScript --publisher Microsoft.Azure.Extensions --version 2.1 --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```

# Describe Azure Desktop

Another type of virtual machine is the Azure Virtual Desktop. Azure Virtual Desktop is a desktop and application virtualization service that runs on the cloud.

It enables you to use a cloud-hosted version of Windows from any location.

### Enhance Security

Azure Virtual Desktop provides centralized security management for users desktops with microsoft Entra ID. You can enable multifactor authentication to secure user sign-ins. You can also secure access to data by assigning granular role based access controls (RBACs) to users.


### Multi-session Windows 10 or Windows 11 deployment..

Windows 10 and 11 allow you to have multiple concurent users on a single VM. Azure virtual desktop also provices a more consistent experience with broader application support compared to Windows server-based operationg systems.

# Describe Azure containers

To run multiple instances of an application on a single host machine, containers are an excellent choice.

### What are containers ?

Containers are a virtulization environment.
It are lightweight and designed to be created, scaled out and stopped dynamically. It's possible to create and deploy virtual machines as application demand increases, but containers are a lighter weight, more agile method. It allow you to respond to changes on demand. With containers, you can quickly restart if there's a crash or hardware interruption


### Azure container Instanes

Azure Containers instanes offer the fastest and simplest way to run a container in Azure; without having to manage any virtual machines or adopt any additional services.

Azure containers instanes are a Platform as a service(PAAS) offering.
Azure container instances allow you to upload your containers and then the service runs the containers for you.

### Azure Container Apps.

It is similar in many ways to a container instance.
They allow you to get up and running right away, they remove the container management piece, and they're a PaaS offering. 
Container Apps have extra benefits such as the ability to incorporate load balancing and scaling.

### Azure Kubernetes Service(AKS)

It is a container orchestration service. An orchestration service manages the lifecycle of containers
When You're deploying a fleet of containers, AKS can make fleet management simpler and more efficient.

# Describe Azure functions

Azure functions is an event-driven, serverless compute option that doesn't require maintaing virtual machines or containers. If you build an app using VMs or containers, those resources have to be "running" in order for your app to function.

With Azure Functions, an event wakes the function, alleviating the need to keep resources provisioned whtn there are no events.

### Serverless computing in Azure

### Benefirs of Azure Functions

Using Azure function is ideal when you're only concerned about the code running your service and not about the underlying platform or infrastructure. Functions are commonly used when you need to perform a work in response to an event(REST request), timer, or massage from anohter Azure service, and when that work can be completed quickly, within seconds or less.

Functions scale automatically based on demand, so they maybe a good choice when demand is variable.

Azure Functions runs your code when it triggers and automatically deallocates resources when the function is finished.

Functions can be either stateless or stateful. When they're stateless (the default), they behave as if they restart every time they respond to an event.

When they're stateful (called Durable Functions), a context is passed through the function to track prior activity.

Functions are a key component of serverless computing. They're also a general compute platform for running any type of code.

# Describe application hosting options.

General options would be VMs or Containers.
VMs will have maximum control of hosting environment and allow you to configure it exactly how you want.

Containers,with the ability to isolate and individually manage differen aspect of the hosting solution, can also be a robust and compelling option.

### Azure APP Service

It helps to build and host web apps, background jobs, mobile back-ends and RESTful APIs in the programming language of your choice without mananging infrastructure.

It offers automatic scaling and high availability.

App Service supports Windows and Linux. 
It enables automated deployments from GitHub, Azure Devops or Git repo

### Types of App Services

1. Webapps
app service includes full support for hosting web apps by using ASP.NET, ASP.NET core, Java, Ruby, Node.js, PHP or Python

2. API apps
Much like hosting a website, you can build REST-based web APIs by using your choice of language and framework. You get full swagger support and the ability to package and publish your API in Azure maketplace

3. WebJobs

You can use the WebJobs feature to run a program(.exe, Java, PHP, python, or NODE.js)

4. Mobile apps

Mobile apps feature of APP service to quickly build a back end of iOS and Android apps.

# Describe Azure virtual networking.

Azure virtual networks and virtual subnets enable Azure resources, such as VMs, web apps, and databases, to communicate with eachother, with users on the internet, and with your on-preises client computers.

* Isolation and segmentation
* Internet communications
* Communicate between Azure resources
* Communicate with on-premises resources
* Route network traffic
* Filter network traffic
* Connect virtual networks

### Isolation and segmentation

Allows to create multiple isolated virtual networks. 
When you set up a virtual network, you define a private IP address space by using either public or private IP address ranges.

The IP range only exists within the virtual network and isn't internet routable.

For name resolution, you can use the name resolution service built into Azure. You also can configure the virtual network to use either an internal or an external DNS server.

### INternet communications.
You can enagle incoming connections from the internet by assigning a public IP address to an Azure resource

### Communciate between Azure resources.

Virtual networks can connect not only VMs but other Azure resources, such as the App Service Environment for Power Apps, Azure Kuberentes Service, and Azure virtual machine scale sets.

Service endpoints can connect to other Azure resource types, such as Azure Sql databases and storage accounts. This approad enable you to link multiple Azure resource to virtual networks to imporve security and provide optimatl routing between resources.

### Communicate with on-premises resources.

Azure virtual networks enable you to link resource together in you on-premises environment an within your Azure subscription.

`Point-to-site` virtual private network connections are from a computer outside your organization back into your corporate network. In this case, the client computer initiates an encrypted VPN connection to connect to the Azure virtual network.

`Site-to-site` virtual private networks link your on-premises VPN device or gateway to the Azure VPN gateway in a Virtual network. In effect, the devices in Azure can appear as being on the local network. The connection is encrypted and works over the internet.

`Azure ExpressRoute` 
Provides dedicate private connectivity to Azure that doesn't travel over the internet.m Expressroute is useful or environements where you need greater bandwidth and even higher levels of security


### Route network traffic

Azure routes traffic between subnets on any connected virtual networks, on-premises networks, and the internet. You also can control routing and override those settings

* route tables allow you to define rules about how traffic should be directed, you can create custom route table that control how packet are routed between subnets

* Border Gateway Protocol (BGP) works with azure VPN gateways, Azure route server or Azure ExpressRoute to propagate on-premises BGP routes

### Filter network traffic

allows you to filter traffic between subnets by using hte following approaches.

`Network security groups` are resource that can container multiple inbound and outbound security rules. You can define these rules to allow or block traffic, based on factors such as source and destination IP address, port and protocol

`Network virtual applicances` are specilized VMs that can be compare to a hardened network appliance. A network virtual appliance carries out a particular network function, such as running a firewall or performing wide are network (WAN) optimization.

### Connect virtual networks

You can link virtual networks together by using virtual network peering. 
Peering allows 2 virtual networks to connect directly to eachother.
Network traffic between peered networks is private, and travels on the microsoft backbone network, never entering the public internet. Peering enables resource in each virtual network to communicate with each other. These virtual networks can be in separate regions. This fetaure allows you to create a global interconnected network through Azure.


### Access your webserver

To verify the VM you created previously is still running, use the following command:

```bash
az vm list
```

Run the following az vm list-ip-addresses command to get your VM's IP address and store the result as a Bash variable:
```bash
IPADDRESS="$(az vm list-ip-addresses --resource-group "learn-d0b7b7df-7eca-4ce8-9bd0-d7896fe5c140" --name my-vm --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" --output tsv)"
```

Task 2: List the current network security group rules
Your web server wasn't accessible. To find out why, let's examine your current NSG rules.

Run the following az network nsg list command to list the network security groups that are associated with your VM:

Azure CLI

Copy
az network nsg list \
  --resource-group "learn-d0b7b7df-7eca-4ce8-9bd0-d7896fe5c140" \
  --query '[].name' \
  --output tsv    

















You see this output:

Output

Copy
my-vmNSG



















Every VM on Azure is associated with at least one network security group. In this case, Azure created an NSG for you called my-vmNSG.

Run the following az network nsg rule list command to list the rules associated with the NSG named my-vmNSG:

Azure CLI

Copy
az network nsg rule list \
  --resource-group "learn-d0b7b7df-7eca-4ce8-9bd0-d7896fe5c140" \
  --nsg-name my-vmNSG    

















You see a large block of text in JSON format in the output. In the next step, you'll run a similar command that makes this output easier to read.

Run the az network nsg rule list command a second time. This time, use the --query argument to retrieve only the name, priority, affected ports, and access (Allow or Deny) for each rule. The --output argument formats the output as a table so that it's easy to read.

Azure CLI

Copy
az network nsg rule list \
  --resource-group "learn-d0b7b7df-7eca-4ce8-9bd0-d7896fe5c140" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table    

















You see this output:

Output

Copy
Name              Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow


















You see the default rule, default-allow-ssh. This rule allows inbound connections over port 22 (SSH). SSH (Secure Shell) is a protocol that's used on Linux to allow administrators to access the system remotely. The priority of this rule is 1000. Rules are processed in priority order, with lower numbers processed before higher numbers.

By default, a Linux VM's NSG allows network access only on port 22. This port enables administrators to access the system. You need to also allow inbound connections on port 80, which allows access over HTTP.

Task 3: Create the network security rule
Here, you create a network security rule that allows inbound access on port 80 (HTTP).

Run the following az network nsg rule create command to create a rule called allow-http that allows inbound access on port 80:

Azure CLI

Copy
az network nsg rule create \
  --resource-group "learn-d0b7b7df-7eca-4ce8-9bd0-d7896fe5c140" \
  --nsg-name my-vmNSG \
  --name allow-http \
  --protocol tcp \
  --priority 100 \
  --destination-port-range 80 \
  --access Allow    

















For learning purposes, here you set the priority to 100. In this case, the priority doesn't matter. You would need to consider the priority if you had overlapping port ranges.

To verify the configuration, run az network nsg rule list to see the updated list of rules:

Azure CLI

Copy
az network nsg rule list \
  --resource-group "learn-d0b7b7df-7eca-4ce8-9bd0-d7896fe5c140" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table    

















You see both the default-allow-ssh rule and your new rule, allow-http:

Output

Copy
Name              Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
allow-http          100        80      Allow    

















Task 4: Access your web server again
Now that you configured network access to port 80, let's try to access the web server a second time.

 Note

After you update the NSG, it may take a few moments before the updated rules propagate. Retry the next step, with pauses between attempts, until you get the desired results.

Run the same curl command that you ran earlier:

Bash

Copy
curl --connect-timeout 5 http://$IPADDRESS

















You see this response:

HTML

Copy
<html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>

















As an optional step, refresh your browser tab that points to your web server. You see the home page:

A screenshot of a web browser showing the home page from the web server. The home page displays a welcome message.

Nice work. In practice, you can create a standalone network security group that includes the inbound and outbound network access rules you need. If you have multiple VMs that serve the same purpose, you can assign that NSG to each VM at the time you create it. This technique enables you to control network access to multiple VMs under a single, central set of rules.

Clean up
The sandbox automatically cleans up your resources when you're finished with this module.

When you're working in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources that you leave running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.



# Azure Virtual Private Networks.

Encrypted tunnel within another network

VPNs are typically deployed to connect 2 or more trusted private networks to one another over an untrusted network (typically the public internet).

Traffic is encrypted while travling over the untrusted network to prevent easesdroppping or other attacks. 

### VPN gateways

* Connect on-premises datacenters to virtual networks through a `site-to-site` connection.
* Connect individula devices to virtual networks through a `point-to-site` connection.
* Connect virtual networks to other virtual networks through a `network-to-network` connection.


All data transfer is encrypted inside a private tunnel as it crosses the internet. You can deploy only one VPN gateway in each virtual network.

When setting up a VPN gateway, you must specify the type of VPN - either policy based or route-based

* Policy-based VPN gateways specify statidally the IP address of packetst that should be encrypted through each tunnel. This type of device evaluates every data packet against those sets of IP addresses to choose the tunnerl where that packet is going to be sen through.

* Route-based gateways, IPSec tunnerl are modeled as a network interface or virtual tunnel interface.
IP routin (either static routes or dynamic routing protocols) decides which one of these tunnel interfaces to use when sending each packet.

### High-availability scenarios

if you're configuring a VPN to keep your information safe, you also want to be sure that it's highly available and fault tolerant VPN configurations.

`Active/standby`

VPN gateways are deployed as 2 instances in an active/standby configuration, even if you only see one VPN gateway resource in Azure. 
When planned maintenance or uplanned disruption affect the active instance, the standby instance automatically assumes responsibility for connection without any user interventions

connenction are interrupted during this failover.
They typically restore within a few seconds for planned maintencae and within 90 seconds for unplanned disruptions


`Active/active`

* support for BGP routing protocol
* Can also deploy VPN gateways in an active/actie configuration
* can assign a unique public IP address to each instance.
* Can create separate tunnel from the on-premises device to each IP address
* Can get addtional high availbility by deploying an additional VPN device on-premises


`ExpressRoute failover`

ExpressRoute circuits have resiliency builit in, they aren't immune to physical problems that affect the cables delivering connectivity or outages that affect the complete ExpressRoute location.
is to configure a VPN gateway as a secure failover path for Express Route connections'

`Zone-redundant gateways`

In regions that support availability zones, VPN gateways and ExpressRoute gateways can be deployed in a zone redundant configurations. 

# Azure ExpressRoute

* Help you to extend your on-premises networks itno the microsoft cloud over a  private connection, with the help of a  connectiviy provider. This connection is called an ExpressRoute Circuit.

* It helps you to connect offices, datacenters, or other facilites to the microsoft cloud.
* This setup allow ExpressRoute connections to offer more reliabilty, faster speeds, consistent latencies and higher security than typical connections over the internet.


### Features and benefits of ExpressRoute

# Azure DNS

Azure DNS is a hosting service for DNS domaints that provides name resolution by using microsoft Azure infrastructure. By hosting you domains in Azure


# Azure Storage Accounts

A storage account provides a unique namespace for your Azure storage data that's accessible from anywhere in the world over HTTP or HTTPs. Data in this account is secure, highly available, durable and massively scalable.

### Storage account endpoints

* benefits of using an Azure Storage Account is having a unique namespace in Azure for your data.
* In order to do this, every storage account in Azure must have a unique-in-Azure account name
* The combination of the account name and the Azure storage service endpoint forms the endpoint for your storage account


### Azure Storage redundancy

Azure storage always stores multiple copies of your data so that it's protected from planned or unplanned events.

Locally Redundant Storage (LRS): Replicates data within a single data center, offering 99.999999999% durability. It is the lowest-cost option but vulnerable to regional disasters.

Zone-Redundant Storage (ZRS): Replicates data across three availability zones, providing 99.9999999999% durability. It ensures data access during zone outages.

For secondary region redundancy, options include:

for security purposes we can copy the data into seconday region that is hundereds of mile away from the primary region.

Geo-Redundant Storage (GRS): Combines LRS in the primary region with asynchronous replication to a secondary region, offering 99.99999999999999% durability.

Geo-Zone-Redundant Storage (GZRS): Combines ZRS in the primary region with LRS in the secondary region, providing high availability and durability.

# Azure Storage services

### `Azure Blobs:` 
Object storage for text and binary data, supporting big data analytics through Data Lake Storage Gen2.
It is good for
    * Serving images or documents directly to a browser.
    * Storing files for distributed access.
    * Streaming video and audio.
    * Storing data for backup and restore, disaster recovery, and archiving.
    * Storing data for analysis by an on-premises or Azure-hosted service.

##### Blob storage tiers

    Hot access tier: Optimized for storing data that is accessed frequently (for example, images for your website).
    Cool access tier: Optimized for data that is infrequently accessed and stored for at least 30 days (for example, invoices for your customers).
    Cold access tier: Optimized for storing data that is infrequently accessed and stored for at least 90 days.
    Archive access tier: Appropriate for data that is rarely accessed and stored for at least 180 days, with flexible latency requirements (for example, long-term backups).

### `Azure Files:` 
Managed file shares for cloud or on-premises deployments

### `Azure Queues:` 
A messaging store for reliable messaging between application components
can store data that much storage account has room for
Each individul message can be up to 64 KB in size.


### `Azure Disks:`
 Block-level storage volmes for Azure VMs. harddisk or ssds

### `Azure Tables:` 
NoSQL table option for structured, non-relational data.
To store stoers large amounts of structured data.


# Azure data migration options

Azure migrate is a service that helps you migrate from an on-premises environment to the cloud.

* unified migration platform: A single portal to start, run an dtrack your migration to Azure

* Range of tools: A 

### AZure Data Box

Azure data box is a physcial migration service that helps to transfer large amount of data in quick, inexpensive and reliable way

# Azure file movement options