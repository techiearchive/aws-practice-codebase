# User data to prepare solr instance (master and slave) with Amazon Linux 2 AMI on EC2

```
#!/bin/bash
CORE_NAME=techiearchive
cd /home/ec2-user
sudo yum update -y
sudo yum install java-11 -y
java -version
wget http://archive.apache.org/dist/lucene/solr/7.5.0/solr-7.5.0.tgz
tar -zxvf solr-7.5.0.tgz solr-7.5.0/bin/install_solr_service.sh --strip-components=2

echo "==========Solr Master instance installation ========"
cd solr-7.5.0/bin
sudo bash ./install_solr_service.sh ../../solr-7.5.0.tgz -i /opt -u solr -s solr-master -p 8983
sudo service solr-master status

echo "==== Creating solr collection ==============="
sudo su - solr -c "/opt/solr-master/bin/solr create -c $CORE_NAME -p 8983"

echo "==========Solr Slave instance installation ========"
cd solr-7.5.0/bin
sudo bash ./install_solr_service.sh ../../solr-7.5.0.tgz -i /opt -u solr -s solr-slave -p 8984
sudo service solr-slave status

echo "==== Creating solr collection ==============="
sudo su - solr -c "/opt/solr-slave/bin/solr create -c $CORE_NAME -p 8984"
```
