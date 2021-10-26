# Prepare solr instance with Amazon Linux 2 AMI on EC2

```
#!/bin/bash
cd $HOME
pwd
sudo yum update -y
sudo yum install java-11 -y
java -version
wget http://archive.apache.org/dist/lucene/solr/7.5.0/solr-7.5.0.tgz
tar -zxvf solr-7.5.0.tgz
echo "Solr 7.5.0 Extracted"
```
## [In progress]
```
==========Solr Installation command ========

cd solr-7.5.0/bin
sudo bash ./install_solr_service.sh ../../solr-7.5.0.tgz -i /opt -d /var/solr -u solr -s solr-master -p 8983
sudo service solr-master status
```
