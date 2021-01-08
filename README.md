## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Stack](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/Proj_Wk13_CloudELK.PNG "ELK Stack")


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [ELK playbook file](https://media.githubusercontent.com/media/goosee007/CyberSecurity-XpreTech/main/Ansible/ELK/install-elk.yml?token=ADA4W4QGTPKMGLL42DEBGS2762DPG)

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


|   Name   |           Function          | IP Address | Operating System | Application |
|:--------:|:---------------------------:|:----------:|:----------------:|:-----------:|
| Jump Box |           Gateway           |  10.0.0.4  |       Linux      |    Apache   |
| Web-1    | Web Server<br>Load Balancer |  10.0.0.5  |       Linux      |     DVWA    |
| Web-2    | Web Server<br>Load Balancer |  10.0.0.6  |       Linux      |     DVWA    |
| Web-3    | Web Server<br>Load Balancer |  10.0.0.9  |       Linux      |     DVWA    |
| ELK      |         Web Server          |  10.1.0.4  |       Linux      |    Kibana   |

_Note: The [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) is used to add/remove values from the table_.


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access SSH to this machine is only allowed from the following IP addresses:
- _Whitelisted IP addresses:_   
	- Public IP address: 	137.116.191.67 
*(summarize firewall rules for this section, can also add screenshots for ELK & Redteam, noting which public IPs for ELK, DVWA accessiblility via rules)

RedTeam NSG Firewall rules:
![RedTeam_NSG](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/RedTeam_NSG_Rules.PNG "Redteam NSG")

ELK NSG Firewall rules: 
![ELK_NSG](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/ELK_NSG%20Rules.PNG "ELK NSG")



Machines within the network can only be accessed by Jump Box via ansible container using its private IP address 10.0.0.4. 

A summary of the access policies in place can be found in the table below.

| Name_test | Publicly  Accessible | Allowed IP Addresses |
|-----------|----------------------|----------------------|
| Jump Box  |          Yes         |    137.116.191.67    |
| Web-1     |          No          |       10.0.0.4       |
| Web-2     |          No          |       10.0.0.4       |
| Web-3     |          No          |       10.0.0.4       |
| ELK       |          No          |       10.0.0.4       |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
of its simplicity and being Agentless...

The playbook implements the following tasks:  
- _The steps of the ELK installation play:_
- ... Install docker image docker.io, this will install docker image
- ... Install python image python3-pip, this is to install python image 
- ... Install docker module, this will install the docker container
- ... Increase memory allocation, this will configure memory allocation
- ... Download and launch a docker elk container and publish ports, install elk container and configure connection ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Docker ps output](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/ELK_Output.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Monitoring | IP Addresses |
|------------|--------------|
| Jump Box   | 10.0.0.4     |
| Web-1      | 10.0.0.5     |
| Web-2      | 10.0.0.6     |
| Web-3      | 10.0.0.9     |


We have installed the following Beats on these machines:

| Monitoring | Beat Service                                        |
|------------|-----------------------------------------------------|
| Jump Box   | -Metricbeat: Apache Metric<br>-Filebeat: Apache log |
| Web-1      | -Metricbeat<br>-Filebeat                            |
| Web-2      | -Metricbeat<br>-Filebeat                            |
| Web-3      | -Metricbeat<br>-Filebeat                            |


Beats is an open platform lightweight data shippers of all kinds of data that sends the data from many machines and systems to
Logstash or Elasticsearch. 

These Beats allow us to collect the following information from each machine:  
- _For example: the kind of data each beat collects and what you would expect to see, to name a couple of them here,
E.g.,
`Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
`Filebeat System` collects Syslog logs files, syslogs are designed to monitor network devices and systems._ 
![Example of Syslog Dashboard](https://github.com/goosee007/CyberSecurity-XpreTech/blob/main/Images/Filebeat_System%20Syslog%20dashboard%20ECS.png "Syslog Dashboard")


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:   (USE THE ANSIBLE YAML FILES FOR THIS PORTION)
- Copy the _____ file to _____.
- Update the hosts _____ file to include...____
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? ***The public IP of the elk server

_As a **Bonus**, some specific commands that you will need to run to download the playbook, update the files, etc._
1. ` `
