# Create your own Cluster license

Dynatrace employee you can create an account in Developement Mission Control and add internal licenses for internal testing purposes.
 
## 1) Login https://mc-dev.internal.dynatracelabs.com/ui/mc/accounts

## 2) Create an account
![Add a new account](./images/managed/addaccount.png?raw=true)

## 3) Fill in the required fields and SAVE
![enter fields](./images/managed/addaccountfields.png?raw=true)

## 4) Open up your account and Add new license
![enter image description here](./images/managed/addlicense.png?raw=true)

## 5) Check Never Expires and click on Add Quota 
![never expires and add quota](./images/managed/expiryaddquota.png?raw=true)

## 6) Add Quota - for Host units (check Unlimited box) and press Create
![Unlimited HU](./images/managed/addHU.png?raw=true)

## 7) Similarly Add quota - DEM units (check Unlimited box) and press Create
![enter image description here](./images/managed/addDEM.png?raw=true)

>Now your license is ready with unlimted HU and DEM units for testing. 
Optional: you can add Davis Data units similarly. 

## 8) Final step is to receive the license key
Select E-mail notification tab and Click on Send invitation e-mail now!
![enter image description here](./images/managed/invitationmail.png?raw=true)

You will receive instantly your Dynatrace Cluster license key in your account email inbox with instructions on how to download the latest software version and installation steps.


compare 


<!-- File: 1_1 Obtain Dynatrace License.md -->

# Chapter 1.1: Create Your Own Cluster License

As a Dynatrace employee, you can create an account in Development Mission Control to generate internal licenses for testing and workshop purposes.

