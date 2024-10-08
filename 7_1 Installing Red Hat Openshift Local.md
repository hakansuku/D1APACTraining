# Install Red Hat OpenShift Local
Create a minimal cluster on your desktop/laptop for local development and testing.

#### In this workshop, we will be installing openshift local 

- You will download and install Openshift in your laptop.

> Openshift Container Platform pre-requisite :

- 4 physical CPU cores
- 9 GB of free RAM memory
- 35 GB of storage space

Login to Redhat via https://sso.redhat.com/
if you don't have an account please register and create one. 

## Download Openshift Local
> URL: https://console.redhat.com/openshift/create/local

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OCP/download.png?raw=true)

> - Download and run the installer 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OCP/crcinstaller.png?raw=true)

accept the license agreement and press next to install till finish. 
Reboot for the changes to take effect. 

> type cmd (administrator rights) to bring up the command prompt

- type
```
crc setup new cluster
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OCP/crcsetup.png?raw=true)

- type below command to start the cluster
```
crc start
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OCP/crcstart.png?raw=true)

use the Url , to access the cluster management console.

> end of document

