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

