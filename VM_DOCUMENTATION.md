# Deploying a Simple Webpage on Azure using a Virtual Machine
---

# Table of Contents
1. [Introduction](#introduction)
2. [Prerequisite](#prerequisite)
3. [Step-by-Step Guide](#step-by-step-guide)

## Introduction
In this project, I will deploy a simple webpage on Microsoft Azure, utilizing Azure compute and network services. The goal is to give me hands-on experience with provisioning and configuring virtual machines (VMs), setting up networking components, and deploying a web app.

## Prerequisite
Before starting this project, ensure you have the following:
- An Azure account. You can sign up for a free account[here]().
- Basic knowledge of web development.
- Access to a web browser.
- An application or webpage ready for deployment


## Step-by-Step Guide
### Provisioning a Virtual Machine
1. Login to the [Azure Portal]()
2. In the Azure portal dashboard, click on `Create a resource` in the upper-left corner.
3. Search for `Virtual Machine` and select `Virtual Machine` from the search results OR select `Virtual Machine` from the list of resources.
4. Under the `Basics` tab, Select your Azure subscription and Resource Group under the project details section. Then In the instance details section give your VM a unique name, select a region in this case i used `South Africa North` because it is closer to my country, chose an availability option and zone.
5. Select your security type, Image (basically the operating system, i chose ubuntu), VM architectureand VM size. For the VM size i chose to use a B series size because they are cheap and use lesser resources, which is enough for my single webpage deployment.
6. For the  virtual Machine authentication type, I selected `password`,I set my public inbound ports to `Allow selected ports`and selected the inbound ports.
7. Under `Disks` tab, I used the default image OS disk size, selected the `standard SSD (locally-redundant storage)` as OS disk type because Standard SSD is the best for web servers lightly used enterprise applications and dev/test, also using locally redundant storage because the project is not serious enough that it only requires data to be replicated within a single datacenter.
8. I chose `platform managed key` for key management because with PMKs, the keys generated are stored and managed by Azure.
9. Under the `Networking` tab, I left everything at default in the Network Interface section.
10. I enabled `Delete public IP and NIC when VM is deleted` and selected `None` for load balancing option because my single webpage would not be recieving traffic that would require one.
11. Under `Management` tab, everything was left at default.
12. Under `Monitoring` tab, I chose `Enable with managed storage account` as the boot diagnostics.
13. Select the `Review + Create` tab.
14. Once VM configuration is satisfactory select `Create`.
> YAAYYY!! the Virtual Machine has been provisioned.

### Connect to the Virtual Machine
> A VM can be connected to using SSH (for Linux VMs) or RDP (for Windows VMs)
1. Go to the virtual machine that was provisioned.
2. click on `Configure`.
3. Select a tool for connecting. I chose the `SSH using Azure CLI`.
4. Configure it and connect.
5. A CLI would appear, I chose `Bash` as the CLI .
6. In the CLI use the code, to ``` ssh username@public_ip_address``` 
7. Key in the VM password.

### Install and Configure a Webserver
Install a web server software on your VM. Common choices include Apache, Nginx, or IIS. For this project i used `Apache` webserver.
1. Update the package index and install Apache web server.
```sudo apt-get update && sudo apt-get install apache2```
2. Configure the web server to serve the web page files. For Apache, you'd typically place your files in the `/var/www/` directory.

### Transfer Webpage files
Tools like SCP, WinSCP, Git or FTP can be used to upload files. Since my webpage is already on GitHub, I would clone the repository to the `/var/www` directory.
1. Move into the `www` directory from thr oot directory.
```cd /var/www```
2. Clone the repository.
``` sudo git clone <git url>```
3. Move into the Azure-Virtual-Machine directory.
``` cd Azure-virtual-Machine``
4. Set Permissions.
``` sudo chmod -R 755 /var/www/```


### Deploying a Webpage
To actually have our webpage served, we need to ensure that Apache is configured to serve the specific webpage.
1. Change directory to the root directory and navigate to the `sites_available` folder to see the `000-default.conf` file.
``` ../../etc/apache2/sites-available```
2. Using Vim open the `000-default.conf file
```sudo vim 000-default.conf```
3. Edit the config file by changing the DocumentRoot from `/var/www/html` to `/var/www/Azure-Virtual-Machine` then save and quit.
4. Before accessing the website, it's a good idea to test the Apache configuration to ensure there are no syntax errors.
``` sudo apache2ctl configtest```
5. If there are no errors, restart the Apache service to apply the changes.
```sudo systemctl restart apache2```

> Now the webpage is accessible via my public address http://4.222.184.194