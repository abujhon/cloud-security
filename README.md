### Overview

Set up a cloud monitoring system by configuring an ELK stack server.

###Objectives

We will use the following skills and knowledge to complete the following project steps:

- Deploying containers using Ansible and Docker.
- Deploying Filebeat using Ansible.
- Deploying the ELK stack on a server.
- Diagramming networks and creating a README.



### Introduction to ELK

We'll cover what the ELK stack can do and how it works before you begin deploying it. You should be familiar with ELK from previous units.  

ELK is an acronym. Each letter stands for the name of a different open-source technology:
- **Elasticsearch**: Search and analytics engine.

- **Logstash**: Server‑side data processing pipeline that sends data to Elasticsearch.

- **Kibana**: Tool for visualizing Elasticsearch data with charts and graphs.

ELK started with Elasticsearch. Elasticsearch is a powerful tool for security teams because it was initially designed to handle _any_ kind of information. This means that logs and arbitrary file formats, such as PCAPs, can be easily stored and saved.

- After Elasticsearch became popular for logging, Logstash was added to make it easier to save logs from different machines into the Elasticsearch database. It also processes logs before saving them, to ensure data from multiple sources has the same format before it is added to the database.

- Since Elasticsearch can store so much data, analysts often use visualizations to better understand the data at a glance. Kibana is designed to make it easy to visualize massive amounts of data in Elasticsearch, and it is well known for its complex dashboards.

In summary:
- Elasticsearch is a special database for storing log data.
- Logstash is a tool that makes it easy to collect logs from any machine.
- Kibana allows analysts to easily visualize their data in complex ways.

Together, these three tools provide security specialists with everything you need to monitor traffic in any network.


#### The Beats Family

The ELK stack works by storing log data in Elasticsearch with the help of Logstash.

Traditionally, administrators would configure servers to collect logs using a built-in tool, like `auditd` or `syslog`. They would then configure Logstash to send these logs to Elasticsearch.

- While functional, this approach is not ideal because it requires administrators to collect all of the data reported by tools like `syslog`, even if they only need a small portion of it.

  - For example, administrators often need to monitor changes to specific files, such as `/etc/passwd`, or track specific information, such as a machine's uptime. In cases like this, it is wasteful to collect all of the machine's log data in order to only inspect a fraction of it.

Recently, ELK addressed this issue by adding an additional tool to its data collection suite called **Beats**.

- Beats are special-purpose data collection modules. Rather than collecting all of a machine's log data, Beats allow you to collect only the very specific pieces you are interested in.

ELK officially supports eight Beats. You will use two of them in this project:
- **Filebeat** collects data about the file system.
- **Metricbeat** collects machine metrics, such as uptime.

  - A **metric** is simply a measurement about an aspect of a system that tells analysts how "healthy" it is. Common metrics include:
    - **CPU usage**: The heavier the load on a machine's CPU, the more likely it is to fail. Analysts often receive alerts when CPU usage gets too high.

    - **Uptime**: Uptime is a measure of how long a machine has been on. Servers are generally expected to be available for a certain percentage of the time, so analysts typically track uptime to ensure their deployments meet service-level agreements (SLAs).

 Metricbeat makes it easy to collect specific information about the machines in the network. Filebeat enables analysts to monitor files for suspicious changes.

You can find documentation about the other Beats at the official Elastic.co site: [Getting Started with Beats](https://www.elastic.co/guide/en/beats/libbeat/current/getting-started.html).


#### Configuring an ELK Server
 First, we will:

    1. Create a new vNet in Azure in a different region, within the same resource group.
		2. Create a peer-to-peer network connection between their vNets.
        2. Create a new VM in the new vNet that has 2vCPUs and a minimum of 4GiB of memory.
        2. Add the new VM to Ansible’s `hosts` file in their provisioner VM.
    3. Create an Ansible playbook that installs Docker and configures an ELK container.
    4. Run the playbook to launch the container.
    5. Restrict access to the ELK VM.

 we will deploy an ELK monitoring stack within MY virtual networks. This will allow us to monitor the performance of the Web server that is running DVWA.

In particular, the ELK stack allows analysts to:
- Easily collect logs from multiple machines into a single database.

- Quickly execute complex searches, such as: _Find the 12 internal IP addresses that sent the most HTTP traffic to my gateway between 4 a.m. and 8 a.m. in April 2019._

- Build graphs, charts, and other visualizations from network data.

- We can expand this network with additional machines to generate a lot of interesting log information.


#### Filebeat setup
Second, we will:

    1. Navigate to the ELK server’s GUI to view Filebeat installation instructions.
    2. Create a Filebeat configuration file.
    3. Create an Ansible playbook that copies this configuration file to the DVWA VMs and then installs Filebeat.
    4. Run the playbook to install Filebeat.
    5. Confirm that the ELK stack is receiving logs.
    6. Install Metricbeat as a bonus activity.



#### Exploration and Diagramming
lastly, we will:
- Continue and complete the Filebeat setup and monitor data collected wether it's as you wanted, draft a network diagram, and complete a README.


### Additional Resources
- [Ansible Documentation](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html)
- [`elk-docker` Documentation](https://elk-docker.readthedocs.io/#Elasticsearch-logstash-kibana-elk-docker-image-documentation)
- [Virtual Memory Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)
- ELK Server URL: http://your-IP:5601/app/kibana#/home?_g=()
- [Docker Commands Cheatsheet](https://phoenixnap.com/kb/list-of-docker-commands-cheat-sheet)



#### Deliverables
As we work through the project, we will develop the following "deliverables".

- **Network diagram**: This document is an architecture diagram describing the topology of our network.

- **Technical brief**: Answers to a series of questions explaining the important features of the suite, completed after deploying the stack.

- **ReadMe**: (This is must have as it's to explain our work to others.) 



#### References

- More information about ELK can be found at [Elastic: The Elastic Stack](https://www.elastic.co/elastic-stack).
- More information about Filebeat can be found at [Elastic: Filebeat](https://www.elastic.co/beats/filebeat).
- To set up the ELK stack, we will be using a Docker container. Documentation can be found at [elk-docker.io](https://elk-docker.readthedocs.io/).

