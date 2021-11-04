### Domain: Network Security

### 1.	Problem Statement
With the increase of cyber security threats and attacks all over the world, is has become crucial that organizations protect themselves from being targets to the threat actors. Confidentiality is one of the CIA triad pillars that forms the basic foundation to network security. SSH protocol also known as secure shell protocol is a method for secure remote login from one computer to another. Among its major uses include providing secure access for users and automated processes, interactive and automated file transfers, managing network infrastructure etc. Therefore, if poorly configured it can lead to major infiltration and attack from unauthorized users or threat actors. It important that unauthorized users should not be allowed to SSH into a network.

### 2.	Scenario explained
During my Cybersecurity bootcamp at GW, our 1st project involved creating and configuring an ELK stack deployment in Azure. Among the items that were configured include:
The security group, The virtual network, DVWA VMs, load balancer, the ELK network and ELK server and the jumpbox provisioner. However, during the project I noticed that one of ssh rules had been incorrectly created to allow all traffic from all ports and hosts to access the network.  As a result, this made the underlying VMs vulnerable and susceptible to attacks.

### 3.	Solution Requirements
SSH connections must be restricted to only be done via the jumpbox provisioner. A jump box provides a centralized location for admins to configure the VMs in the network. It is also used for provisioning and managing the VMs which makes it easier to administer these machines from a central place. In addition, rules must be properly created and configured to ensure that only authorized ssh connection is allowed. 

### 4.	Solution in detail
The immediate action was to ensure that the inbound and outbound rules within Azure Resource group were correctly updated.
Secondly, in order to ensure that only authorized users can ssh into the network I incorporated the use of a public key that is manually generated and added into the VMs. This added an extra layer of security and helped in providing authentication into the network. Moreover, I ensured that only the jumpbox provisioner can be used for ssh connections. A combination of all these efforts ensures that the underlying machines are protected from external forces.

In order to test my solution, I attempted to ssh into one of the DVWA VMs and received a permission denied error. I then performed ssh via the jump box provisioner using the public IP and the access was successful. I tested this by accessing the DVWA site and access was successful.

### 5.	Advantages And Disadvantages of the solution
This solution worked very well for my project because I managed to quickly resolve the issue since the number of machines in my network were minimal. It was easy to identify and address the issue promptly. I was able to quickly alleviate the issue and address it with minimal impact. However, in a large enterprise this may be a challenge. It calls for extra vigilance and proper policies put in place and adhered to accordingly. Secondly access to such rules should be limited to specific people to avoid such an occurrence. Such an attack in a large enterprise would be catastrophic.

### 6.	Monitoring Controls – Kibana Capabilities
In order to test the monitoring scenario, I incorporated the "Kibana continued" portion of the activities of the week to test the monitoring capabilities. My intention was to explore more Kibana capabilities and to understand the vulnerabilities that may be presented by unauthorized ssh access.

SSH Barrage: i performed ssh directly to one of the VMs to generate a high amount of failed SSH logins and to verify that Kibana is picking up this activity.

There were 3 initial denial attempts but 1 was successful as shown in the screenshot below. Filebeat allows for a lightweight way to forward and centralize logs and files. The GUI and infographic view tracks down curious behavior across aggregated logs.

File beat Diagram-Syslog


It also provides further analysis opportunities to check items like the sudo commands used, ssh login details among others.

FileBeat diagram 2-sudo commands

These among many other Filebeat functionalities can be very helpful to admins while monitoring the logs in their network. In addition, Metricbeat is another great monitoring tool that collects metric data from servers such as CPU usage, memory usage. This can be very handy specially to track DOS attacks.

