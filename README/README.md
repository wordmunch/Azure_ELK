## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/NetworkDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select .yml files found in Resources may be used to install only certain pieces of it, such as Filebeat.

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

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it means identical machines can be spun up quickly and easily.

The playbook implements the following tasks:
- Install Docker
- Install package managers (pip3 & docker pip)
- Install ELK image and map ports
- Enable Docker


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://drive.google.com/file/d/1xfPY2GM8Nty4NW66oF8soFfExBRNlHny/view?usp=sharing

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.9)
- Web-2 (10.0.0.10)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat ships logs and lets us keep tabs on things like system processes.
- Metricbeat uses different modules to collect metrics on services. The Docker metrics module is being to used to collect infomation like memory use for Docker containers.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the install-all-elk.yml file to /etc/ansible
- Update the /etc/ansible/hosts file to include the webservers and elk server under [webservers] and [elk] headings respectively. For instance:

```
[webservers]
10.0.0.9 ansible_python_interpreter=/usr/bin/python3
10.0.0.10 ansible_python_interpreter=/usr/bin/python3
[elk]
10.2.0.4 ansible_python_interpreter=/usr/bin/python3
```

- Run the playbook with `ansible-playbook /etc/ansible/install-elk-all.yml`, and navigate to http://13.86.88.63:5601/app/kibana (where 13.86.88.63 is the ELK server's IP) to check that the installation worked as expected.
