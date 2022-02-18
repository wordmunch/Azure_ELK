## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/NetworkDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select .yml files found in Resources may be used to install only certain pieces of it, such as Filebeat.

()

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the servers being monitored and system status.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|         Name         |        Function       |  Public IPv4  | Private IPv4 | Operating System |
|:--------------------:|:---------------------:|:-------------:|:------------:|:----------------:|
| Jump-Box-Provisioner | Gateway               | 20.127.78.17  | 10.0.0.4     | Ubuntu 18.04.6   |
| Web-1                | Webserver             | -             | 10.0.0.9     | Ubuntu 18.04.6   |
| Web-2                | Webserver             | -             | 10.0.0.10    | Ubuntu 18.04.6   |
| ELK-1                | ELK server            | 13.86.88.63   | 10.2.0.4     | Ubuntu 18.04.6   |
| LoadBalancer_01      | Load Balancer Gateway | 20.127.116.72 | -            | -                |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box-Provisioner, LoadBalancer_01, and ELK-1 machines can accept connections from the Internet. Access to Jump-Box-Provisioner and ELK-1 machines is only allowed from the following IP address:
- 98.171.77.117

All IP addresses are able to connect to the LoadBalancer_01 machine.

The to Webserver machines are only able to be accessed by machines from 10.0.0.0/24.

A summary of the access policies in place can be found in the table below.

|         Name         | Accessibility          | Protocol/Port/Service                                                        | Allowed IP Addresses       |
|:--------------------:|------------------------|------------------------------------------------------------------------------|----------------------------|
| Jump-Box-Provisioner | Single IP              | TCP/22 (SSH)                                                                 | 98.171.77.117              |
| Web-1                | Internal only          | TCP/80 (HTTP) TCP/22 (SSH)                                                   | 10.0.0.0/24                |
| Web-2                | Internal only          | TCP/80 (HTTP) TCP/22 (SSH)                                                   | 10.0.0.0/24                |
| ELK-1                | Single IP and Internal | TCP/80 (HTTP) TCP/22 (SSH) TCP/5601 (Kibana) TCP/9200 (HTTP) TCP/5044 (HTTP) | 98.171.77.117; 10.0.0.0/24 |
| LoadBalancer_01      | Public                 | TCP/80 (HTTP)                                                                | All                        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
