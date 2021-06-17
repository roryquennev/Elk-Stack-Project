## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.  

![Network-Diagram](Images/Network-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will have high availability, in addition to restricting access to the network. In addition, the load utilizing the load balancer ensures that server response times are minimized and achive maximum throughput. Efficiency and availability are two objectives that can be met here.

On the other hand, using our Jump-Box-Provisioner as the only virtual machine that can directly access other machines on the network 
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.

|          Name         |           Function         | IP Address |     Operating System     |
|-----------------------|----------------------------|------------|--------------------------|
| Jump-Box-Provisioner  | Gateway - Docker - Ansible | 10.0.0.4   | Linux (Ubuntu 20.04 LTS) |
| Web-Server1           | Web Server - Docker - DVWA | 10.0.0.5   | Linux (Ubuntu 20.04 LTS) |
| Web-Server2           | Web Server - Docker - DVWA | 10.0.0.6   | Linux (Ubuntu 20.04 LTS) |
| Web-Server3           | Web Server - Docker - DVWA | 10.0.0.10  | Linux (Ubuntu 20.04 LTS) |
| Elk-Server            | Elk Stack                  | 10.1.0.4   | Linux (Ubuntu 20.04 LTS) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Personal IP Address

Machines within the network can only be accessed by SSH.
- The only machine that can directly access the ELK-Server VM is the Jump-Box-Provisioner VM with its internal IP address of 10.0.0.4. My workstation, using my personal IP address, has been enabled to access Kibana using HTTP. 


A summary of the access policies in place can be found in the table below.

|          Name         |  Publicly Accessible  |                      Allowed IP Addresses                       |
|-----------------------|-----------------------|-----------------------------------------------------------------|
| Jump-Box-Provisioner  | No                    | My Personal IP Address                                          |
| Web-Server1           | Yes via load balancer | 52.151.240.129 (Load Balancer), 10.0.0.4 (Jump-Box-Provisioner) |
| Web-Server2           | Yes via load balancer | 52.151.240.129 (Load Balancer), 10.0.0.4 (Jump-Box-Provisioner) |
| Web-Server3           | Yes via load balancer | 52.151.240.129 (Load Balancer), 10.0.0.4 (Jump-Box-Provisioner) |
| Elk-Server            | No                    | My Persnal IP Address, 10.0.0.4 (Jump-Box-Provisioner)          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker-ps-output](Images/docker-ps-output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

|         Name          | IP Address |   
|-----------------------|------------|
| Web-Server1           | 10.0.0.5   |
| Web-Server2           | 10.0.0.6   | 
| Web-Server3           | 10.0.0.10  | 


We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
