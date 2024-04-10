# Dynatrace Managed Cluster Installation & maintenance

## 1) Open the license email and refer to the installation guide 
> you should have received a download link with a token generated for your license.

![installation guide](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/installationmail.png?raw=true)
> Gain root user permission using 'sudo su' command
Copy and paste YOUR license token download link command from your invitation email into the command prompt to trigger the download.
- wget -O dynatrace-managed.sh "https://mcsvc-ap-dev.dynatracelabs.com/downloads/installer/get/latest?token=AQECAHhxuvu5y6kpzj-Wo7g-6EIEO37a13xdLw9AvZ7cPYFyJQAAAIQwgYEGCSqGSIb3DQEHBqB0MHICAQAwbQYJKoZIhvcNAQcBMB4GCWCGSAFlAwQBLjARBAxEoMYsxTvY2usGE4ECARCAQNHq6L621VV0vkmiVliVqrQ9vPco93ygNTOSmwyotObUliNMfWEjyIFVO8DwEaaUWlRIe3commMMpPlXXXXXXXX"

![paste download](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/downloadDT.png?raw=true)

## 2) Check the file is downloaded using 'ls -l' command
![paste download](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/DTmanagedsh.png?raw=true)

## 3) Copy and paste the Start the installer with root rights which contains your license string as a parmeter from the email.
> 	Start the installer with root rights:
/bin/sh dynatrace-managed.sh --license Do94PnGuvVxXXXXXX 

![install configuration](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/install.png?raw=true)

> starting the installation , type in agree. 
simply press enter to accept the default directory for Dynatrace binaries (else specify another folder).
simply press enter to accept default directory for Dynatrace Data (else specify another folder).
simply press enter to accept y to keep all data in default directory.
simply press enter to n as this is a new cluster installation.
simply press enter to use 'sudo -n %CMD' for executing commands with superuser priviledges.

The installation should complete in 10 minutes and will automatically start the Cluster.
![install complete](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/installcomplete.png?raw=true)

## 4) Check Dynatrace service is running 
> go to the dynatrace binary installation folder 'cd /opt/dynatrace-managed/launcher/'
run the command './server.sh status' to check the Dynatrace server status

![install complete](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/serverstatus.png?raw=true)

> TIP: you can use -h parameter after the command in launcher folder to find the command usage.  (eg. start|stop|status|restart)
![install complete](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/launchercommands.png?raw=true)

## 5) Check system resources utilization and processes running using 'htop' command
![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/DThtop.png?raw=true)

## 6) Log into your Dynatrace server using your public ip address 
> https://<your public ip address/
eg. https://3.26.24.46/
![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/loginDT.png?raw=true)

## 7) Fill in the details to create an environment and set admin password
>Make sure you remember your admin password, keep a copy somewhere safe.
![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/createenvironment.png?raw=true)

Click Next and will route you to the familiar Dynatrace CMC screen.

![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/CMC.png?raw=true)
> Further documentation on configuring managed cluster is available 
https://docs.dynatrace.com/managed/managed-cluster

## 8) Cluster Node storage information
> Click Deployment status, select the node and click on Configure.

![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/nodestorage.png?raw=true)

## 9) Enabling Log monitoring and RUM session replay
> Click Environments, select your environment and click under capabilities section.
Log monitoring is disabled by default and can be activated.
RUM session replay is enabled by default.

![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/logmonitoring.png?raw=true)

## 10) Storage settings for data retention
> Click Environments, select your environment and click under Storage settings section.
Max limit for managed cluster is 365 days. Storage is heavily impacted by the retention time.

![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/retentiontimes.png?raw=true)

## 10) Cluster overload prevention settings
> Click Environments, select your environment and click under Storage settings section.
These settings control performance impact to Dynatrace server and is proportional to the server resources CPU/RAM/Storage availability.

![utilization](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/clusteroverload.png?raw=true)

End of document
