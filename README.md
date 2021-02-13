## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network_Diagram](https://github.com/EddyMedina/ELKproject/blob/main/Diagrams/NetworkDiagram.JPG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

 ![ELK_PLAYBOOK](https://github.com/EddyMedina/ELKproject/blob/main/Ansible/ELKYML.txt)

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

- _TODO: What aspect of security do load balancers protect? Availability

 What is the advantage of a jump box? Single point of entry.

The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users — namely, ourselves — will be able to connect in the first place.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system of the VMs on the network and system metrics.

-Filebeat detects changes to the filesystem. Specifically, we use it to collect event logs.

-Metricbeat detects changes in system metrics, such as CPU usage from a brute force attack or DDOS attack.

The configuration details of each machine may be found below.


| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web-1    | Web Server | 10.0.0.5   | Linux            |
| Web-2    | Web Server | 10.0.0.6   | Linux            |
| web-3    | Web Server | 10.0.0.8   | Linux            |
| ELK      | Monitoring | 10.2.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 20.64.227.103

Machines within the network can only be accessed by the Jump box. 

- _TODO: Which machine did you allow to access your ELK VM? The Jump BoxAnsible container  IP 10.0.0.4 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Address |
|----------|---------------------|--------------------|
| Jump Box | Yes                 | 20.64.227.103      |
| Web-1    | No                  | 10.0.0.1-254       |
| Web-2    | No                  | 10.0.0.1-254       |
| web-3    | No                  | 10.0.0.1-254       |
| Elk      | No                  | 10.2.0.1-254       |

### Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because…

- _TODO: What is the main advantage of automating configuration with Ansible? You can automate installation for multiple VMs

The playbook implements the following tasks:

- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image:

Log in to ELK
Install Docker
Download Docker container
Resize memory
Start the container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Dockerps](Images/docker_ps_output.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

List the IP addresses of the machines you are monitoring:

Web-1 / 10.0.0.5
Web-2 / 10.0.0.6
Web-3 / 10.0.0.8

We have installed the following Beats on these machines:

Specify which Beats you successfully installed:

Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

filebeat collects and monitors log files from protected folders. User access the shadow file.

Metricbeat Monitors resource usage. High CPU usage from bruteforce attack.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Playbooks file to the Ansible Control Node.
- Update the host file to include IP adresses
- Run the playbook, and navigate to the VMs to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:

-Which file is the playbook? YML file

Where do you copy it? Playbooks directory

Which file do you update to make Ansible run the playbook on a specific machine? The host file.

How do I specify which machine to install the ELK server on versus which to install Filebeat on? Linking IP to a group.

Which URL do you navigate to in order to check that the ELK server is running? The ELKs servers public IP.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

