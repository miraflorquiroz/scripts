# Cloud Network

This is a collection of Linux Scripts and Ansible Scripts from my CyberClass.

Most of the scripts are used to configure cloud servers with different docker containers.

The final setup was 4 servers running vulnerable DVWA containers along with a jump box and server running an ELK stack container. 


### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Update the path with the name of your diagram] https://github.com/miraflorquiroz/scripts/blob/4b5da91b1dfcb7d0ad36f2237ca2eb3b68cc5056/Diagrams/Azures%20reource%20group.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project 1 Red-Team Network Diagrams file may be used to install only certain pieces of it, such as Filebeat.

Enter the playbook file. https://github.com/miraflorquiroz/scripts/blob/e12500c898c1e297c389a41351105501f2d32a82/Ansible/filebeat-playbook.yml 

This document contains the following details:

-Description of the Topologu
-Access Policies
-ELK Configuration
 -Beats in Use
 -Machines Being Monitored
-How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting high-traffic to the network.

-What aspect of security do load balancers protect?

Load balancing lets you evenly distribute network traffic to prevent failure caused by overloading a particular resource. This strategy improves the performance and availability of applications, websites, databases, and other computing resources. It also helps process user requests quickly and accurately. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider.

-What is the advantage of a jump box?
A jump box is a system on a network that accesses and manages all the devices in a different zone of security. It is a hardened device that spans two different security zones and enables a controlled means of access between them. Admins use the hardened server to “jump” through to access other servers. Jump-box are highly secured computers that are never used for non-administrative tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

-What does Filebeat watch for? Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

-What does Metricbeat record? Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as: Apache.

The configuration details of each machine may be found below. Note: Use the Markdown Table Generator to add/remove values from the table.

| Name                 | Function                   | IP Address | Operating System |
|----------------------|----------------------------|------------|------------------|
| Jump-Box-Provisioner | Gateway                    | 10.0.0.4   | Ubuntu LTS 18.04 |
| Elk                  |   Application Server       | 10.1.0.4   | Ubuntu LTS 18.04 |
| Web-1                |   Application Server       | 10.0.0.5   | Ubuntu LTS 18.04 |
| Web 2                |   Application Server       | 10.0.0.6   | Ubuntu LTS 18.04 |
| Web-3                |   Application Server       | 10.0.0.7   | Ubuntu LTS 18.04 |


### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 69.231.95.8 (local host)

Add whitelisted IP addresses (Jump-Box-Provisioner) 13.89.1.62
Machines within the network can only be accessed by Jump-Box-Provisioner.

Which machine did you allow to access your ELK VM? Jump-Box-Provisioner

What was its IP address? 10.0.0.4 (Private IP)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump-Box | Yes                 | 69.231.95.8.         |
| Elk-Web-1| No                  | 10.0.0.4             |
| Web-1    | No                  | 10.0.0.4             |
| Web-2.   | No                  | 10.0.0.4             |
| Web-3.   | No                  | 10.0.0.4             |

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because 

What is the main advantage of automating configuration with Ansible? Very simple to set up and use. No special coding skills are necessary to use Ansible's playbooks. Ansible lets you model even highly complex IT workflows. You can orchestrate the entire application environment no matter where it's deployed.

The playbook implements the following tasks:

In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
-First step is to SSH into the Jump-Box-Provisioner (ssh sysadmin@13.89.1.62)
-Second step is to start and attach to the ansible docker (run sudo docker start sleepy_shaw) then (sudo docker attach sleepy_shaw)
-Then I navigated to ansible directory (cd /etc/ansible/roles/) where I created the filebeat-playbook.yml
-Lastly, run the command to SSH into Elk-Web-1 to verify the server is up and running (ssh ansible@10.1.0.4)

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

!Update the path with the name of your screenshot of docker ps output

https://github.com/miraflorquiroz/scripts/blob/9fdcb772b1346edfb0ea245d00802b45daaa3ee0/Diagrams/docker%20ps.png

Target Machines & Beats
This ELK server is configured to monitor the following machines:

List the IP addresses of the machines you are monitoring 10.0.0.5 and 10.0.0.6

We have installed the following Beats on these machines:

https://github.com/miraflorquiroz/scripts/blob/9fdcb772b1346edfb0ea245d00802b45daaa3ee0/Diagrams/Filebeat%20module%20status.png
https://github.com/miraflorquiroz/scripts/blob/9fdcb772b1346edfb0ea245d00802b45daaa3ee0/Diagrams/Metricbeat%20module%20status.png

Specify which Beats you successfully installed Filebeat Metricbeat
These Beats allow us to collect the following information from each machine:

In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., Winlogbeat collects Windows logs, which we use to track user logon events, etc.
-Filebeat is used to collect log files from specific files on remote machines while Metricbeat collects machine metrics.

Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the filebeat-configuration.yml file to /etc/ansible/files
Update the filbert-configuration.yml file to include Elk private IP in lines 1106 and 1808
Run the playbook, and navigate to http://51.120.95.74:5601/app/kibana to check that the installation worked as expected.
_Answer the following questions to fill in the blanks:

_Which file is the playbook? Where do you copy it? Filebeat-playbook.yml
_Which file do you update to make Ansible run the playbook on a specific machine? etc/ansible/hosts file (IP of the Virtual Machines)
_How do I specify which machine to install the ELK server on versus which to install Filebeat on? Will need to specify a separate groups in the /etc/ansible/hosts directory. One will be assigned for webservers which contains the IP's of VM's where a filebeat will be installed. The other group will be assigned for Elkserver with VM installed with it's own IP.
_Which URL do you navigate to in order to check that the ELK server is running? http://51.120.95.74:5601/app/kibana

### As a Bonus, provide the specific commands the user will need to run to download the playbook, update the files, etc.
https://github.com/miraflorquiroz/scripts/blob/9fdcb772b1346edfb0ea245d00802b45daaa3ee0/Ansible/filebeat-playbook.yml
https://github.com/miraflorquiroz/scripts/blob/9fdcb772b1346edfb0ea245d00802b45daaa3ee0/Ansible/metricbeat-playbook.yml
