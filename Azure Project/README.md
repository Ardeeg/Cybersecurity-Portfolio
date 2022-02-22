## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/23627063/147436994-4ecc0669-30f0-4976-ba9b-8a6036b34187.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install_elk.yml file may be used to install only certain pieces of it, such as Filebeat.

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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.

The configuration details of each machine may be found below.

| Name      | Function    | IP Address | Operating System |
|-----------|-------------|------------|------------------|
| Jump Box  | Gateway     | 10.1.0.4   | Linux            |
| Web 1     | Web Server  | 10.1.0.5   | Linux            |
| Web 2     | Web Server  | 10.1.0.6   | Linux            |
| Web 3     | Web Server  | 10.1.0.7   | Linux            |
| ElkServer | Monitoring  | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 65.128.0.238

Machines within the network can only be accessed by other machines in the network as well as IP: 65.128.0.238 on port 5601 for the ELK server and port 80 for the Web servers through the Load Balancer with an external IP.

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses                          |
|-----------|---------------------|-----------------------------------------------|
| Jump Box  | Yes                 | 65.128.0.238                                  |
| Web 1     | No                  | 10.1.0.1-254 10.2.0.1-254                     |
| Web 2     | No                  | 10.1.0.1-254 10.2.0.1-254                     |
| Web 3     | No                  | 10.1.0.1-254 10.2.0.1-254                     |
| ElkServer | No (Yes)            | 10.2.0.1-254 10.1.0.1-254 (65.128.0.238:5601) |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it can be repeated using the same configuration files for future Elk servers or updates.

The playbook implements the following tasks:
- First the playbook installs the Docker engine on the Elk server
- Then it will install the Python 3 Module
- It will install an ELK container for Docker
- Additionally it will enable the docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/23627063/147437413-fa5b998b-3bac-4393-ab34-42b7b7a5f5e3.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web 1: 10.1.0.5
Web 2: 10.1.0.6
Web 3: 10.1.0.7

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will be used to monitor the filesystem and consolidate logs when changes occur.
- Metricbeat will monitor the system metrics involved with the operating system and services that run on the web servers.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the jump box and follow the steps below:
- Copy the playbooks (YAML files) to the jumpbox container
- Update the hosts file to include the IPs of the virtual machines the playbook will run on
- Run the playbook with the command `ansible-playbook install_elk.yml`, and navigate to http://10.2.0.4:5601/app/kibana to check that the installation worked as expected.
