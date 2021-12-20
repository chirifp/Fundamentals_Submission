## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![https://github.com/chirifp/Fundamentals_Submission/blob/main/Diagrams/Cloud%20Security%20-%20Network%20Diagram.drawio.png](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - - name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:

  - name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb

  - filebeat-config.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaiable, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system log.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name    | Function  | IP Address | Operating System |
|---------|-----------|------------|------------------|
| Jumpbox | Gateway   | 10.0.0.4   | Ubuntu           |
| ELKVM   | Webserver | 10.1.0.4   | Ubuntu           |
| Web1VM  | Webserver | 10.0.0.5   | Ubuntu           |
| Web2VM  | Webserver | 10.0.0.6   | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _209.171.88.184_

Machines within the network can only be accessed by Jump-box.
- _209.171.88.184_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessable | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 209.171.88.184       |
| Web-1    | No                  | 20.120.1.168 (JB)    |
| Web-2    | No                  | 20.120.1.168 (JB)    |
| ELK VM   | Yes                 | 209.171.88.184       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
servcies running can be limited, system installation and update can be streamlined, and processes become more replicable.

The playbook implements the following tasks:
- download filebeat deb
- install filebeat deb
- drop in filebeat.yml
- enable and configure system module
- set-up, start and enable  filebeat (on boot)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!https://docs.google.com/drawings/d/1kCRZqk4KGsisTGy9L4-6drXo8BKFWpployKO9FbGND4/edit?usp=sharing (Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web #1_ 10.1.0.4 
- Web #2_ 10.1.0.5

We have installed the following Beats on these machines:
- _Filebeat and Metricbeat_

These Beats allow us to collect the following information from each machine:
- Fielbeat monitors log files and event logs assocaited with traffic including orginal, destiabtion, size, type, etc. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml
- Update the hosts file to include the attribute, such as [elk], then include your destination ip of the ELK server directly
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
