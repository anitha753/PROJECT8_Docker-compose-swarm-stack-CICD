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



DOCKER SWARM:
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
   yum install docker -y
   systemctl start docker
   systemctl status docker
   sudo usermod -aG docker ec2-user
   docker swarm init --advertise-addr 98.81.58.237
       docker swarm join --token SWMTKN-1-5w96adwcop4fl8sf4on8cp1phr1aqhzp4fdwohdn25zrlhqq4t-8twfr69g4eithxfocnw6gi6vg 98.81.58.237:2377
   docker node ls
   docker swarm leave --force
   docker swarm join-token worker
   docker node ls
   vim index.html
   vim Dockerfile
   git --version
   git init
   git add *
   git config --global user.name "anitha"
   git config --global user.email "anithaburre@gmail.com"
   git commit -m "index.html and Dockerfile committed" .

++++++++++++++++++++++++++++++++++++++++++++++
Pipeline script
-----------
pipeline {
    agent any
    stages {
        stage(checkoutcode) {
            steps {
                git branch: 'main' , url: 'https://github.com/anitha753/PROJECT8_Docker-compose-swarm-stack-CICD.git'
            }
        }
        stage(buildimage) {
            steps {
                sh 'docker build -t $image .'
            }
        }
        stage(tagimage) {
            steps {
                sh 'docker tag $image $repo '
            }
        }
        stage(dockerlogin) {
            steps {
                sh 'docker login -u anithaburre -p $password '
            }
        }
        stage(pushimage) {
            steps {
                sh 'docker push $repo '
            }
        }
    }
}
  
  add dockerpassword in jenkins 
  --------------
  settings--->manage jenkins-->system->
  Global properties --->
  Environment variables --->
  add variable -->
  Name:  password
  Value: dockerhub password


DOCKER-COMPOSE SETUP
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
search docker-compose install --->dockerdocs --->
Docker Compose /Install/ Standalone (Legacy) -> On Linux --->
curl -SL https://github.com/docker/compose/releases/download/v5.0.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version

vim docker-compose.yml
version: '3.8'
services:
  python:
    image: anithaburre/python
    ports:
      - "81:80"
    deploy:
      replicas: 3
  aws:
     image: anithaburre/aws
     ports:
       - "82:80"
     deploy:
       replicas: 3
  devops:
     image: anithaburre/devops
     ports:
        - "83:80"
     deploy:
       replicas: 3
  linux:
     image: anithaburre/linux
     ports:
        - "84:80"
     deploy:
       replicas: 3

git add docker-com






vim index.html
<!DOCTYPE html>
<html>
  <head>
    <title>Registration form </title>
  </head>
  <body>
    <h2>Registration form </h2>
    <form>
      <label>Enter your first name</label>
      <input type="text" name="name" id="name" placeholder="Enter your first name" value=""> <br>
      <label>Enter your last name</label>
      <input type="text" name="name" id="name" value=""><br>
      <label>Enter your password</label>
      <input type="password" name="password" id="password" value=""> <br>
      <label>ReEnter your password</label>
      <input type="password" name="confirm" id="confirm" value=""> <br>
      <label>Enter your email</label>
      <input type="email" name="email" id="email" value=""><br>
      <label>Enter your mobile</label>
      <input type="tel" name="mobile" id="mobile" value=""><br>
      <label>Enter your address </label>
      <input type="textarea" row="6" col="7" ></textarea> <br>
      <label>Select your gender </label>
      <input type="radio" name="gender" id="male" value="male"><span>Male</span>
      <input type="radio" name="gender" id="female" value="female"><span>Female </span> <br>
      <label>Select sports you love</label>
      <input type="checkbox" name="a" id="a" value="cricket"><span>cricket</span>
      <input type="checkbox" name="b" id="b" value="football"><span>football </span>
      <input type="checkbox" name="c" id="c" value="hockey"><span>hockey</span> <br>
      <label>Select your Date of Birth</label>
      <input type="date" name="dob" id="dob" value=""><br>
      <label>Select your country </label>
      <select name="country" id="country">
        <option value="">... Select your country...</option>
        <option value="India">India </option>
        <option value="Afghanistan">Afghanistan </option>
        <option value="France">France </option> <br>
      </select> <br>
      <label >Upload image </label>
      <input type="file" name="fileupload" id="fileupload" value="fileupload"> <br>
      <input type="submit" name="submit" id="submit" value="Register">
      <input type="submit" name="reset" id="reset" value="Reset">
      </form>
     </body>


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

