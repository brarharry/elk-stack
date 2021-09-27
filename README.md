## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/brarharry/elk-stack/blob/main/Diagram/ELK-DIAGRAM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the "filebeat-playbook.yml" file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting accessibilty to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logs and system resources.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box-Provisioner  | Gateway             | Private-10.1.0.4, Public-137.116.119.192   | Linux            |
| Web-1                 | Web Server          | Private-10.1.0.5, Public-20.106.93.197     | Linux            |
| Web-2     | Web Server          | Private-10.1.0.6, Public-20.106.93.197   | Linux            |
| ELK-Stack | ElasticSearch Stack | Private-10.2.0.4, Public-137.116.119.192   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My personal machine: 130.212.94.94

Machines within the network can only be accessed by Jump-Box-Provisioner: 20.150.136.43.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |     130.212.94.94(My Machine's IP)             |
| Web-1    | No                  |     10.1.0.4(Private - JumpBox's IP)           |
| Web-2    | No                  |     10.1.0.4(Private - JumpBox's IP)           |
| ELK-VM   | No                  |     10.1.0.4(Private - JumpBox's IP)    	  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because fewer resources are needed as Ansible uses shared resources to set up multiple machines at once.

The playbook implements the following tasks:
- Installs the following services:
	- docker.io
	- python3-pip
	- docker, which is the Docker Python pip module
- Increases the memory of the ELK-VM
- Downloads Elk container on the ELK-VM
- Enables the service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![screenshot of docker ps output](https://github.com/brarharry/elk-stack/blob/main/Resources/elk-docker.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.1.0.5
- Web-2: 10.1.0.6

We have installed the following Beats on these machines:
- Filebeat and Metricbeat on both the web servers, Web-1 and Web-2.

These Beats allow us to collect the following information from each machine:
- [Filebeats](https://github.com/brarharry/elk-stack/blob/main/Resources/FileBeat%20check.PNG "Filebeats") collect system logs, for example login activity, active users, and more. 
- [Metricbeats](https://github.com/brarharry/elk-stack/blob/main/Resources/MetricBeat%20check.PNG) collect information like how healthy machine is, for example cpu usage, memory usage 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the "install-elk.yml" file to "/etc/ansible/".
- Update the "hosts" file to include the "elk" group, then add the ELK-VM IP and what interpreter it is going to use.
	- ![](https://github.com/brarharry/elk-stack/blob/main/Resources/adding-elk-group.PNG)
- Run the playbook, and navigate to "http://137.116.119.192:5601/app/kibana" to check that the installation worked as expected.
	- ![](https://github.com/brarharry/elk-stack/blob/main/Resources/kibana-check.PNG)

_The specific commands the user will need to run to download the playbook, update the files, etc.
- To run the Playbook: ansible-playbook /etc/ansible/install-elk.yml
