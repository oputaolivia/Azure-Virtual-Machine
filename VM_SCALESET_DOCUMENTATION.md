# Deploying a zone-resilient Azure Virtual Machine Scale Sets
---
A Virtual Machine Scale Set (VMSS) is a powerful feature in Microsoft Azure that allows you to create and manage a group of identical virtual machines (VMs). These VMs are automatically load-balanced and can scale up or down based on demand or a predefined schedule.

# Table of Contents
1. [Create a Virtual Machine Scale Set (VMSS)](#create-a-virtual-machine-scale-set-vmss)
2. [Configure Virtual Network](#configure-virtual-network)
3. [Configure Load Balancing](#configure-load-balancing)
4. [Access the Virtual Machine Instance](#access-the-vmss-instance)

## Create a Virtual Machine Scale Set (VMSS)
1. Login to the [Azure Portal](https://portal.azure.com/).
2. In the search bar, search for __Virtual Machine Scale Set__ and select it.
![1](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/17c8df29-42c0-4af5-b8b6-cdfd04f488e0)

3. Click on the __+ Create__ or __create virtual machine scale set__ icon.
![2](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/a4498d0a-6b71-4182-9f62-59096b1f3f8c)

4. On the __Basics__ tab, Select an Azure subscription and Resource Group in the project details section. Then In the scale set details section give the VMSS a unique name, select a region (in this case I used __South Africa North__ because it is closer to my country) chose an availability zone.
![3](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f6bb6a7e-f8d5-4469-896e-c8bdb60d2e42)

5. In the orchestration section select a mode (For me I picked flexible) and a security type. In the Instance details section pick a VM image (basically the operating system, I chose ubuntu), VM architecture and VM size. For the VM size I chose to use a B series size because they are cheap and use lesser resources, which is enough for this practice.
![4](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/bfdc61d7-2a2a-41b8-b54d-90d718e904bf)

6. In the Administration account section, select an authentication type and do the needful. For me I chose to work with password authentication instead of SSH public key.
![5](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/79de17c5-248f-4dda-97c3-3b963296d5ec)

7. Leaving everything on the __Spot__ tab as default.
![6](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/24881877-acac-49e9-946e-02c9851fc138)

8. On the __Disks__ tab, I picked the default OS disk size and selected the OS disk typpe as Standard SSD (zone-redundant storage).
![7](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5b7031f4-4f31-4735-bb1b-094e28def328)

9. On the __Networking__ tab, I selected the recommended virtual network and network interface.
![8](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/a194e52e-c87e-4495-85e4-910456caada7)

10. In the Load balancing section, I selected none (Would configure this later).
![9](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/13988481-0ce8-40b2-925c-1af6092d9384)

11. On the __Scaling__ tab, I set my Initial instance count to 2 and scaling policy to Custom with a min. number and max. number of instances as 1 and 15 respectively. The following where the values of my scale out and scale in parameters;
     __Scale Out__:
    - CPU Threshold = 85
    - Duration (min) = 30
    - Number of instances to increase by = 1
![10](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/7b9f33fb-b134-46bb-a2f1-345bf94084ba)

    __Scale In__:
    - CPU Threshold = 30
    - Number of instances to increase by = 1
![11](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/5d467ba2-e2d1-4e53-a91d-999e6652d093)

12. Leaving everything on the __Management__ tab as default.
![12def](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/00ba5b75-baee-4e7a-a16c-e59530e84f92)

13. Leaving everything on the __Health__ tab as default.
![13def](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/bf82688a-0f6a-445b-afaf-5c75cb7e008c)

14. Leaving everything on the __Advanced__ tab as default.
![14def](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/b3fa1dca-7a2a-42b1-aeee-62d16a7e8413)

15. Click on the __Review + Create__ and await validation.
![15](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/ea7dc787-7d7d-4ad6-a10e-8de5c70b5705)

16. Once Validation passes, click on __Create__.

17. Once deployment is complete click on __Go to Resource__.
![16](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/7d2f14c2-4b78-4ff5-b7ac-adcaa7d45958)

## Configure Virtual Network
Already we selected a virtual network but here, some inbound port rules would be confihured to allow HTTPS and SSH (Since it's an Ubuntu VM instance that was created).
1. In the VMSS resource that was just created select the __Networking settings__ blade under the __Networking section__ and click on __+ Create Port rule__ then inbound port rule.
![17](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/645e653f-1fb1-4492-9645-05b266466b07)

3. Since I intend on creating an rule to allow SSH; leaving my source and destination as *Any*, I selected a service of SSH and action Allow.
![18](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/af4c3881-d10e-4905-a498-276cb3f8b863)

4. Giving the rule a priority of 100 (The lesser the number, the more imorpantant), a unique name and description. Once done select __Add__.
![19](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/2c3fa8f2-ea1b-4f9e-9d8d-dcccc58da1b7)

5. Refresh and the new rule would be visible.
![20](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f639b25a-ab1d-4287-9889-06bcbb2963a7)

## Configure Load Balancing
Remeber when trying to create a VMSS I selected Load balancing as none, now I would be configuring that.
1. Still in the VMSS resource, select the __Load balancing__ blade under the networking section and select Add load balancing.
![21](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/d96b3dd0-91cf-4c28-a86d-81611e750a56)

2. Give the load balancer a name, select the type and protocol.
![22](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/9684a41e-7178-40c5-a3d5-8fef3f413ed6)

3. Include the necessary load balancer rule and select __Create__.
![23](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/f6554e95-50b8-4dcb-947e-598f19d058d5)

4. Refresh and you have your load balancer.
![24](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/6d4b6cd1-188c-4ba0-8dd6-e115ada80ce8)

> Auto-Scaling can also be configured by going to the __Scaling__ blade under the __AValiability + Scale__ section.

## Access the VMSS Instance
Finally the VMSS is up and running, next we need to connect to it.
1. In the __Instances__ blade, select the VM instance.
![connect1](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/fe63ffad-0ac3-4eae-bc74-aca84e11c524)

2. Click on __Overview__ and copy the Public IP Address.
![connect2](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/c397bdc3-9d46-4edd-9ac2-7b1880b3108e)

3. Opening a command line interface like powershell or bash key in the following commands:
``` 
ssh username@public_ip_address
```
> Replace __username__ with your SSH username and __public_ip_address__ with the instance's Public IP Address that was copied.

4. Enter the SSH password when prompted.
> You are In!!
![27](https://github.com/oputaolivia/Azure-Virtual-Machine/assets/72948572/a51b5e60-3080-4ae2-87fe-e6bb7f262830)

