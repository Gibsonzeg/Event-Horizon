# Event-Horizon
forking and version control

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

README/Images/Azure_cloud_diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

playbook.yml

 This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
 - Beats in Use
 - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Also, one way to mitigate Dos attacks is to have multiple servers running the same website with a load balancer in front of them. Having a jump box at the front end of a network has the advantage of providing extra security in the form of two factor authentication for ssh login to the jump box, implementing a host firewall on the jump box, limiting the number of machines a jump box can access, limiting the number of connections from certain IP addresses, and limiting jump box network access with a virtual private network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics. Elk addressed this issue by adding an additional tool to its data collection suite called “Beats”. Specifically, “Filebeat” and “Metricbeat”. 
Filebeat watches for data about the filesystem.
Metricbeat records metrics about the machines in the network, such as uptime and CPU usage.
The configuration details of each machine may be found below

Name
Function
IP Address
Operating System

Jump Box
Gateway
52.188.122.248
Linux

VM 1
Server
10.0.0.6
Linux

VM 2
Server
10.0.0.7
Linux

VM 3
Server
10.0.0.8
Linux

ELK Stack
Server
10.1.0.4
Linux







### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address: (Home IP address)

Machines within the network can only be accessed by My Home IP address, including the ELK VM.

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| JumpBox   | Yes                 | Home IP              |
| VM 1      | NO                  | 10.0.0.4, Home IP    |
| VM 2      | No                  | 10.0.0.4, Home IP    |
| VM 3      | No                  | 10.0.0.4, Home IP    |
| ELK Stack | No                  | 10.0.0.4, Home IP    |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because automation eliminates the possibility of human error or any variability at all, and it is much much faster as one can literally configure potentially thousands of identical machines all at once.

The playbook implements the following tasks:

    • Install docker.io
    • Install python3-php
    • Install docker (Docker Python pip module)
    • Download and run the sebp/elk:761 container
    • Container should be started with published ports 5601:5601, 9200:9200, 5044:5044
    • 
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

    • VM 1 10.0.0.6
    • VM 2 10.0.0.7
    • VM 3 10.0.0.8
      
We have installed the following Beats on these machines:
      
    • Filebeat
    • Metricbeat

These Beats are special-purpose data collection modules that allow us to collect the following information from each machine:
      
    • Filebeat collects data about the filesystem. It reads and if interrupted, will remember the location of where it left off when the system comes back online. File beat is an amalgamation of software modules that simplify the collection, parsing, and visualization of common log formats down to a single command.
      
    • Metricbeat is a lightweight data shipper that collects and sends system and service metrics (metrics are numbers that tell you important information about a process under question). Metricbeat is installed on the different servers in your environment and used for monitoring performance, as well as different external services running on them.
        _
      
### Using the Playbook
      
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
      
    • - Copy the roles file to /etc/ansible. Update the hosts file to include the elk group, the address of the VM you want it to connect to, and the administrative user name it should use when making ssh connections.
    • - Run the playbook, and navigate to the ELK server (10.1.0.4) to check that the installation worked as expected.
