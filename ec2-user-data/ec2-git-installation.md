## Sample user data to install Git on EC2
```
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
sudo yum update -y
sudo yum install git -y
git config --global user.name "github_username"
git config --global user.email "github_emailid"
git --version
```
