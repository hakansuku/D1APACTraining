# 6_1 Environment preparation

Install Jenkins in Ubuntu

> Refer to workshop 1_2 Cloud environment preparation.md to create a spot instance. 

- Create a AWS Spot instance , with the 
  OS : Ubuntu 22.04 LTS
  Instance type t3a.medium  (2 vCPU , 4 GB RAM)

- connect via SSH

Run updates to update to latest version
```
sudo su
apt update -y
apt upgrade -y
```

Install JDK 17
```
apt install openjdk-17-jdk -y
```


> Check installed java version using command : 
```
java -version
```
 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/jdkversion.png?raw=true)

type to add jenkins packages library repository for downloads

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]  https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

```

Now update apt to get information on the newest versions of jenkin packages
```
apt update

apt upgrade
```
then run the installation command to install jenkins
```
apt install jenkins -y
```

> Now check jenkins installed status by typing
```
systemctl status jenkins
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/jenkinsservice.png?raw=true)

> Once installation is confirmed now you can access jenkins using VM instance's public ip address on port 8080.
Access the initial jenkins website using your browser (eg http://<your public ip address>:8080)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/unlockJenkins.png?raw=true)

Jenkins generates a password upon installation which is required to start using jenkins.
To obtain the generated password type (Note: requires root access)
```
cat /var/lib/jenkins/secrets/initialAdminPassword
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/adminpass.png?raw=true)

> Copy the password string and enter into Administrator password field of the initial jenkins website

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/passwordcontinue.png?raw=true)

> Select Install suggested plugins to continue setup

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/suggestedplugins.png?raw=true)

> let the installation to proceed installing default plugins till completion
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/installplugins.png?raw=true)

> Create your admin user by entering the required fields with your own credentials as below and click Save and Continue.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/createadminuser.png?raw=true)

Finally, confirm the instance URL is correct and click Save and Finish to finalize the setup.
You are now ready to start using Jenkins.  Click start using Jenkins button. 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/jenkinsstartpage.png?raw=true)





