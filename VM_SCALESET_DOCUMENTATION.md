# Deploying a zone-resilient Azure Virtual Machine Scale Sets
---

# Table of Contents
1. [Create a Virtual Machine Scale Set (VMSS)](#create-a-virtual-machine-scale-set-vmss)
2. [Configure Networkiing](#prerequisite)
3. [Configure Load Balancing](#step-by-step-guide)
4. [Access the Virtual Machine Instance]()

## Create a Virtual Machine Scale Set (VMSS)
1. Login to the [Azure Portal](https://portal.azure.com/).
2. In the search bar, search for __Virtual Machine Scale Set__ and select it.

3. Click on the __+ Create__ or __create virtual machine scale set__ icon.

4. On the __Basics__ tab, Select an Azure subscription and Resource Group in the project details section. Then In the scale set details section give the VMSS a unique name, select a region (in this case I used __South Africa North__ because it is closer to my country) chose an availability zone.

5. In the orchestration section select a mode (For me I picked flexible) and a security type. In the Instance details section pick a VM image (basically the operating system, I chose ubuntu), VM architecture and VM size. For the VM size I chose to use a B series size because they are cheap and use lesser resources, which is enough for this practice.

6. In the Administration account section, select an authentication type and do the needful. For me I chose to work with password authentication instead of SSH public key.

7. Leaving everything on the __Spot__ tab as default.

8. On the __Disks__ tab, I picked the default OS disk size and selected the OS disk typpe as Standard SSD (zone-redundant storage).

9. On the __Networking__ tab, I selected the recommended virtual network and network interface. In the Load balancing section, I selected none (Would configure this later).

10. On the __Scaling__ tab, I set my Initial instance count to 2 and scaling policy to Custom with a min. number and max. number of instances as 1 and 15 respectively. The following where the values of my scale out and scale in parameters;
     __Scale Out__:
    - CPU Threshold = 85
    - Duration (min) = 30
    - Number of instances to increase by = 1
    __Scale In__:
    - CPU Threshold = 30
    - Number of instances to increase by = 1

11. Leaving everything on the __Management__ tab as default.

12. Leaving everything on the __Health__ tab as default.

13. Leaving everything on the __Advanced__ tab as default.

14. Click on the __Review + Create__ and await validation.

15. Once Validation passes, click on __Create__.

16. Once deployment is complete click on __Go to Resource__.

## Configure Virtual Network
Already we selected a virtual network but here, some inbound port rules would be confihured to allow HTTPS and SSH (Since it's an Ubuntu VM instance that was created).
1. In the VMSS resource that was just created select the __Networking settings__ blade under the __Networking section__ and click on __+ Create Port rule__ then inbound port rule.

2. Since I intend on creating an rule to allow SSH; leaving my source and destination as *Any*, I selected a service of SSH and action Allow.

3. Giving the rule a priority of 100 (The lesser the number, the more imorpantant), a unique name and description. Once done select __Add__.

4. Refresh and the new rule would be visible.

## Configure Load Balancing
Remeber when trying to create a VMSS I selected Load balancing as none, now I would be configuring that.
1. Still in the VMSS resource, select the __Load balancing__ blade under the networking section and select Add load balancing.

2. Give the load balancer a naem, select the type and protocol.

3. Include the necessary load balancer rule and select __Create__.

4. Refresh and you have your load balancer.

> Auto-Scaling can also be configured by going to the __Scaling__ blade under the __AValiability + Scale__ section.

## Access the VMSS Instance
Finally the VMSS is up and running, next we need to connect to it.
1. In the __Instances__ blade, select the VM instance.

2. Click on __Overview__ and copy the Public IP Address.

3. Opening a command line interface like powershell or bash key in the following commands:
``` 
ssh username@public_ip_address
```
> Replace __username__ with your SSH username and __public_ip_address__ with the instance's Public IP Address.

4. Enter the SSH password when prompted.
> You are In!!

