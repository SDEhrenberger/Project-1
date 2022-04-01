## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![image](https://github.com/SDEhrenberger/Project-1/blob/9229d1a86cfce00f473be408478183c50e4b11be/Diagrams/RedTeamNetwork.png)


These files have been tested and used to generate a live ELK deployment on Azure. 
They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the playbook (.yml) file may be used to install only certain pieces of it, such as Filebeat.

  - [pentest.yml](https://github.com/SDEhrenberger/Project-1/blob/9229d1a86cfce00f473be408478183c50e4b11be/Ansible/pentest.yml.txt)  -Used to install the DVWA servers
  - [Install-Elk.yml](https://github.com/SDEhrenberger/Project-1/blob/9229d1a86cfce00f473be408478183c50e4b11be/Ansible/install-elk.yml.txt) -Used to install the elk stack
  - [Install-filebeat.yml](https://github.com/SDEhrenberger/Project-1/blob/9229d1a86cfce00f473be408478183c50e4b11be/Ansible/filebeat-playbook.yml.txt) -Used to install Filebeat on elk and DVWA servers.
  - [Install-metricbeat.yml](https://github.com/SDEhrenberger/Project-1/blob/9229d1a86cfce00f473be408478183c50e4b11be/Ansible/metricbeat-playbook.yml.txt) -Used to install Metricbeat on elk and DVWA servers.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build
 

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system files.


The configuration details of each machine may be found below.


| Name       | Function                 | IP Address | Operating System |
|------------|--------------------------|------------|------------------|
| Jump box   | Gateway                  | 10.0.0.4   | Linux            |
| Web-1      | DVWA Container           | 10.0.0.5   | Linux            |
| Web-2      | DVWA Container           | 10.0.0.6   | Linux            |
| Elk-Server | Search and Log Analyitcs | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
My Personal IP.

Machines within the network can only be accessed by Jump Box.  The only machine that had access to the Elk VM was the Jump Box.  Its IP is:
52.190.188.234


A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses     |
|------------|---------------------|--------------------------|
| Jump box   | Yes                 | My Personal IP           |
| Web-1      | No                  | 10.0.0.4, 10.1.0.4       |
| Web-2      | No                  | 10.0.0.4, 10.1.0.4       |
| Elk-Server | Yes                 | 10.0.0.4, My personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because... 

It ensures that no part of the configuration was missed.  This allows the playbook to be copied and pasted on seperate machines allowing a perfect installation every time.  This will help the machines be effiecent and the exact same each installation.


The playbook implements the following tasks:

- Install Docker
- Download the Image
- Configure the Container
- Create a playbook to install the container with Docker, Filebeat, and Metricbeat
- Run the playbook to launch the container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://github.com/SDEhrenberger/Project-1/blob/95279780db7e997e5cd8f76c13b20f8c5af11b97/Images/docker%20ps%20output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 : 10.0.0.5
Web-2 : 10.0.0.6


We have installed the following Beats on these machines:
Filebeats
Metricbeats

These Beats allow us to collect the following information from each machine:
Filebeat collects the log data for each virtual machine.  This allows us us to see information such as how many visitors you've had, as well as where they are located and if they experienced any
errors.
Metricbeat provides metric logs for each virtual machine as well as cpu usage and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the [filebeat-config.yml](https://github.com/SDEhrenberger/Project-1/blob/5a827da5ac382fa1cc75c96a5f4da1e3576d5086/Ansible/filebeat-config.yml.txt) and [metricbeat-config.yml](https://github.com/SDEhrenberger/Project-1/blob/5a827da5ac382fa1cc75c96a5f4da1e3576d5086/Ansible/install-Metric.yml.txt) file to /etc/ansible/files.
- Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.


Commands needed to run the Anisble Configuration for the Elk-Server are:

    ssh RedAdmin@JumpBox(PrivateIP)
    sudo docker container list -a - Locate the ansible container
    sudo docker start (Container_Name)
    sudo docker attach (Container_Name)
    cd /etc/ansible
    ansible-playbook elk-playbook.yml (Installs and Configures ELK-Server)
    cd /etc/ansible/
    ansible-playbook beats-playbook.yml (Installs and Configures Beats)
    Open a new browser on Personal Workstation, navigate to (ELK-Server-PublicIP:5601/app/kibana) - This will bring up Kibana Web Portal
