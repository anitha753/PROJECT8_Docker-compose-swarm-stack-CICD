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





APP :
Registration form   ---------
Enter your first name ----------------
Enter your first name-------------
Enter your last name -------------
Enter your password ---------
ReEnter your password ------------------
Enter your email ----------------------
Enter your mobile ---------
Enter your address ------------
Select your gender Male Female  ------------
Select sports you love cricket football hockey  ------
Select your Date of Birth 
dd-mm-yyyy

Select your country 
... Select your country...

Upload image   ---------  No file chosen
 RIGISTER     RESET

