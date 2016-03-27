
## Second step: Install and configure MongoDB database ##
> Based on [http://docs.mongodb.org/ecosystem/tutorial/install-mongodb-on-amazon-ec2/](http://docs.mongodb.org/ecosystem/tutorial/install-mongodb-on-amazon-ec2/ "Installing mongodb on Amazon EC2 tutorial")

First add an entry to the local **yum** repository for MondoDB

    echo "[10gen]
    name=10gen Repository
    baseurl=http://downloads-distro.mongodb.org/repo/redhat/os/x86_64
    gpgcheck=0" | sudo tee -a /etc/yum.repos.d/10gen.repo

You must respect jump of lines in the previous code

Next, install **MongoDB** and the **sysstat** diagnostic tools:

    sudo yum -y install mongo-10gen-server mongodb-org-shell
    sudo yum -y install sysstat

We are using `/var/lib/mongo` folder to save database, log and journal data, you can another folder path.

    sudo mkdir /var/lib/mongo/data
    sudo mkdir /var/lib/mongo/log
    sudo mkdir /var/lib/mongo/journal

Set the storage items (data, log, journal) to be owned by the user (mongod) and group (mongod) that MongoDB will be starting under:

    sudo chown mongod:mongod /var/lib/mongo/data
    sudo chown mongod:mongod /var/lib/mongo/log
    sudo chown mongod:mongod /var/lib/mongo/journal

### Starting and testing MongoDB ###

Set the MongoDB service to start at boot and activate it:

    sudo chkconfig mongod on
    sudo /etc/init.d/mongod start

When starting for the first time, it will take a couple of minutes for MongoDB to start, setup it’s storage and become available. Once it is, you should be able to connect to it from within your instance:

    $ mongo
    MongoDB shell version: 2.4.3
    connecting to: test
    >

> For more information about how to configure storage setting for MongoDB on Amazon EC2, checkout [http://docs.mongodb.org/ecosystem/tutorial/install-mongodb-on-amazon-ec2/](http://docs.mongodb.org/ecosystem/tutorial/install-mongodb-on-amazon-ec2/ "Install MongoDB on Amazon EC2")

###Setup database on MongoDB  EC-2 for Mean app###

    use admin
    db.createUser(
      {
        user: "admin",
        pwd: "password",
        roles: [ { role: "root", db: "admin" } ]
      }
    );
    exit;

Shell back into mongodb with the above admin user

     mongo --port 27017 -u admin -p password --authenticationDatabase admin

Create user for a database called test and provide R/W access

        use test
        db.createUser(
            {
              user: "tester",
              pwd: "password",
              roles: [
                 { role: "read", db: "test1" },
                 { role: "read", db: "test2" },
                 { role: "read", db: "test3" },
                 { role: "readWrite", db: "test" }
              ]
            }
        );
Shell into mongodb with the test user

    mongo -u tester -p --authenticationDatabase test

