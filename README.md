# RyanF_Project1
Project files for Project 1 of my cybersecurity bootcamp

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!https://github.com/tiviator/RyanF_Project1/tree/main/Diagrams/Red_Team_VNet_RyanF.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.

 - dvwa_playbook.txt
 - elk_playbook.txt
 - filebeat_playbook.txt
 - metricbeat_playbook.txt

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
 - Beats in Use
 - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available through redundancy, in addition to restricting access to the network.
- Load balancers improve the availability of content/services that they service. Jump boxes limit the attack surface of a network by creating a choke point where a network can accessed from.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system logs.
- Filebeat watches for log events that are user-specified and forwards them to Elasticsearch.
- Metricbeat monitors operating system metrics as well as metrics from the systems and services that are running.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name              | Function    | IP Address | Operating System |
|-------------------|-------------|------------|------------------|
| Jump Box          | Gateway     | 10.0.0.4   | Linux            |
| DVWA Web Server 1 | DVWA Server | 10.0.0.7   | Linux            |
| DVWA Web Server 2 | DVWA Server | 10.0.0.6   | Linux            |
| ELK Server        | ELK Server  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK server and the Jump Box can accept connections from the Internet. Access to these machines is only allowed from the following IP addresses:
- The Workstation IP address

Machines within the network can only be accessed by the Jump Box via a ssh key that was generated in an Ansible controller on the Jump Box.
- The Workstation and the Jump Box IP addresses were whitelisted to access the ELK server.

A summary of the access policies in place can be found in the table below.

| Name             | Publicly Accessible | Allowed IP Addresses             |
|------------------|---------------------|----------------------------------|
| Jump Box         | No                  | Workstation IP Address           |
| ELK Server       | No                  | Workstation IP Address, 10.0.0.4 |
| DVWA Web Servers | No                  | 10.0.0.4                         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Deployment and provisioning of the ELK server can be performed rapidly and repeatedly if the server is malfunctioning. Additionally the deployment and provisioning can be guaranteed to succeed as long as the Ansible playbook is configured correctly.

The playbook implements the following tasks:

- Utilizes more of the VM’s available memory to handle the ELK processes
- Installs Docker
- Installs pip
- Installs the Docker Python module
- Downloads and launches a docker web container with the ELK stack
- Ensures that Docker is running and automatically starts on reboot

The following screenshot displays the result of running `sudo docker ps` after successfully configuring the ELK instance.

!https://github.com/tiviator/RyanF_Project1/tree/main/Diagrams/elk_server_provisioned.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA Web server 1
- DVWA Web Server 2

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat watches for log events that are user-specified and forwards them to Elasticsearch.
- Metricbeat monitors operating system metrics as well as metrics from the systems and services that are running.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Navigate to /etc/ansible/ and copy the playbook file to /etc/ansible/install_elk.yml with the following command:

	- curl https://raw.githubusercontent.com/tiviator/RyanF_Project1/main/Ansible/elk_playbook.yml > elk_playbook.yml

- Update the Ansible hosts file to include the IP address of the host that is to be configured by the playbook and specify the python interpreter that will be used by ansible. Add the following line under an uncommented group name:

	- [internal IP address of your elk server] ansible_python_interpreter=/usr/bin/python3

- In the [ - hosts:] field of the playbook file ensure that the group name that was uncommented in the Ansible hosts file is specified. 

- Run the playbook with the following command:
	- ansible-playbook /etc/ansible/elk_playbook.yml

- Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.
