JENKINS SETUP:
To install Jenkins on Amazon Linux 2023, you need to first launch an EC2 instance, install the required Java version, add the Jenkins repository, and then install and configure the service
====================
vim jenkins.sh
----------------------------------------------------------
#!/bin/bash
sudo dnf update y
sudo dnf install git maven -y
sudo dnf install java-17-amazon-corretto-devel -y
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo dnf install jenkins -y
sudo systemctl start jenkins
sudo systemctl status jenkins
chkconfig jenkins on
--------------------------------------------------------
chmod +x jenkins.sh
sh jenkins.sh
---------------------------------------------------
publicip:8080
cat /var/lib/jenkins/secrets/initialAdminPassword
