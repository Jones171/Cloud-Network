## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

- Images/Cloud_Network.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK-playbook file may be used to install only certain pieces of it, such as Filebeat.

  - Playbooks/filebeat-playbook.yml
  - Playbooks/install-elk.yml
  - Playbooks/metricbeat-playbook.yml
  - Playbooks/my-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly optimized, in addition to restricting access to the network.
- Load Balancers protect the Network aspect of security. The Jump box functions as a gateway, only from the  Jump box are the other VMs accessible.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system and system logs.
- FileBeat monitors logs and collects log events that we specify, then forwards those logs for further action.
- Metricbeat takes metrics and statistics from the system and the processes that are running on it.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web-1    | Web Server | 10.0.0.5   | Linux            |
| Web-2    | Web Server | 10.0.0.6   | Linux            |
| Web-3    | Web Server | 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 104.33.146.171

Machines within the network can only be accessed by the Jump Box.
- Jump Box, 10.0.0.4 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 104.33.146.171       |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- If there are multiple servers within a network that require configuration, having it automated by Ansible saves a lot of time

The playbook implements the following tasks:
- Installs docker.io also updates the cache
- Installs python3-pip
- Installs Docker Module
- Uses more memory via sysctl command
- Downloads and launches elk container wtih published ports: 5601,9200,5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- (Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.4

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects system logs, for example if you were to filter through the logs you can find the number of SSH login attempts
- Metricbeat collects CPU, memory, network, and disk statistics from the host, for example it can show the CPU usage and/or memory usage

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible.
- Update the hosts file to include the servers in need of configuration
- Run the playbook, and navigate to the servers to check that the installation worked as expected.

- The file that is the playbook are the files that have .yml at the end. You can copy it from /Playbooks/
- If you want to run any of these playbooks on a specific machine then you will have to configure the /etc/ansible/hosts file. To specify which machines to install filebeat, metricbeat, etc.
make a new group indicated by [GROUP_NAME] and place the private IPs of the machines under the group. Make sure to change the group in the playbook file itself indicated by 'hosts: '
- To check if the ELK server is running navigate to http://<ELK.VM.External.IP>:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
