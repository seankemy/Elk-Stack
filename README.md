# Elk-Stack
Contains: Ansible YAML scripts, Linux Bash scripts, cloud security network diagrams

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/seankemy/Elk-Stack/blob/main/Diagrams/RedTeam%20Cloud%20Network%20Diagram%202.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

<<<<<<< HEAD
(https://github.com/seankemy/Elk-Stack/blob/main/Ansible/install_elk_yml.txt)
(https://github.com/seankemy/Elk-Stack/blob/main/Ansible/filebeat_playbook_yml.txt)
(https://github.com/seankemy/Elk-Stack/blob/main/Ansible/metricbeat_playbook_yml.txt)
=======
![](https://github.com/seankemy/Elk-Stack/blob/main/Ansible/install_elk_yml.txt)
![](https://github.com/seankemy/Elk-Stack/blob/main/Ansible/filebeat_playbook_yml.txt)
![](https://github.com/seankemy/Elk-Stack/blob/main/Ansible/metricbeat_playbook_yml.txt)
>>>>>>> 67ae4837d4859d0a061a226eae716a87d47cbed4

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- Load balancers protect the availability aspect of security by using multiple servers to share the work of processing traffic. The advantage of a jump box is that it allows only authorized users to connect via a single gateway.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMS on the network, and system metrics.
- Filebeat watches for changes to the filesystem.
- Metricbeat records changes in system metrics.

The configuration details of each machine may be found below.

|         Name         |          Function         | IP Address | Operating System |
|----------------------|---------------------------|------------|------------------|
| Jump-Box-Provisioner | Gateway                   | 10.0.0.6   | Linux            |
| ELK-VM               | Monitoring/Configuration  | 10.1.0.4   | Linux            |
| Web-1                | Web Server/DVWA Container | 10.0.0.9   | Linux            |
| Web-2                | Web Server/DVWA Container | 10.0.0.10  | Linux            |
| Web-3                | Web Server/DVWA Container | 10.0.0.15  | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My workstation: 108.185.101.253

Machines within the network can only be accessed by the Jump-Box-Provisioner.
- My workstation is the only machine that can access the ELK VM, through my personal IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump-Box | Yes                 | 108.185.101.253      |
| ELK      | No                  | 10.0.0.6             |
| Web-1    | No                  | 10.0.0.6             |
| Web-2    | No                  | 10.0.0.6             |
| Web-3    | No                  | 10.0.0.6             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Ansible is that it increases the efficiency and accuracy when configuring multiple machines.

The playbook implements the following tasks:
- Install Docker
- Install python3
- Install Docker module
- Increase virtual memory
- Download image and launch Docker container
- Enable Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/seankemy/Elk-Stack/blob/main/Diagrams/docker_ps_output.PNG)


### Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-1 | 10.0.0.9
- Web-2 | 10.0.0.10
- Web-3 | 10.0.0.15

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects specific changes to logs in the filesystem, such as Apache logs.
- Metricbeat periodically collects changes in system metrics, such as CPU usage.


### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to the /etc/ansible/roles folder.
- Update the hosts file to include the IP addresses of webservers and elk.
- Run the playbook, and navigate to http://10.1.0.4:5601/app/kibana to check that the installation worked as expected.
<<<<<<< HEAD
=======

>>>>>>> 67ae4837d4859d0a061a226eae716a87d47cbed4
