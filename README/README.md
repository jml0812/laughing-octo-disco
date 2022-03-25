## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

C:\Users\Joe Levesque\laughing-octo-disco\diagrams\WK13_Project_diagram.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
The load balancer ensures that owrk to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users; ourselves, will be able to connect in the first place.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems and system metrics.
Filebeat watches system logs for changes to file systems
Metricbeat records system metrics for things such as CPU usage, attempted SSH logins and sudo escalation failures

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|       Name     | Function | IP Address | Operating System |
|----------------|----------|------------|------------------|
| Jump Box       | Gateway  | 10.1.0.4   | Linux            |
| WEB 1          |Web Server| 10.1.0.5   | Linux            |
| WEB 2          |Web Server| 10.1.0.6   | Linux            |
| WK13-Project   |Monitoring| 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
24.155.65.248

Machines within the network can only be accessed by each other. The WEB 1 and WEB 2 VMs send traffic to WK13-Project

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|-------------|---------------------|----------------------|
| Jump Box    | Yes                 | 24.155.65.248        |
| WK13-Project| No                  | 10.1.0.4             |
| WEB 1       | No                  | 10.1.0.4             |
| WEB 2       | No                  | 10.1.0.4		   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this allows you to push configurations to multiple places from one host.

The playbook implements the following tasks:
-First step of playbook is to install apt packages for Docker and Python
-Second step is to increase and utilize more memory on the system
-Third step is to download and launch the elk container
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

C:\Users\Joe Levesque\Desktop\WK13_Project\README\Images\WK13_capture.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
WEB 1 10.1.0.5
WEB 2 10.1.0.6

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat: Detects changes to our filesystem. We are using it to collect Apache logs
Metricbeat: Detects changes in system metrics. We are using it to detects SSH login attempts, failed sudo attempts, and CPU/RAM stats.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbooks file to Ansible Control Node.
- Update the hosts file to include
	[webservers]
	10.1.0.5
	10.1.0.6
	[elk]
	10.0.0.4
	
- Run the playbook, and navigate to /etc/ansible to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
playbook file: install-elk1.yml copy to /etc/ansible folder
To make Ansible run the playbook on a specific machine you must update the 'Hosts' file to include the addresses of your target machine
To specify which machine to install ELK on vs Filebeat you run playbooks as such:
ansible-playbook install-elk1.yml elk
ansible-playbook filebeat-playbook.yml webservers
To verify ELK is running navagate to 'elk-server-publicip:5601/app/kibana'
