### Creating git bare repo on EC-2 for node deployment ###

================
- Amazon Linux: ec2-user
- Ubuntu: ubuntu
- Debian : admin

To access the instance through a browser, make sure you add a rule in your security group to allow port 80 and port 443 inbound.

Just create pub/private file passing passphrase  from pem and load ppk private and access using putty …cool

create git bare repo on EC-2 

Setup git deploy for AWS ec2 Ubuntu instance
-------------------------------------------------------------------

The following instructions are for setting up git deployment on an AWS ec2 ubuntu instance (or any ubuntu server for that matter). Also included are instructions for deploying to the remote server and github simultaneously.
Git deploy setup:

1. copy your public key to your ec2 instance:

     cat ~/.ssh/id_rsa.pub | ssh -i ~/.ssh/your_pemfile.pem ubuntu@your_ip_addr "cat>> .ssh/authorized_keys"
     cd ~
     mkdir ProjectDir.git && cd ProjectDir.git
     git init --bare

on remote server: create post-receive hook
--------------------------------------------------------------

$ cat > hooks/post-receive

#!/bin/sh
	echo "Stopping service"
	sudo forever stopall
	echo "Deploying to Dev ..."
	_TREE=/home/ec2-user/allakarte
	GIT_WORK_TREE=$_TREE git checkout -f
	cd $_TREE
	pwd
	echo "Installing dependencies"
	sudo npm install
	ls -la $_TREE
	echo "Starting service"
	sudo NODE_ENV=production  forever start app.js
	sudo forever list
	echo "Deployment finished."

To push to remote repo in future:

	$ git push ec2 master


 

