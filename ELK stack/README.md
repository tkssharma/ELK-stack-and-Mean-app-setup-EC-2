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
	cloud.aws.access_key: ********
	cloud.aws.secret_key: ***************
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
Install Elastic Search plugins 
------------------------------------------
cd /usr/share/elasticsearch/

	sudo ./bin/plugin install  lukas-vlcek/bigdesk
	sudo ./bin/plugin install  karmi/elasticsearch-paramedic
	sudo ./bin/plugin install lmenezes/elasticsearch-kopf/1.5.7
	sudo ./bin/plugin install  mobz/elasticsearch-head
	sudo ./bin/plugin install  elasticsearch/elasticsearch-cloud-aws/2.7.1

install Kibana
--------------------

	wget https://download.elasticsearch.org/kibana/kibana/kibana-4.0.1-linux-x64.tar.gz
	tar xzf kibana-4.0.1-linux-x64.tar.gz
	cd kibana-4.0.1-linux-x64
	vi config/kibana.yml 
	nohup ./bin/kibana &
	http://KIBANA_URL:5601/

install Logstash
----------------------

	wget https://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.tar.gz 
	tar zxvf logstash-1.4.2.tar.gz 
	cd logstash-1.4.2
	bin/logstash -e 'input { stdin { } } output { stdout {} }' 
	hello world 
	bin/logstash -e 'input { stdin { } } output { elasticsearch { host => localhost } }' 
	bin/logstash -e 'input { file { path => "/home/ec2-user/allakarte/logfile.txt" } } output { elasticsearch { host => "52.35.154.103" protocol => "http" } }'
	bin/logstash -e 'input { file { path => "/tmp/logfile.txt" start_position => beginning  } } output { elasticsearch { host => "52.35.154.103:9200" protocol => "http" } }'
	bin/logstash -e 'input { stdin {} }   output { elasticsearch { host => "52.35.154.103:9200" protocol => "http" } }'

contact
-----------

[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/MARTIN2.png" />](http://gennexttraining.herokuapp.com/)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/github.png" />](https://github.com/tkssharma)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/mail.png" />](mailto:tarun.softengg@gmail.com)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/linkedin.png" />](https://www.linkedin.com/in/tkssharma)
[<img src="https://s3-us-west-2.amazonaws.com/martinsocial/twitter.png" />](https://twitter.com/tkssharma)