### 1. Access Development Mission Control
Log in to the [Mission Control Accounts page](https://mc-dev.internal.dynatracelabs.com/ui/mc/accounts).

### 2. Create an Account
Click on **Add new account** to start the creation process.
![Add a new account](./images/managed/addaccount.png?raw=true)

### 3. Configure Account Details
Fill in the required fields with your information and click **Save**.
![enter fields](./images/managed/addaccountfields.png?raw=true)

### 4. Add a New License
Open your newly created account and click **Add new license**.
![enter image description here](./images/managed/addlicense.png?raw=true)

### 5. Set Expiration and Add Quota
Check the **Never Expires** box, then click **Add Quota**.
![never expires and add quota](./images/managed/expiryaddquota.png?raw=true)

### 6. Configure Host Units (HU)
Select **Host units**, check the **Unlimited** box, and click **Create**.
![Unlimited HU](./images/managed/addHU.png?raw=true)

### 7. Configure DEM Units
Click **Add Quota** again. Select **DEM units**, check the **Unlimited** box, and click **Create**.
![enter image description here](./images/managed/addDEM.png?raw=true)

> **Note:** Your license is now ready with unlimited HU and DEM units for testing. *(Optional: You can add Davis Data units using this same method).*

### 8. Generate the License Key
Navigate to the **E-mail notification** tab and click **Send invitation e-mail now!**
![enter image description here](./images/managed/invitationmail.png?raw=true)

You will instantly receive your Dynatrace Cluster license key in your inbox, along with instructions and a secure token to download the latest software version.

---

<!-- File: 1_2 Cloud Environment Preparation.md -->

# Chapter 1.2: Cloud Environment Preparation

We will use Amazon Web Services (AWS) to provision the host server required to install the Dynatrace Managed Cluster.

### 1. Access the AWS Environment
Ensure you are on the corporate network and navigate to the internal AWS portal:
> [Internal ACE Tools UPM](https://internal.ace-tools.dynatrace.com/upm/)

Click **Assume Role**. This will redirect you securely to the AWS Management Console.

### 2. Set the AWS Region
In the top right corner of the AWS Console, select the region where you want to deploy the host (e.g., **Sydney**).
![Select Region](./images/managed/region.png?raw=true)

### 3. Navigate to EC2
Search for **EC2** in the top search bar and click the service. Amazon Elastic Compute Cloud (EC2) provides the resizable compute capacity we need.
![Select EC2](./images/managed/ec2search.png?raw=true)

### 4. Initiate a Spot Request
In the left-hand menu, click on **Spot Requests**, then click **Request Spot Instances**. Spot instances allow us to utilize spare AWS compute capacity at a significant discount.
![Spot request](./images/managed/spotrequest.png?raw=true)
![Spot request](./images/managed/spotrequest2.png?raw=true)

### 5. Select the Operating System (AMI)
Search for `Ubuntu` and select the **Ubuntu Server 22.04 LTS** Amazon Machine Image (AMI). 
![choose AMI](./images/managed/ubuntu2204.png?raw=true)

### 6. Create a Key Pair
We must create a secure key pair to access the server via SSH.
1. Click **Create new key pair**. A new browser tab will open.
2. Enter a name for the key pair, select your preferred format (`.pem` is standard for most SSH clients), and click **Create**.
3. **Important:** This will download the key to your local machine. *Do not lose this file*, as it is the only way to log into your host later.

![new key pair](./images/managed/keypair.png?raw=true)
![create key pair](./images/managed/createkey.png?raw=true)
![keypair](./images/managed/cretenewkey.png?raw=true)

Return to the original Spot Request tab, click the **Refresh** icon, and select your new key pair from the dropdown.
![Spot request](./images/managed/confirmkey.png?raw=true)

### 7. Configure Storage
Expand the **Additional launch parameters** tab. Change the root storage to **300 GiB**. *(300 GB is the minimum recommended storage for a managed cluster node).*
![change storage](./images/managed/storage.png?raw=true)

### 8. Set Maximum Cost
Click **Set maximum cost for Spot instances** and enter **0.15**. This ensures you never pay more than $0.15 per instance hour.
![delete list of type](./images/managed/maxcost.png?raw=true)

### 9. Select the Instance Type
The minimum hardware requirement for a cluster node is 8 CPU cores and 32 GiB RAM.
1. Select the **Manually select instance types** radio button.
2. Select all default instance types listed and click **Remove**.
3. Click **Add instance types**.
4. Search for `t3.2xlarge`, select it, and click **Select**.

![delete list of type](./images/managed/deleteinstancetype.png?raw=true)
![add instance type](./images/managed/addinstancetype.png?raw=true)
![t32xlarge](./images/managed/t32xlarge.png?raw=true)

### 10. Launch and Verify the Instance
Scroll to the bottom of the page and click **Launch**.
![t32xlarge](./images/managed/launch.png?raw=true)

Open your request history. Once the status reads **Active**, your instance has been created. Click on **Instances** in the left menu to view it. 
![t32xlarge](./images/managed/active.png?raw=true)

### 11. Rename and Retrieve IP Address
Hover over the instance name field and click the pencil icon to rename the instance to your name. 
Wait until the "Status check" column reads **2/2 checks passed**.
![rename instance](./images/managed/instancename.png?raw=true)

Click the Instance ID to view its details. **Copy the Public IPv4 address** — you will need this to connect via SSH.
![rename instance](./images/managed/publicIP.png?raw=true)

### 12. Configure Security Group (Inbound Rules)
We need to open specific network ports to allow administrative and web traffic.
1. Navigate to the **Security** tab of your instance and click the **Security group** link.
2. Click **Edit inbound rules**.
3. Click **Add rule** to open the following ports to source `0.0.0.0/0` (Anywhere):
   * **Port 22** (SSH)
   * **Port 80** (HTTP)
   * **Port 443** (HTTPS)
4. Click **Save rules**.

![security group](./images/managed/security.png?raw=true)
![security group](./images/managed/inbound.png?raw=true)
![security group](./images/managed/inbountrules.png?raw=true)

---

<!-- File: 1_3 Linux Environment Fundamentals.md -->

# Chapter 1.3: Learning the Linux Environment

### 1. Install an SSH Client (Windows Users)
Download and install [MobaXterm Home Edition](https://mobaxterm.mobatek.net/download-home-edition.html), a free SSH client with a built-in X server and tabbed terminal.

### 2. Connect to the Host Server
1. Open MobaXterm and click **Session** -> **SSH**.
2. **Remote host:** Paste your AWS Public IP address.
3. **Specify username:** Type `ubuntu`.
4. Click the **Advanced SSH settings** tab.
5. Check **Use private key** and select the `.pem` file you downloaded in the previous lab.
6. Click **OK** to connect.

![Select Region](./images/managed/moba.png?raw=true)

Notice the terminal prompt format: `ubuntu@ip-172-31-30-75`. You are logged in as the standard user.
![Select EC2](./images/managed/login.png?raw=true)

### 3. Gain Root Access
Elevate your privileges to the root administrator account to install software:
```bash
sudo su
