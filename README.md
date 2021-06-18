## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.  

![Network_Diagram](Images/Network_diagram.PNG)

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

Load balancing ensures that the application will have high availability, in addition to restricting access to the network. With our load balancer, response times are minimized and maximum throughput is achieved. Efficiency and availability are two objectives that can be met here, mitigating the risks associated with denial of service attacks and being able to compensate should a server become compromised. Naturally, these risks are reduced but not completely. 

On the other hand, using our Jump-Box-Provisioner as the only virtual machine that can directly access other machines on the network ensures
access to the network is kept minimized. No other machines, beyond the webservers hosting the DVWA, can foreseeably be accessed by another outside machine.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic. Filebeat will collect the logs and forward them to the server and, similarly, Metricbeat will record the metrics and statistics and forward them to the same destination. Examples we can expect to see are system logs that pertain to the syslogs of the webservers and metrics monitoring the overall health of the containers (CPU usage, Memory usage, current status etc).

The configuration details of each machine may be found below.

|          Name         |      Function     | IP Address |     Operating System     |
|-----------------------|-------------------|------------|--------------------------|
| Jump-Box-Provisioner  | Gateway - Ansible | 10.0.0.4   | Linux (Ubuntu 20.04 LTS) |
| Web-Server1           | Web Server - DVWA | 10.0.0.5   | Linux (Ubuntu 20.04 LTS) |
| Web-Server2           | Web Server - DVWA | 10.0.0.6   | Linux (Ubuntu 20.04 LTS) |
| Web-Server3           | Web Server - DVWA | 10.0.0.10  | Linux (Ubuntu 20.04 LTS) |
| Elk-Server            | Elk Stack         | 10.1.0.4   | Linux (Ubuntu 20.04 LTS) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Personal IP Address

Machines within the network can only be accessed by SSH.
- The only machine that can directly access the ELK-Server VM is the Jump-Box-Provisioner VM with its internal IP address of 10.0.0.4. My workstation with my personal IP address, has been enabled to access Kibana using HTTP. 


A summary of the access policies in place can be found in the table below.

|          Name         |  Publicly Accessible  |                      Allowed IP Addresses                       |
|-----------------------|-----------------------|-----------------------------------------------------------------|
| Jump-Box-Provisioner  | No                    | My Personal IP Address                                          |
| Web-Server1           | Yes via load balancer | 52.151.240.129 (Load Balancer), 10.0.0.4 (Jump-Box-Provisioner) |
| Web-Server2           | Yes via load balancer | 52.151.240.129 (Load Balancer), 10.0.0.4 (Jump-Box-Provisioner) |
| Web-Server3           | Yes via load balancer | 52.151.240.129 (Load Balancer), 10.0.0.4 (Jump-Box-Provisioner) |
| Elk-Server            | No                    | My Personal IP Address, 10.0.0.4 (Jump-Box-Provisioner)         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because 
ansible allows for the continuous integration and continuous deployment regarding any current and future machines.

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

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook (.yml) file to /etc/ansible 
- Update the hosts file in the same directory to include the virtual machines by their internal IP and their respective server grouping:

  ![hosts](Images/hosts.PNG)

  *This will aid in specifying which machine to install the ELK server on versus the machines that will require Filebeat and Metricbeat
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana (Kibana) to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
