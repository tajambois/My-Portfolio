# My-Portfolio
Folder of my personal work and examples
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://github.com/tajambois/My-Portfolio/blob/main/Diagrams/Elk_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the elk-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.
(https://github.com/tajambois/My-Portfolio/blob/main/Ansible/elk-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly fault tolerant, in addition to restricting traffic to the network.
- Load balancers increase the difficulty of a DDoS attack, usiong reporting a security measures set by the administrators. The andvantage of a jumpbox is the singular source of entry into enviroment, via a whitelisted IP.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

- Filebeat is a lightweight shipper for passing and centralizing log data. When installed on these servers, Filebeat monitors the log files, collects log events, and forwards them either to Kibana for indexing.
- Metricbeat will be used will to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name   | Function  | IP Address              | Operating System |
|--------|-----------|-------------------------|------------------|
| NU-VM  | Jump Box  | 104.208.33.190/10.0.0.8 | Ubuntu           |
| Web-1  | Webserver | 10.0.0.7                | Ubuntu           |
| Web-2  | Webserver | 10.0.0.6                | Ubuntu           |
| Elk-VM | Elk Stack | 138.91.197.195/10.1.0.4 | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the NU-VM machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-	24.13.45.184

Machines within the network can only be accessed by SSH.
-NU-VM 10.0.0.8

A summary of the access policies in place can be found in the table below.

| Name   | Publicly Accessible | Allowed IP Addresses |
|--------|---------------------|----------------------|
| NU-VM  | Yes - Whitelist     | 24.13.45.184         |
| Web-1  | NO - Port 80        | 10.0.0.8             |
| Web-2  | NO - Port 80        | 10.0.0.8             |
| Elk-VM | Yes - Port 5601     | 24.13.45.184         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It allows me to mass deploy to several machines efficiently. This will create a uniform network.

The playbook implements the following tasks:
- Installed Docker
- Install pip3
- Install Docker Python Module
- Configured the target VM (the machine being configured) to use more memory.
- Download and Launch Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

  ![Docker PS](https://github.com/tajambois/My-Portfolio/blob/main/Images/Docker%20PS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:
- FileBeat

FileBeat allows us to collect the following information from each machine:
- System logs

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config file to /etc/ansible/files. Run: https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml
- Update the config file to include the IP address of my webservers. in the playbook, ensure host is set to correct group.
- Run the playbook, and navigate to http://138.91.197:5601/app/kibana to check that the installation worked as expected.
