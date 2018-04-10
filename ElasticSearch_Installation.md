# Install and configure Elasticsearch on ubuntu 16.04

**Elasticsearch** is an open source search engine based on Lucene, developed in java. It provides a distributed and multitenant full-text search engine with an HTTP Dashboard web-interface (Kibana) and JSON documents scheme. Elasticsearch is a scalable search engine that can be used to search for all types of documents, including log file. Elasticsearch is the heart of the 'Elastic Stack' or ELK Stack.

## Getting Started

### Prerequisites

For this tutorial to work, there are a couple of requirements:
- 64-bit Ubuntu 16.04 server
- A user with sudo privileges

>All the commands in this tutorial should be run as user root or via sudo.

### Update the system and install necessary packages
```
sudo apt update && apt -y upgrade
sudo apt install apt-transport-https software-properties-common wget
```
### Install Oracle Java JDK via PPA

We will use the PPA repository maintained by the Webupd8 Team. The install script will ask you to accept the license agreement and it will download the Java archive file from the Oracle download page and set everything up for you.

To add the Webupd8 Team PPA repository, run the following commands on your server:
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt update
```
You can now install JDK8 with the following command:
```
sudo apt install oracle-java8-installer
```
To check if everything is set correctly, run:
```
java -version
```
and you should see something like the following:
```
java version "1.8.0_161"
Java(TM) SE Runtime Environment (build 1.8.0_161-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.161-b12, mixed mode)
```
## Install Elasticsearch
We will install Elasticsearch using the package manager from the Elastic repository.
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
sudo apt update
sudo apt install elasticsearch
```
## Configure Elasticsearch
Once the installation is completed, open the elasticsearch.yml file .
```
sudo nano /etc/elasticsearch/elasticsearch.yml
```
Remove the # character at the beginning of the lines for cluster.name and node.name to uncomment them, and then update their values. Your first configuration changes in the /etc/elasticsearch/elasticsearch.yml file should look like this:
```
#Set the name of your Elasticsearch Cluster
cluster.name: my-application

# Set the name of the current node
node.name: node-1

```
Start the Elasticsearch service and set it to automatically start on boot:
```
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```
By default Elasticsearch will listen on localhost:9200 .

## Make sure Elasticsearch is up and running
To check if your installation of Elasticsearch is running, you can try sending an HTTP GET request on port 9200.
``` 
curl -X GET "http://localhost:9200"
```
You should see a response similar to this:
```
{
  "name" : "node-1",
  "cluster_name" : "my-application",
  "cluster_uuid" : "K4EJ_U3aSWi09j115yQawg",
  "version" : {
    "number" : "6.2.2",
    "build_hash" : "10b1edd",
    "build_date" : "2018-02-16T19:01:30.685723Z",
    "build_snapshot" : false,
    "lucene_version" : "7.2.1",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}

```





## Webographie

[Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html)

[RoseHosting](https://www.rosehosting.com/blog/install-and-configure-the-elk-stack-on-ubuntu-16-04/)

[Statusengine](https://statusengine.org/tutorials/Elasticsearch-Xenial-Install/)


