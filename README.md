## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: ELK Stack](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/Proj_Wk13_CloudELK.PNG)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: [ELK install yaml file](https://media.githubusercontent.com/media/goosee007/CyberSecurity-XpreTech/main/Ansible/install-elk.yml?token=ADA4W4VR5KS4PEEUSJQXHQK76KQIC)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _What aspect of security do load balancers protect?_
	- Load balancers off-loading functionality has the potential to deflect DDOS attacks. 
	- Shift attack traffic from corporate servers to public cloud providers.
- _What is the advantage of a jump box?_
    - Advantages: is that it allows admins to minimize attacks surface thus making an attack harder. 
	- Is an hardened and monitored device that provides a controlled means of access between two dissimilar security zones.
		
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file logs and system metrics traffic.
- *What does Filebeat watch for?*
    - Filebeat is designed to watch for and ship log files and forwards the data to Elasticsearch for indexing.
	- It's actually a logging agent that is installed on a server that is generating log files. 
- *What does Metricbeat record?*
	- Metricbeat monitors and collects statics and metrics from the servers' system and services running on that server. 
	- Monitors the standard cpu/memory/disk/network metric data, also records:
		- Apache
		- Docker
		- Nginx
		- MySQL
		- Redis, etc

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|   Name   |           Function          | IP Address | Operating System | Application |
|:--------:|:---------------------------:|:----------:|:----------------:|:-----------:|
| Jump Box |           Gateway           |  10.0.0.4  |       Linux      |    Apache   |
| Web-1    | Web Server<br>Load Balancer |  10.0.0.5  |       Linux      |     DVWA    |
| Web-2    | Web Server<br>Load Balancer |  10.0.0.6  |       Linux      |     DVWA    |
| Web-3    | Web Server<br>Load Balancer |  10.0.0.9  |       Linux      |     DVWA    |
| ELK      |         Web Server          |  10.1.0.4  |       Linux      |    Kibana   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access ____ to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_  137.116.191.67 

Machines within the network can only be accessed by Jump Box.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name_test | Publicly  Accessible | Allowed IP Addresses |
|-----------|----------------------|----------------------|
| Jump Box  |          Yes         |    137.116.191.67    |
| Web-1     |          No          |       10.0.0.4       |
| Web-2     |          No          |       10.0.0.4       |
| Web-3     |          No          |       10.0.0.4       |
| ELK       |          No          |       10.0.0.4       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ... Install docker image docker.io, this will install docker image
- ... Install python image python3-pip, this is to install python image 


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Docker ps output](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/ELK_Output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

![Example of Syslog](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/Filebeat_System%20Syslog%20dashboard%20ECS.png)


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the hosts _____ file to include...____
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? ***The public IP of the elk server

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
