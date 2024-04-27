# Cloud Environment Preparation

## 1) Login to AWS environment  
Use the below link, make sure you're on corporate network.
> https://internal.ace-tools.dynatrace.com/upm/
Click on Assume Role , this will redirect you to AWS console
We will be using Amazon Web services to provision a host server to install Dynatrace Managed Cluster server.

## 2) Set the AWS region 
Select the region where you will be creating the host (e.g Sydney)
![Select Region](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/region.png?raw=true)

### 3) Search for EC2 service and click on the service
this will redirect you to EC2 service page
![Select EC2](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/ec2search.png?raw=true)
> Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. 

### 4) Click on Spot Request 
![Spot request](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/spotrequest.png?raw=true)
> A Spot Instance Request defines the number of instances, instance types, availability zones, and the maximum hourly rate you are willing to pay per instance. 
### 5) Request a spot instance
![Spot request](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/spotrequest2.png?raw=true)

### 7) Search for Ubuntu , and choose latest Ubuntu Server 22.04 LTS
we will be using Linux ubuntu as the operating system for our host server instance
![choose AMI](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/ubuntu2204.png?raw=true)
> An Amazon Machine Image (AMI) is used to create virtual servers (Amazon Elastic Compute Cloud or EC2 instances) in the Amazon Web Services (AWS) environment.

### 8) Click to create new key-pair
We will be creating a key pair to access the server
![new key pair](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/keypair.png?raw=true)

a separate browser tab will open for key pair creation

![create key pair](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/createkey.png?raw=true)

### 9) Type a name for key pair, select the type and file format and submit for creation

![keypair](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/cretenewkey.png?raw=true)
> A key pair is a combination of a public key that is used to encrypt data and a private key that is used to decrypt data
> - NOTE: This will trigger a download a copy of the keyfile into your local disk under the browser Download folder. DO NOT LOSE THIS KEY, as this will be used to connect to the host later.

Return to the original screen tab, click the refresh button and confirm your newly created key is selected in the dropdown box as below example.

![Spot request](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/confirmkey.png?raw=true)

### 10) Expand the Additional launch parameters tab and increase the root storage to 300 GiB
The minimum recommended storage for a managed cluster node is 300 GB

![change storage](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/storage.png?raw=true)

### 11) Click on Set maximum cost for Spot instances and set 0.15
![delete list of type](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/maxcost.png?raw=true)
> Using Spot Instances to Reduce Cluster Costs:
> The maximum spot price is the maximum price you would be willing to pay for a Spot instance hour.
> If you don't specify a maximum price, the maximum price defaults to the On-Demand price. Note that you never pay more than the Spot price that is in effect when your Spot Instance is running.

### 12) Select Manually select instance types radio button
- select all instance types listed and press delete. 
![delete list of type](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/deleteinstancetype.png?raw=true)

### 13) Once deleted click on Add instance types button
We will be adding a instance type that suits our requirements.
![add instance type](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/addinstancetype.png?raw=true)

### 14) Type t3.2xlarge in the filter screen , select the result and click Select
The minimum requirements for cluster node hardwared is 8 CPU cores and 32 GiB RAM
![t32xlarge](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/t32xlarge.png?raw=true)

### 15) Scroll down to the end of the page and press Launch
This will submit a spot instance request
![t32xlarge](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/launch.png?raw=true)

> If estimated hourly price is above $0.15 adjust max. cost in step 11)

### 16) Open the request and check the history. 
Once the status is active , it means an instance has been created.  
Click on Instances to go to the Instances page
![t32xlarge](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/active.png?raw=true)

### 17) Locate the instance from the list and set a name
Click to edit and rename the instance created to your name  
NOTE: If the status is initializing - Wait until the Status check turns to 2/2 check passed

![rename instance](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/instancename.png?raw=true)

### 18) Click on the instance ID to view the host information
Confirm the Instate state is Running
- NOTE- write down the public ip address 
We will be needing this to connect to the host 

![rename instance](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/publicIP.png?raw=true)

### 19) Go to Security tab and click on Security group to open the host security settings

![security group](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/security.png?raw=true)
> Use security groups to control the inbound and outbound traffic for associated resources.

### 19) On the security group page click on Edit inbound rules
We will be opening specific security ports to enable access connection to the host

![security group](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/inbound.png?raw=true)

### 20) On the Inbound rules page click on Add rule to open ports 80 , 22 , 443
Each rule opens a port number to allow incoming traffic to the host
> Inbound traffic rules control incoming traffic to the instances
> It helps define which types of traffic are allowed to pass through the security group
> source (0.0.0.0/0) means it allows traffic on the specified port from anywhere 

![security group](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/inbountrules.png?raw=true)


end of document
