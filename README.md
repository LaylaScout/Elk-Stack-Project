# Elk-Stack-Project
This is the Elk Stack Project done in week 13 of the cybersecurity bootcamp.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

---
  - name: installing and launching filebeat
    hosts: elk
    become: yes
    tasks:

      - name: download filebeat deb
        command: curl -L -O artifacts.elastic.co/downloads/bea>

      - name: install filebeat deb
        command: dpkg -i filebeat-7.4.0-amd64.deb

      - name: drop in filebeat.yml
        copy:
          src: /etc/ansible/files/filebeat-config.yml
          dest: /etc/filebeat/filebeat.yml

      - name: enable and configure system module
        command: sudo filebeat modules enable system

      - name: setup filebeat
        command: filebeat setup

      - name: start filebeat service
        command: service filebeat start

      - name: enable service filebeat on boot
        systemd:
          name: enable filebeat service
          enabled: yes

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
What aspect of security do load balancers protect? Load balancer are there to equally distribute the traffic to prevent the server from getting overwhelmed. They protect from DDoS attacks and allow the cybersecurity team to fix broken servers without shutting down the entire system. 

What is the advantage of a jump box?_The advantage of a jump box is to control smaller virtual machines and containers. They also allow remote connections from different networks which protects the network from attack due to key access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
-  Filebeat watches for forwarding and centralizing data.
-  Metricbeat records metrics and statistics so you can compile them into a log storing application. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|-------- ---|------------|---------------|----------------------|
| Jump Box | Gateway | 10.0.0.1    |     Linux              |
| Elk Stack |  Gateway |  10.1.0.4   |     Linux              |
| Web1     |   Gateway  |  10.0.0.6   |     Linux              |
| Web2     |    Gateway  |  10.0.0.7  |     Linux              |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: 45.27.229.149

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? Ubuntu What was its IP address?_ 45.27.229.149

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
| Elk Stack  |             Yes        |     45.27.229.149                 |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible? To be able to mass automate other machines and keep configurations the same throughout. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

Path: ~/Documents/Cybersecurity-Bootcamp/ClassWork/Unit13Project/DockerPSScreenshotProject




### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring: 10.0.0.6 and 10.0.0.7

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed: filebeats and metricbeats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat watches for forwarding and centralizing data. This data can be used to collect log events and stores them in Logstash. Metricbeat records metrics and statistics so you can compile them into a log storing application. An example of this would be Apache and other systems running on the server. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the file to _____.
- Update the  to include...
- Run the playbook, and navigate to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? The playbook is in the ansible folder and it is named install-elk-playbook
- _Which file do you update to make Ansible run the playbook on a specific machine? 
How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
In order to tell the machine which action to do, you need to log into the correct container and virtual machine. The ansible folder holding the playbooks were on elk and my vibrant_cray containers. 
- _Which URL do you navigate to in order to check that the ELK server is running? 20.122.183.105:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._anisble-playbook insta-elk-playbopok.yml
