## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network_Diagram](https://github.com/EddyMedina/ELKproject/blob/main/Diagrams/Azure%20cloud%20diagram%20(1).jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

The Playbook is duplicated below:
 ![ELK_PLAYBOOK](https://github.com/EddyMedina/ELKproject/blob/main/Ansible/Elk_Playbook_Insatall.JPG)

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

What aspect of security do load balancers protect? Availability.

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

Which machine did you allow to access your ELK VM? The Jump BoxAnsible container  IP 10.0.0.4 

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

What is the main advantage of automating configuration with Ansible? You can automate installation for multiple VMs.

The playbook implements the following tasks:

Log in to ELK
Install Docker
Download Docker container
Resize memory
Start the container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Dockerps](https://github.com/EddyMedina/ELKproject/blob/main/Linux/Dockerps.JPG)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

Web-1 / 10.0.0.5

Web-2 / 10.0.0.6

Web-3 / 10.0.0.8

We have installed the following Beats on these machines:

Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

filebeat collects and monitors log files from protected folders and user access the shadow file.

Metricbeat Monitors resource usage and high CPU usage from bruteforce attack.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Playbooks file to the Ansible Control Node.
- Update the host file to include IP adresses
- Run the playbook, and navigate to the VMs to check that the installation worked as expected.

Note the following:

Which file is the playbook? YML file

Where do you copy it? Playbooks directory

Which file do you update to make Ansible run the playbook on a specific machine? The host file.

How do I specify which machine to install the ELK server on versus which to install Filebeat on? By Linking IP to a group.

Which URL do you navigate to in order to check that the ELK server is running? The ELKs servers public IP.

## Bonus: ### Specific commands you need to run and download the playbook.

To use the playbooks, we must perform the following steps:

-Copy the playbooks to the Ansible Control Node

-Run each playbook on the appropriate targets

The easiest way to copy the playbooks is to use Git:

$ cd /etc/ansible

$ mkdir files

$ git clone https://github.com/EddyMedina/ELKproject/blob/main/Ansible/ELKYML.txt

Move Playbooks and hosts file Into `/etc/ansible`

$ cp project-1/playbooks/* .

$ cp project-1/files/* ./files

This copies the playbook files to the correct place.

Next, you must create a hosts file to specify which VMs to run each playbook on.

Run the commands below:

$ cd /etc/ansible

$ cat > hosts <<EOF

[webservers]
10.0.0.5
10.0.0.6

[elk]
10.0.0.8

EOF

After this, the commands below will run the playbook:

$ cd /etc/ansible

$ ansible-playbook install_elk.yml elk

$ ansible-playbook install_filebeat.yml webservers

$ ansible-playbook install_metricbeat.yml webservers

To verify success, wait five minutes to give ELK time to start up.
Then, run: curl http://10.0.0.8:5601. This is the address of Kibana. If the installation succeeded, this command should print HTML to the console.

