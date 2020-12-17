## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
https://drive.google.com/file/d/1K5t9xBTDusYbFMzFBbRNASMYjmDjqHww/view?usp=sharing
https://github.com/bishi808/Elk-Stack-Project/blob/main/README/Images/ELK%20Diagram.png
![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network. The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users — namely, ourselves — will be able to connect in the first place.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network, as well as watch system metrics, such as CPU usage; attempted SSH logins; sudo escalation failures; etc.

The configuration details of each machine may be found below:

| Name     |   Function  |   IP Address | Operating System |
|----------|-------------|--------------|------------------|
| Jump Box | Gateway     | 10.0.0.1     |      Linux       |
| DVWA 1   | Web Server  | 10.0.0.7     |      Linux       |
| DVWA 2   | Web Server  | 10.0.0.8     |      Linux       |
| DVWA 3   | Web Server  | 10.0.0.9     |      Linux       |
| ELK      | Monitoring  | 10.1.0.4     |      Linux       |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 212.103.49.154

Machines within the network can only be accessed by each other.

A summary of the access policies in place can be found in the table below:

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |           Yes       |  212.103.49.154      |
| ELK      |           No        |  10.1.0.0/16         |
| DVWA 1   |           No        |  10.0.0.0/16         |
| DVWA 2   |           No        |  10.0.0.0/16         |
| DVWA 3   |           No        |  10.0.0.0/16         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this allows you to automatically configure many machines simultaneously thereby saving time. 

The playbook implements the following tasks:


- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.7
Web-2 10.0.0.8
Web-3 10.0.0.9

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat: Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs.
Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the playbook files to the Ansible control nodes
	-Run cd /etc/ansible to get to ansible directory
	-Create a file named “files”
	-Paste the playbook.yml in the “files” you just created 

- Update the hosts file in ansible directory to include the public ip of each DVWA and ELK server
		[webservers]
		10.0.0.7 ansible_python_interpreter=/usr/bin/python3
		10.0.0.8 ansible_python_interpreter=/usr/bin/python3
		10.0.0.9 ansible_python_interpreter=/usr/bin/python3

		[elkservers]
		10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook (ie ansible-playbook filebeat.yml) and then curl http://10.1.0.4 to check that the installation worked as expected.

