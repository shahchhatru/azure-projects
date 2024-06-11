## In this we will create our own virtual network

Step 1: First let's click on resource group click create Resource group.

Fill in the information for example I named it chhhatra_group.


Step 2 : Click on create Virtual network.
Assign it to the resource group .
Enable Bastain host and 
Enable Firewall and 
Choose a proper Ip address with appropiate CIDR.
![alt text](azure_img1_virtual_network-1.png)

Once deployment is completed your dashboard should look something like this.

![alt text](azure_img2_virutalnetwork-1.png)

Now create a Virtual Machine 
follow similar steps [Click here](../README.md)

only difference is that you will choose the chhatra_resource group or the resource group which we have created instead of creating a new one  and assign it to one of the subnet in our virtual network.

And we won't have any public IP address for this virtual machine as we will use bastian to connect to our machine .

**Note always chose free services eligible ubuntu and B1 series machine free services eligible**

![alt text](azure_img3_vm_networksettings.png)

We are not assigning it any public ip address.s

Now we have the user group created , we created a virtual network with firewall and bastain host  and connect our virtual machine in the default subnet.

Go to the created a virtual machine and search 

![alt text](azure_img4_vm_bastianhost.png)

Change authentication type to ssh  private key from local

and upload the pem file from your local computer . the pem file must have been downloaded while creating vm.

![alt text](azure_img5_vm_bastianhost.png)

give user nmae as azureuser if you havenot changed the default while configuration.

Just search Bastian that you created and you can view access control permssion which you can edit as per your need.

Right now , we are just using bastian as a proxy to access to VM.


![alt text](azure_img6_vm_bastian_host-1.png)


Okay now let's come back to VM 


![alt text](azure_img5_vm_bastianhost.png)

click connect


and you should see a new tab opening like this.
![alt text](azure_img7_bastian_terminal.png)

Now you can run all ubuntu commands in the terminal as a normal computer 

In this example let's install nginx.

```
sudo su
apt-get update

```
You can always refer to nginx documentation for installing nginx on ubuntu.

```
apt-get install nginx -y

```

Now I want to host a static website.

```
cd /var/www/html

```

```
ls
```

```
pwd
```
Let's create a simple file named index.html

![alt](azure_img8_settingup_static_page.png)

```
vim index.html
```

and then 

```
systemctl restart nginx

```

Nginx is installed in vm but the vm can't be directly accessed as it has only private subnet.

Now the only way to access it is configuring the firewall

So le't configure it.

search for firewall and open it.


![firewall](azure_img9_firewalldashboard.png)

Click on firewall poclies 
and go to DNAT rules.



![alt text](azure_img10_firewallsetings.png)


Click on ADD a rule collection

![alt text](azure_img11_adding_a_rulecollection-1.png)

After adding a collection create a rule
source ip should be your ip address
destiantion ip the ip address of firewall
Translation type is Ip address

translated ip address is the ip address of the vm.
nginx always run on port 80 so translated port should be 80

![alt text](azure_img12_dnat_ruleapplied-1.png)

Click save

Now if you type destination address the address of the firewall and then port 4000

You should probably see this 

![alt](success.png)

Horray we successfullly completed the task.

