# 9_1_1 Prepare Coding Environment 

## In this tutorial we will spin a Ubuntu linux AWS::EC2 instance , we will then install Visual studio code-server 

- Prepare a development ubuntu VM instance
  You will start with a spot instance .  This comes to be cheaper for our purpose
  
- Choose VM OS Ubuntu 24.04 image
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/spot1.png?raw=true)

- We will set the max cost of the spot instance to be $0.03 per hour.  (Currently is at $0.0245 for t2.medium size). 
  Means if demand goes and price goes above $0.03 per hour we'll lose the VM instance. 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/spotprice.png?raw=true)

- Choose Manually select instance type. Select and delete all types of VM in the list. Simply add t2.medium type instance to the list. 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/vmtype.png?raw=true)

- At the bottom of page press LAUNCH button.   This will create a spot VM instance for our test purpose.
  
> Go to AWS EC2 instance tab and observe new instance being created. 

- Open the newly created instance and select security tab mid-page.
- Edit Inbound port rules and add port 8000 and port 8080
> Port 8080 will be used for VS code server.
> Port 8000 will be used at later stage for Laravel

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/inbountport.png?raw=true)


# 9_1_2  Installing Visual Studio code-server
### Connecting to your ubuntu instance
- Step 1: Connect to SSH terminal of your new server with Mobaterm. Use the public address of your EC2 instance with username ubuntu and your AWS public key.
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/mobaterm.png?raw=true)

### Upgrade system libraries
- Gain root access and update the ubuntu system libraries using the below linux commands.
  
```
sudo su
apt update
apt upgrade -y
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/mobaterm2.png?raw=true)

### Downloading VS code-server installer 

- Download VS code-server
```
curl -fOL https://github.com/coder/code-server/releases/download/v4.96.4/code-server_4.96.4_amd64.deb
```
> you can check for latest release from https://github.com/coder/code-server/releases/

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/codeserver.png?raw=true)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/cs2.png?raw=true)

- Install code-server package with below command:
```
dpkg -i code-server_4.96.4_amd64.deb
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/installcs.png?raw=true)




- Enable code-server as a service
```
sudo systemctl enable --now code-server@ubuntu

```
> above this will create a file in  directory in /home/ubuntu/.config/code-server/config.yaml

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/enablecs.png?raw=true)

- Modify binding address and password in /home/ubuntu/.config/code-server/config.yaml
- Edit this file and change binding address and password as below

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/changeip3.png?raw=true)

- Now restart code-server service for the modifications to reflect into the service.
  
```
systemctl restart code-server@ubuntu
```

- Open a browser, use the EC2 instance public address with port 8080 (eg http://<EC2instance-public ip>:8080
> login with your password you set in config.yaml

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/welcomecs.png?raw=true)

- You can now use VS code to start coding 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/loginok.png?raw=true)

End of document
