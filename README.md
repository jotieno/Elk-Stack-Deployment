# Elk-Stack-Deployment
This is my submission to the GW CyberSecurity Bootcamp - Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/jotieno/Elk-Stack-Deployment/blob/main/Images/Project1-NetworkDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-dvwa.yml file may be used to install only certain pieces of it, such as DVWA.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load balancers enhance user experience by providing flexibility, scalability and redundancy. In addition, A jump box provides a centralized location for admins to configure the VMs in the network. It is also used for provisoning and managing the VMs which makes it easier to administer these machines from a central place. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system resources.
Filebeat monitors the log files and collects the log events. 
Metricbeat collects machine metrics, e.g uptime, CPU memory metrics etc.

The configuration details of each machine may be found below.

| Name       | Function  | IP Address | Operating System     |
|------------|-----------|------------|----------------------|
| Jump Box   | Gateway   | 10.0.0.4   | Linux                |
| Web-1      | Webserver | 10.0.0.7   | Linux (ubuntu 18.04) |
| Web-2      | Webserver | 10.0.0.8   | Linux (ubuntu 18.04) |
| Elk-Server | Monitoring| 10.1.0.4   | Linux (ubuntu 18.04) |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 40.112.62.242

Machines within the network can only be accessed via the ansible container within the Jump Box. Elk Server is the VM that contains the ELK stack and the IP address is 10.1.0.4 whose purpose is to provide services such monitor logs and metrics of the web servers via the Filebeats and Metricbeats respectively.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 40.112.62.242        |
| Elk Server | No                  | 40.122.193.5         |
| Web-1      | No                  | -                    |
| Web-2      | No                  | -                    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it expedites the process of implementing new virtual machines and eliminates the human error factor.

The install ELK-playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Increase memory
- Download and launch ELK docker and ELK container

The install metricbeat-playbook implements the following tasks:
- Download metricbeat
- Install metricbeat
- drop in metricbeat config
- Enable and configure docker module for metricbeat
- Set up metricbeat
- Start metricbeat
- Enable metricbeat on boot

The tasks to install filebeat are similar to the tasks to install metricbeat as outlined above apart from some slight differences in the config files at set up.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Docker](https://github.com/jotieno/Elk-Stack-Deployment/blob/main/Images/ELK-Docker-ps-Output.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.7
- Web-2: 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: monitors Elastic search log files, collects log events and forwards them to the monitoring cluster e.g system log events.
- Metricbeat: collects metric data from servers such as CPU usage, memory usage etc.

Filebeat successful installation!
![FileBeat](https://github.com/jotieno/Elk-Stack-Deployment/blob/main/Images/FileBeat-Screenshot.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/ansible/roles.
- Update the host file to include the IP addresses of the web servers and the IP address of the ELK server as well.
- Run the playbook, and navigate to http://[elkserver-public-ip]:5601/app/kibana to check that the installation worked as expected.

![ELK Evidence](https://github.com/jotieno/Elk-Stack-Deployment/blob/main/Images/ELK-Evidence-Kibana.png)


### Other useful commands
- sudo docker container list -a - to list the containers that have been created
- sudo docker start [name-of-container] - To start a container
- sudo docker attach [name-of-container] - To connect to the container
- nano [name-of-container] - To create/edit/update the YAML file
- ansible-playbook [name-of-container] - To run the playbook on the VMs
 