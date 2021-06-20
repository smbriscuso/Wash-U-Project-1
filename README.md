# Wash-U-Project-1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Each playbook file in ansible folder installs specified packages for example filebeat-playbook.yml installs filebeat on webservers. 


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable by protecting it from DDoS attacks, in addition to restricting heavy traffic to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logs and system health.

The configuration details of each machine may be found below.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.7   | Linux(Ubuntu)    |
| web-1     | DVWA     | 10.0.0.5   | Linux(Ubuntu)    |
| web-2     | DVWA     | 10.0.0.6   | Linux(Ubuntu)    |
| web-3     | DVWA     | 10.0.0.4   | Linux(Ubuntu)    |
| ELK-Config| ELK Stack| 10.1.0.4   | Linux(Ubuntu)    |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box-provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
201.249.75.13(Workstation IP)


Machines within the network can only be accessed by jump-box-provisioner VM with ansible container.Jump-box Public IP:138.91.249.80;Private IP:10.0.0.7.


A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      | No                  | 201.249.75.13        |
| ELK-Config-VM | No                  | 10.0.0.7             |
| web VM's      | No                  | 10.0.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because we can configure multiple servers by grouping all required commands into a single playbook file and execute it rather than configuring each one which is time consuming.


The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Increase virtual memory
- Download and launch docker ELK Container
- Enable docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 VM IP:10.0.0.5
- Web-2 VM IP:10.0.0.6
- Web-3 VM IP:10.0.0.4

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat which collects data about the file system, which specifies which hosts accessed a file, created a file or made changes to any files or their locations.
- Metricbeat which collects data about the machine, which specifies the CPU usage, Uptime and other system metrics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /etc/ansible/filebeat-playbook.yml file to /etc/ansible/files/filebeat-playbook.yml.
- Update the /etc/ansible/hosts.yml file to include 
[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3
[webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to https://publicIP_of_elk_server:5601/app/kibana to check that the installation worked as expected.
