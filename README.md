
 # Elk-Stack
 ## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below. 

(Elk-Stack\diagram\Elk_Stack_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the my-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly effecent, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system logs.

The configuration details of each machine may be found below.

| Name         | Function | IP Address    | Operating System |
|--------------|----------|---------------|------------------|
| The-Jump-Box | Gateway  | 10.0.0.10     | Linux            |
|              |          | 137.135.40.55 |                  |
| Web-1        | VM       | 10.0.0.7      | Linux            |
| Web-2        | VM       | 10.0.0.9      | Linux            |
| VMProject    | Elk      | 10.1.0.5      | Linux            |
|              |          | 20.185.247.69 |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the The-Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 70.171.193.188

Machines within the network can only be accessed by The-Jump-Box (10.0.0.10).

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses |
|--------------|---------------------|----------------------|
| The-Jump-Box | Yes                 |    70.171.193.188    |
|   Web-1      | No                  |    10.0.0.10         |
|   Web-2      | No                  |    10.0.0.10         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it will automate daily tasks. Freeing time to work on bigger projects.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip3
- Install Docker Module
- Increase virtual memory
- download and launch a docker web container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Elk-Stack\linux\docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 
- Web-2

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- filebeat collects and parses logs created by the system logging service of common Unix/Linux based distributions
- metricbeat fetches metrics from the Docker server

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the configuration file to your Ansible container.

    - run the command "curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml"

- Update the configuration file (filebeat-config.yml) to include your ELK server's IP address 

    - run the command "nano /etc/ansible/file/filebeat-config.yml"

    - Scroll to line #1106 and replace the IP address with the IP address of your ELK machine.
        
        - output.elasticsearch:
        - hosts: ["<your_Elks_IP>:9200"]
        - username: "elastic"
        - password: "changeme"

    - Scroll to line #1806 and replace the IP address with the IP address of your ELK machine.
        
        - setup.kibana:
        - host: "<your_Elks_IP>:5601"

- Run the playbook, (run the command "ansible-playbook filebeat-config.yml") and navigate to http://<Your_Elks_Private_IP>:5601/app/kibana#/home/tutorial/systemLogs to check that the installation worked as expected. scroll down to click "check data"


