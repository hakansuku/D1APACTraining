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
java -version 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/jdkversion.png?raw=true)

type to enable jenkins libary repository
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]  https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

```

Now update apt to get information on the newest versions of jenkin packages
```
apt update
```
then run the installation command to install jenkins
```
apt install jenkins -y
```
once installed now you can access jenkins using VM instance public address on port 8080.




