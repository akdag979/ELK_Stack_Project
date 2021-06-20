# ELK_Stack_Project
Install the Elastic Stack (ELK) on an Azure Platform

In this project, I will configure an ELK Stack Server in order to monitor cloud web servers.
This document contains the following details:
 -Details of the Network Topology
 -Access Policies
 -ELK Configuration
 	-Beats in Use
	-Machines being monitored
-How to use Ansible Build
-Additional Information


Description of Topology:
	A Load balanced and monitored instance of DVWA, the Damn Vulveranle Web Application.
	Load balancing ensures that the application will be highy stable, and Integrating an ELK server allows admins to easily monitor the vulnerable VMs.

The configuration details of each machine may be found below.

Name	                Function	IP Address	Operating System
Jump-Box-Provisioner	Gateway	        137.135.52.100	Ubuntu 18.04
Web-1	                Web Server	10.0.0.5 / 137.117.15.130	Ubuntu 18.04
Web-2	                Web Server	10.0.0.6 / 137.117.15.130	Ubuntu 18.04
Web-3	                Web Server	10.0.0.7 / 137.117.15.130	Ubuntu 18.04
ELK-Server	        Data Monitoring	20.98.153.248	Ubuntu 18.04

Access Policies
The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from my personal ip address.

Machines within the network can only be accessed by the Jump Box machine via ssh with the correct ssh key. The Elk-Server Vm could only be accessable via sshing from the container within the jump box.

A summary of the access policies in place can be found in the table below.

Name	        Publicly 	Accessible		Allowed IP Addresses
Jump Box	Yes		My-IP-Address
Web-1	        No		10.0.0.4
Web-2	        No		10.0.0.4
Web-3	        No		10.0.0.4
Elk-Server	No		10.0.0.4



Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the filebeat config file to /etc/ansible/files/filebeat-config.yml

Update the config file to include the IP address of your ELK-Server machine

Run the filebeat playbook, and navigate to http://[ELK-Server IP]:5601/app/kibana to check that the installation worked as expected.

Copy the metricbeat config file to /etc/ansible/files/metricbeat-config.yml

Update the config file to include the IP address of your ELK-Server machine

Run the metricbeat playbook, and navigate to http://[ELK-Server_IP]:5601/app/kibana to check that the installation worked as expected


Additional Informations:

Objective 1: Setup a virtual private network and 3VMs.

-Create a resource group.

-Create a Virtual Network in this Azure resource group.

-Create a virtual machine named Jump-Box-Provisioner. Take note of the publicIpAddress.
	SSH into your VM. In my example, the IP address is 137.135.52.100
		-->ssh azureuser@137.135.52.100

-Create 3 webservers named as Web-1, Web-2, Web-3 in an availibilty set without public adress.
	Make sure image is Ubuntuserver and size is "Standard B1ms"
	Use pentest.yml file to configure VM's with docker.

-Create a load balancer

-Install docker and Ansible to Jump-Box.
	-->sudo apt update
	-->sudo apt install docker.io
	-->sudo docker pull cyberxsecurity/ansible
	-->sudo docker run -ti cyberxsecurity/ansible:latest bash

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

