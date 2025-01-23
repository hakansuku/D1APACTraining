# 8_1_1 Prepare Coding Environment

- Prepare a development ubuntu VM instance
  You will start with a spot instance .  This comes to be cheaper for our purpose
  
- Choose VM OS Ubuntu 24.04 image
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/spot1.png?raw=true)

- We will set the max cost of the spot instance to be $0.03 per hour.  (Currently is at $0.0245 for t2.medium size). 
  Means if demand goes and price goes above $0.03 per hour we'll lose the VM instance. 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/spotprice.png?raw=true)

- Choose Manually select instance type. Select and delete all types of VM in the list. Simply add t2.medium type instance to the list. 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/vmtype.png?raw=true)

- At the bottom press Done button.   This will create a spot VM instance for our test purpose.
  
> Go to AWS EC2 instance tab and observe new instance being created. 

- Open the newly created instance and select security tab mid-page.
- Edit Inbound port rules and add port 8000 and port 8080
> Port 8080 will be used for VS code server.
> Port 8000 will be used at later stage for Laravel

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/inbountport.png?raw=true)

# 8_1_2  Installing Visual Studio code-server
- SSH to your server using the public address of your EC2 instance

