## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/94577797/161359826-a9ecfcfb-e965-45d5-ab70-e79581c4afe7.png)






These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing is an important application that protects organizations from Denial of Service Attacks or DDoS.  They will evenly distribute traffic among all servers that are connected to it to prevent overload.  

A Jump Box allows for greater control over network access.  In order to gain access, individuals must have the IP addresses of the machines and the firewall can assist in limiting the traffic.  


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- Filebeats watch and gather logs and forwards any changes to Elasisearch.  
- Metricbeat is used for gathering data and metrics and send them to Elastisearch and Kibana

![Filebeat-Configuration](Configuration-Files/filebeat-configuration.yml)
![Filebeat-Playbook](Configuration-Files/filebeat-playbook.yml)

The configuration details of each machine may be found below.  Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System       |
|----------|----------|------------|------------------      |
| Jump Box | Gateway  | 10.0.0.8   | Linux(Ubuntu 18.04 LTS)|
| Web-1    | Server   | 10.0.0.9   | Linux(Ubuntu 18.04 LTS)|                 
| Web-2    | Server   | 10.0.0.10  | Linux(Ubuntu 18.04 LTS)|
| ELK-VM   | Server   | 10.1.0.4   | Linux(Ubuntu 18.04 LTS)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

13.72.230.119 

20.189.64.98

20.24.68.183

Machines within the network can only be accessed by the Jump Box.
Jump Box - Public IP 20.189.64.98 - Private IP: 10.0.0.8

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.8             |
| Web 1,2  | No                  | Web LB 20.24.68.183  |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

The main advantage of automating the installation process is that we could deploy several servers quick and easy without having to physically touch each server.

The playbook implements the following tasks:

- ... Install Docker.io and pip3
- ... Download and configure ELK docker container
- ... Increases VM memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![image](https://user-images.githubusercontent.com/94577797/161396703-e1d926f9-af7d-404b-83ad-bf2212487d1f.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.9
Web-2 10.0.0.10

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat watches for log files and also collect log events and data about the file system.
- Metricbeat will record metrics and data from the operating system and from services running on the server, such as uptime.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to metricbeat-config.yml to /etc/ansible/files.
- Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File.
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.

- _Which file is the playbook?
- elk-playbook.yml - used to install ELK Server.  
- Filebeat-playbook.yml - Used to install and configure Filebeat on ELK Server and DVWA servers
- metricbeat-playbook.yml - Used to install and configure Metricbeat on ELK Servers and DVWA servers
- Where do you copy it? /etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts/cfg
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? /etc/ansible/hosts is where you want each to be installed ELK-Servers or Filebeat _
- _Which URL do you navigate to in order to check that the ELK server is running?
http://publicip(elkserver):5601
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
