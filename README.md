
# Project-Elk-Stack

## The Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![](https://github.com/omar-github20/Project-Elk-Stack/blob/master/Network/ELK-Stack-Project.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Cloud Security Project 1 file may be used to install only certain pieces of it, such as Filebeat.

[filebeat-playbook](https://github.com/omar-github20/Project-Elk-Stack/blob/master/Ansible/Filebeat-playbook.txt)

[filebeat-configuration](https://github.com/omar-github20/Project-Elk-Stack/blob/master/Linux/Filebeat-configuration.yml.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build

## Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

What aspect of security do load balancers protect?

-It helps rerouting traffic to different servers in the network and maximizing productivity between machines to prevent overloading traffic in the network.

 What is the advantage of a jump box?
 
 It allows you to have remote and secure access to devices in a different security zone in your network. It also provides additional layer of securty.
 
 
 Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Network and System Logs.
 
 
What does Filebeat watch for?
 -Monitors and collects log files and locations that you specify and then collects those log events and forward them to Elasticsearch or Logstash for further analysis and or indexing.
 
 What does Metricbeat record?
-Collects metrics from the operating system and services that are actively running in the server then ships them to the output specified, such as Elasticsearch or Logstash

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name           | Function      | IP Address                                  | Operating System      |
|----------------|---------------|---------------------------------------------|-----------------------|
| Jump Box       | Gateway       |(private) 10.0.1.4  (public) 52.151.10.207   | Linux                 |
|  DVWA1         |Web Server     | 10.0.3.5                                    | Linux                 |
| DVWA2          | Web Server    | 10.0.3.6                                    | Linux                 |
| ELK-VM         | Elk Server    |(private) 10.2.3.4 (public) 40.76.105.30     | Linux                 |


### Access Policies

The machines on the internal network are not exposed to the public Internet.
Only the Jump-Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:   99.123.52.226 (localhost ip address)

-A whitelist is a list of IP’s that are granted access to a certain system or protocol.
Machines within the network can only be accessed by -The- Jumping-Box Provisioner.
Which machine did you allow to access your ELK VM? What was its IP address?
-Jump-Box Provisioner (10.0.1.4)
A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible          | Allowed IP Addresses      |
|-------------|----------------------------- |---------------------------|
| Jump Box    |      YES                     |      99-123-52-226        |
| DVWA1  *    |       NO                     |      10.0.1.4             |
| DVWA2  *    |       NO                     |       10.0.1.4            |
|ELK-VM   *   |       NO                     |       10.0.1.4            |

* All this VM’s can only be accessed from the Jump-Box-Provisioner

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?-YALM is a better alternative for configuration management and automatization and it is a good way to provide large productivity gains in a very simple to use and powerful enough to automate complex tasks.

The playbook implements the following tasks:

 In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

1.First step was ssh into the jump Box. (ssh RedAdmin@52.151.10.207)
2.Then start and attached to the ansible docker. (sudo docker start/attach exciting_spence)
3.Went to /etc/ansible/roles and created the ELK playbook (Elk-Playbook.yml)
4.Ran Elk_Playbook.yml
5.Ssh into the ELK-VM to verify the server is up and running.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/omar-github20/Project-Elk-Stack/blob/master/Images/Docker-PS.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines
List the IP addresses of the machines you are monitoring
DVWA1 - 10.0.3..5
DVWA2 - 10.0.3.6

We have installed the following Beats on these machines:
Specify which Beats you successfully...

[Filebeat-configuration.yml](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Linux/Linux/Filebeat-configuration.yml.txt)

[Metricbeat-configuration.yml](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Linux/Linux/Metricbeat-configuration.yml.txt)


Filebeat:
![](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Images/Filebeat.png)




Metricbeat:
![](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Images/Metricbeat.png)


These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat is used for collecting and shipping log files, and is also the most commonly used beat. One of the facts that make Filebeat so efficient is the way it handles backpressure—so if Logstash is busy, Filebeat slows down it’s read rate and picks up the beat once the slowdown is over.

Metricbeat Is a lightweight shipper that can be install on your servers to periodically collects metrics from operating systems amd from services running in the server.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

------Filebeat------

SSH into the control node and follow the steps below:

- copy the [filebeat-configuration.yml](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Linux/Linux/Filebeat-configuration.yml.txt) file to /etc/ansible/roles/files/

- Update the [filebeat-configuration.yml](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Linux/Linux/Filebeat-configuration.yml.txt)file to include...the ELK private ip in lines 1106 and 1806
- Run the playbook, and navigate to  http://40.76.106.30:5601 (ELK public IP) to check that the installation worked as expected.

------Metricbeat-------

- copy the [metricbeat-configuration.yml](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Linux/Linux/Metricbeat-configuration.yml.txt) file to /etc/ansible/roles/files 

- update the [metricbeat-configuration.yml](https://github.com/omar-github20/ELK-Stack-Project1/blob/master/Linux/Linux/Metricbeat-configuration.yml.txt) file to include the ELK Private IP in lines 62 and 96.

-Run the playbook, and navigate to http://40.76.105.30.5601 (ELK public IP) to check that the installation worked as i expected.



Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Filebeat-playbook.yml 
Where do you copy it? - /etc/ansible/roles/     
- _Which file do you update to make Ansible run the playbook on a specific machine? The file path to run the ansible playbook on a specific machine is /etc/ansible/hosts/  
How do I specify which machine to install the ELK server on versus which to install Filebeat on? -Divide it into groups in this case webservers and elkservers which will host the ip of the VM it will install ELK to
- _Which URL do you navigate to in order to check that the ELK server is running? http://40.76.106.30:5601






_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
---
  -name: installing and launching filebeat
   hosts: webservers
   become: true
   tasks: 
   -name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.7.1-amd64.deb
    name: install filebeatdeb
    command: dpkg -i filebeat-7.7.1-amd64.deb
   -name: drop in filebeat.yml
    copy:
    src: .files/filebeat-configuration.yml
    dest: /etc/filebeat/filebeat.yml
    name: enableand configure system module 
    command: filebeat modules enable system
   -name: setup filebeat
    command: filebeat setup
   -name: start filebeat service
    command: filebeat filebeat start

 
To run the playbook: ansible-playbook filebeat-playbook.yml *
* In order to run the playbook, you have to be in the directory the playbook is at, or give the path to it (ansible-playbook /etc/ansible/roles/filebeat-playbook.yml.



