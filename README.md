ELK stack and Mean stack application setup on amazon EC-2 Ubuntu and AMI machine 


Elasticsearch 1.7.2 on Amazon AMI & Ubuntu
================
- Setting up EC-2 Instance 
- Elastic Search Cluster 
- Installing Logstash and Kibana
- Installing Elastic search  Plugins
- Installing Node js , git &  Mongo DB
- Setting up Test DB access for MEAN application 
-  Setting and Bare git  repo on EC-2
-  Creating git hook to deploy application 

Elasticsearch 1.7.2 on Amazon AMI
===================
sudo su

yum update -y

cd /root

wget https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.2.noarch.rpm

yum install elasticsearch-1.7.2.noarch.rpm -y

rm -f elasticsearch-1.7.2.noarch.rpm

cd /usr/share/elasticsearch/

./bin/plugin -install mobz/elasticsearch-head

./bin/plugin -install lukas-vlcek/bigdesk

./bin/plugin install elasticsearch/elasticsearch-cloud-aws/2.7.1

./bin/plugin --install lmenezes/elasticsearch-kopf/1.5.7

cd /etc/elasticsearch

nano elasticsearch.yml

Config
------
cluster.name: awstutorialseries

cloud.aws.access_key: ACCESS_KEY_HERE

cloud.aws.secret_key: SECRET_KEY_HERE

cloud.aws.region: us-east-1

discovery.type: ec2

discovery.ec2.tag.Name: "AWS Tutorial Series - Elasticsearch"

http.cors.enabled: true

http.cors.allow-origin: "*"

Commands
--------
service elasticsearch start 


Logstash 1.5.4-1
==============

Commands
--------
sudo su

yum update -y

cd /root

wget https://download.elastic.co/logstash/logstash/packages/centos/logstash-1.5.4-1.noarch.rpm

yum install logstash-1.5.4-1.noarch.rpm -y

rm -f logstash-1.5.4-1.noarch.rpm

nano /etc/logstash/conf.d/logstash.conf

Config
------
input { file { path => "/tmp/logstash.txt" } } output { elasticsearch { host => "ELASTICSEARCH_URL_HERE" protocol => "http" } }

Commands
--------
service logstash start


Kibana 4.1.2
============

Commands
--------
sudo su

yum update -y

cd /root

wget https://download.elastic.co/kibana/kibana/kibana-4.1.2-linux-x64.tar.gz

tar xzf kibana-4.1.2-linux-x64.tar.gz

rm -f kibana-4.1.2-linux-x64.tar.gz

cd kibana-4.1.2-linux-x64

nano config/kibana.yml 

Config
------
elasticsearch_url: "ELASTICSEARCH_URL_HERE"

Commands
--------
nohup ./bin/kibana &

Navigate In Browser
-------------------
http://KIBANA_URL:5601/


Elasticsearch 1.7.x on Ubuntu Machine
-------------------------------------------------------
sudo apt-get update

sudo apt-get -y install oracle-java8-installer

java -version java version "1.8.0_66" Java(TM) SE Runtime Environment (build 1.8.0_66-b17) Java HotSpot(TM) 64-Bit Server VM (build 25.66-b17, mixed mode)

Installing Elasticsearch
--------------------------------

$ wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

$ echo "deb http://packages.elastic.co/elasticsearch/1.7/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-1.7.list

$ sudo apt-get update $ sudo apt-get -y install elasticsearch

$ sudo service elasticsearch status * elasticsearch is not running

$ sudo service elasticsearch start * Starting Elasticsearch Server

Alternative Way to Install Elasticsearch
------------------------------------------------------

Alternative Way to Install Elasticsearch
There are alternative way of installing Elasticsearch. The first alternative is by downloading the .deb package directly and install using dpkg command. You don't have to add the Elasticsearch repository if you are using this method. To use this method you can use command below :

$ wget -c https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.3.deb

$ wget -c https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.3.deb.sha1.txt

$ sha1sum -c elasticsearch-1.7.3.deb.sha1.txt elasticsearch-1.7.3.deb: OK

$ sudo dpkg -i elasticsearch-1.7.3.deb

Configuring Elasticsearch
------------------------------------
sudo vi /etc/elasticsearch/elasticsearch.yml

cluster.name: Allakarte

cloud.aws.access_key: AKIAIIWR3RQ64DLXOOWA

cloud.aws.secret_key: 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

cloud.aws.region: us-west-2

discovery.type: ec2

discovery.ec2.tag.Name: "EC-2 Elastic search"

http.cors.enabled: true

http.cors.allow-origin: "*"

node.name: "node-Test"

node.master: true

node.data: true

discovery.zen.ping.multicast.enabled: false

discovery.zen.ping.unicast.hosts: ["172.31.25.97"]


Install plugins 
--------------------
cd /usr/share/elasticsearch/

sudo ./bin/plugin install  lukas-vlcek/bigdesk

sudo ./bin/plugin install  karmi/elasticsearch-paramedic

sudo ./bin/plugin install lmenezes/elasticsearch-kopf/1.5.7

sudo ./bin/plugin install  mobz/elasticsearch-head

sudo ./bin/plugin install  elasticsearch/elasticsearch-cloud-aws/2.7.1

Contact
-----------
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/MARTIN2.png" />](http://gennexttraining.herokuapp.com/)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/github.png" />](https://github.com/tkssharma)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/mail.png" />](mailto:tarun.softengg@gmail.com)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/linkedin.png" />](https://www.linkedin.com/in/tkssharma)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/twitter.png" />](https://twitter.com/tkssharma)
