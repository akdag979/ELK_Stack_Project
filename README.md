# ELK_Stack_Project
Install the Elastic Stack (ELK) on an Azure Platform

In this project, I will configure an ELK Stack Server in order to monitor cloud web servers.


Objective 1: Setup a virtual private network and 3VMs.

-Create a resource group.

-Create a Virtual Network in this Azure resource group.

-Create a virtual machine named Jump-Box-Provisioner. Take note of the publicIpAddress.
	SSH into your VM. In my example, the IP address is 137.135.52.100
		-->ssh azureuser@137.135.52.100
-Create 3 webservers named as Web-1, Web-2, Web-3 in an availibilty set without public adress.

-Create a load balancer

-Install docker and Ansible to Jump-Box.
	-->sudo apt update
	-->sudo apt install docker.io
	-->sudo docker pull cyberxsecurity/ansible
	-->sudo docker run -ti cyberxsecurity/ansible:latest bash

-Deploy Containers using Ansible and Docker
-Update the Ansible config file and hosts file
	-->ls /etc/ansible
	-->nano /etc/ansible/hosts
	-->nano /etc/ansible/ansible.cfg
-Test an Ansible connection 
	-->ansible all -m ping

-Create a new virtual network in the same resoruce group
	Make sure this vNet is located in a new region and not the same region as other VM's.

-Create a Peer connection between vNets. This peer connection will make both a connection from first vNet to Second vNet and a reverse connection from second vNet back to first vNet.

-Setup a new virtual machine to run ELK
	Make sure this VM has at least 4 GB of RAM.
	Make sure it has a public IP address.
	Make sure it is added to the new vNet and create a new Security Group for it.
-Configure Elk VM with Docker
	Check ELK Playbook for reference
	Create an incoming rule for your security group that allows TCP traffic over port 5601 from your IP address.
	Verify that you can load the ELK stack server from your browser at http://[your.VM.IP]:5601/app/kibana


-Deploy Filebeat and Metricbeat using Ansible 
-Allow access only from jump-box and load balancer to Web servers.
-Allow SSH connections from your current IP address.


Objective 2: Create a Load Balancer on the Azure platform. 