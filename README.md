# Elk-Stack
Contains: Ansible YAML scripts, Linux Bash scripts, cloud security network diagrams

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/seankemy/Elk-Stack/blob/main/Diagrams/RedTeam%20Cloud%20Network%20Diagram%202.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

---
- name: Configure Elk VM with Docker
  hosts: elk
  remote_user: azureuser
  become: true
  tasks:
    # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        #force_apt_get: yes
        name: docker.io
        state: present

      # Use apt module
    - name: Install python3-pip
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

      # Use pip module (It will default to pip3)
    - name: Install Docker module
      pip:
        name: docker
        state: present

      # Use command module
    #- name: Increase virtual memory
      #command: sysctl -w vm.max_map_count=262144

      # Use sysctl module
    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes

      # Use docker_container module
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        # Please list the ports that ELK runs on
        published_ports:
          -  5601:5601
          -  9200:9200
          -  5044:5044

      # Use systemd module
    - name: Enable service docker on boot
      systemd:
        name: docker
        enabled: yes

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

| Name     |  Function  | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump-Box | Gateway    | 10.0.0.6   | Linux            |
| ELK      | Monitoring | 10.1.0.4   | Linux            |
| DVWA-1   | Web Server | 10.0.0.9   | Linux            |
| DVWA-2   | Web Server | 10.0.0.10  | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 108.185.101.253

Machines within the network can only be accessed by each other.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump-Box | Yes                 | 108.185.101.253      |
| ELK      | No                  | 10.0.0.6             |
| DVWA-1   | No                  | 10.0.0.6             |
| DVWA-2   | No                  | 10.0.0.6             |


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
- DVWA-1 | 10.0.0.9
- DVWA-2 | 10.0.0.10

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects changes in the filesystem, such as Apache logs.
- Metricbeat collects changes in system metrics, such as CPU usage.


### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the Ansible control node.
- Update the hosts file to include the IP of the specific VM to run the playbook on.
- Run the playbook, and navigate to http://10.1.0.4:5601 to check that the installation worked as expected.
