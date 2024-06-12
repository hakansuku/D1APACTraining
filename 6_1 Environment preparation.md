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






