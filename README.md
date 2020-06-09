## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/Network_Topology.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, *the roles in the YAML file project1-playbook.yml* may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly *available*, in addition to restricting *access* to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the *file system* and system *metrics*.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name          | Function         | Ip Address             | Operating System   |
|---------------|------------------|------------------------|--------------------|
| ProjJumpBox   | Gateway          | 51.173.46.228 10.2.0.4 | Linux Ubuntu 18.04 |
| ProjElkServer | ELK Stack Server | 52.175.244.90 10.2.0.5 | Linux Ubuntu 18.04 |
| ProjDVWA-1    | DVWA Web Server  | 10.2.0.6               | Linux Ubuntu 18.04 |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the *Jump Box* machine can accept SSH connections from the Internet. Access to this machine is only allowed from the following IP addresses:
70.95.190.26

Machines within the network can only be accessed by *SSH from the Jump Box*.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible     | Allowed IP Addresses                                    |
|---------------|-------------------------|---------------------------------------------------------|
| ProjJumpBox   | No                      | 70.95.190.26 (22)                                       |
| ProjElkServer | No                      | 70.95.190.26 (5601) 10.2.0.4 (22) 10.2.0.6 (5044, 9200) |
| ProjDVWA-1    | Yes, via load balancer. | 10.2.0.4 (22) Internet (80)                             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because *the configuration process can be easily replicated*.

The *ELK server role in the* playbook implements the following tasks:
- Set max map count. Prevent ELK from encountering errors.
- Download and install docker.io
- Download and install python-pip
- Use pip to install the docker python module
- Download and install the ELK container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/ELK_Stack.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
*10.2.0.6*

We have installed the following Beats on these machines:
*Filebeats*
*Metricbeats*

These Beats allow us to collect the following information from each machine:
Filebeat - Collects log data about changes to the file system. The logs will include information about which files have been changed and when those changers were made.
Metricbeat - Collects log data about systeme usage information. The logs include information on CPU usage, memory usage, disk IO, and network IO statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the *project1-playbook.yml* file to */etc/ansible*.
- Copy the contents of the roles directory into /etc/ansible/roles
- Copy the contents of the files directory into /etc/ansible/files
- Update the *hosts* file to include *the private ip addresses of the webservers and the elk server*.
- Update the ansible.cfg file so that remote_user= is set to a user with ssh access to the ELK server and webservers.
- Run the playbook with *ansible-playbook project1-playbook.yml*, and navigate to *http://[ELK server IP address]:5601* to check that the installation worked as expected.
