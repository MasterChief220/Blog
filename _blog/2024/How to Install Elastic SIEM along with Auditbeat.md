---
layout: blog
title: How to Install Elastic SIEM along with Auditbeat
tags: SIEM Blue-Team
comments: true
date: 2024-10-14
---
If you’re here you probably want to set up a SIEM to gather logs from a machine. There are a couple of open-source solutions, but the ELK Stack is one of the most robust ones. But first what exactly is the ELK Stack? 

# What is ELK Stack?

The ELK Stack combines three powerful open-source tools: Elasticsearch, Logstash, and Kibana. Elasticsearch is used for fast and scalable search, Logstash collects and processes logs or data, and Kibana helps visualize the data in dashboards. ELK is used for managing large volumes of log data, helping to search, analyse, and visualize it in real time. It’s popular in monitoring, troubleshooting, and security use cases, making it easier to track performance, identify issues, and gain insights from system logs or events.

We will be using Elasticsearch and Kibana since Logstash is not needed for our purposes. We will use Auditbeat to send logs from Linux Devices. 

# Installing ElasticSearch:

First, you need any Linux Distribution to install Elasticsearch. We are using Kali Linux in the below examples but you may use Ubuntu or any other distribution.
Please note that in this example we will do a bare-metal install of the ELK stack with security disabled. I will make another tutorial which has the security features enabled later on.

We will first run the following command, which will download the Elasticsearch GPG Key, which is used to verify the authenticity of the Elasticsearch Packages. 

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```  

We will now run the following command that will install a pre-requisite package that would enable the system package manager to handle package downloads over HTTPS: 

```bash
sudo apt-get install apt-transport-https
```

Now we will run the following command which basically adds the official Elasticsearch repository to our system’s APT Sources. 

```bash
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list 
``` 

Now we will run,

```bash
sudo apt-get update && sudo apt-get install elasticsearch
```

which will update the package list and further on also install Elasticsearch.  

![Image](https://github.com/MasterChief220/Blog/blob/master/assets/images/1_eA42er5ix7bS3wcbGwVSUg.webp) 