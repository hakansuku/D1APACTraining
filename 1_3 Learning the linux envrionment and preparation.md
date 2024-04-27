# Learning the Linux Environment and preparation

## 1) Install an SSH client (windows users) 
Use the below link, to download and install Mobaxterm free client
We will be using this tool to establish an SSH connection to the AWS instance host server.
> https://mobaxterm.mobatek.net/download-home-edition.html
>Free X server for Windows with tabbed SSH terminal, telnet, RDP, VNC and X11-forwarding - Download.

## 2) Create an SSH session and connect to the host server
> 1. Click Session 
> 2. Select SSH 
> 3. Input Host public IP address
> 4. Set specify user: ubuntu
> 5. Click Advanced SSH settings tab 
> 6. Set Use private key - select the key pair .pem file downloaded from previous workshop
Press OK
![Select Region](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/moba.png?raw=true)

### 3) SSH Login (Secure SHell) as ubuntu user
this will redirect you to EC2 service page
![Select EC2](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/login.png?raw=true)
> SSH (Secure Shell) enables logging in to and running terminal sessions on remote systems.
> NOTICE: ubuntu (user) at the beginning of the shell prompt followed by ip-172-31-30-75(@server name)

### 4) Gain Root access using 'sudo su' command
Type 'sudo su' to gain root user access (root = administrator)
NOTICE how the user changes from ubuntu to root in the command prompt
![Spot request](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/sudosu.png?raw=true)
> - The 'pwd' (print working directory) command in Linux is a built-in command that displays the full pathname of the current directory.
> - 'ls' is a Linux shell command that lists directory contents of files and directories. '-l' option tells ls command to use a long listing format, providing additional information about directory contents.
> - 'sudo' is a command-line utility to temporarily grant users or user groups privileged access to system resources so that they can run commands that they cannot run under their regular accounts

### 5) Download updates for OS package in linux system using 'apt update' command
With root permission, type apt update and press enter.
![download updates](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/aptupdate.png?raw=true)
> The sudo apt update command downloads the updates for each outdated package and dependency on your system.

### 7) Install downloaded updates for OS package in linux system using 'apt upgrade' command

![instal updates](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/aptupgrade.png?raw=true)
> The sudo apt upgrade command installs downloaded updates for each outdated package and dependency on your system. Hence need to run 'apt update' command prior 'apt upgrade' command.

![press yes](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/aptupgradeyes.png?raw=true)
>Note: type y when prompted to continue the upgrade

![press oks](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/kernel.png?raw=true)
> When prompted for New Kernel simply press enter to continue.
Similarly, press enter when prompted to restart services.

### 9) Check host storage using 'df -h' command
> The df command displays information about total space and available space on a file system. The FileSystem parameter specifies the name of the device on which the file system resides, the directory on which the file system is mounted, or the relative path name of a file system.

![keypair](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/df.png?raw=true)
> The -h or --human-readable option is passed to the df command to show you Linux filesystem disk space usage in a human-readable format.
Notice how / (root) directory total size is 291GiB , 2.2GiB is being used and 289GiB is available.  This also means that any sub-directories are able to use 289 GiB available disk space.

### 10) Check host's CPU,Memory and process utilization using 'htop' command in linux
> .htop command in Linux system is a command line utility that allows the user to interactively monitor the system’s vital resources or server’s processes in real time. 
Notice the 0-7 represents real time CPU utilization
Mem is the RAM utilization currently using 281MiB out of 31GiB
List of processes running below and information on commands running the each process.

![htop](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/htop.png?raw=true)

End Of Workshop
# APPENDIX

### OPTIONAL) ONLY REQUIRED if the server DOES NOT have enough disk space : 
In such scenario you need to add additional disk space. The following steps are required to add additional volume disk to the host.
### A) Check availability zone under Networking tab
> remember the availability zone as we need to create a disk volume in the same availability zone as the host

![availability zone](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/hostavailability.png?raw=true)
### Go to Volumes page and click on Create volume
![create volume](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/createvolume.png?raw=true)
### Go to Volumes page and click on Create volume
> - Set size to 300 GiB
- Select the availability zone same as the host availability zone

![create volume 300G](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/createvolume300G.png?raw=true)
> AWS Availability Zone (AZ) is a distinct location within a Region that is insulated from failures in other Availability Zones, and provides inexpensive, low-latency network connectivity to other Availability Zones in the same Region.

Click on CREATE VOLUME button at the end of the page.
### Check the volume ID, select the created volume and click on attach volume
> Note : Attach volume is grayed out if the volume is initializing status. Wait until status changes to Available.
![volume successful](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/volumesuccessful.png?raw=true)

### Attach the volume to the host server
> - Set size to 300 GiB
- Select the availability zone same as the host availability zone

![create volume 300G](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/attachvolumesde.png?raw=true)
Click on Attach volume button
> When you attach a volume to your instance, you include a device name for the volume. This device name is used by Amazon EC2. The block device driver for the instance assigns the actual volume name when mounting the volume, and the name assigned can be different from the name that Amazon EC2 uses.

### Check attached storage block using 'lsblk' command
Notice nvme1n1 disk has been added to the host.  Also note that there is no mountpoint assigned
![create volume 300G](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/lsblk.png?raw=true)
> The 'lsblk' stands for 'list block devices', and as the name suggests, it is used to list out all block devices in a tree-like format. This powerful command can help you gather comprehensive information about each block device connected to your Linux system, including the disk partitions and their respective sizes.

### Create a file system on new added storage block (nvme1n1) using 'mkfs -t xfs /dev/nvme1n1' command
> -t xfs: specifies the XFS file system 
/dev/nvme1n1: specifies the device (disk)

![create volume 300G](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/mkfs.png?raw=true)
> The mkfs command makes a new file system on a specified device. The mkfs command initializes the volume label, file system label, and startup block. Note: The file system is created with the setgid (set group ID) bit enabled.

### Create a directory (/mynewdisk) to act as the mountpoint and mount the disk
- create a directory using 'mkdir /mynewdisk' command
- mount the disk using 'mount /dev/nvme1n1 /mynewdisk' command

![create volume 300G](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/mount.png?raw=true)
> Use the mkdir command to create one or more directories specified by the Directory parameter.
> The mount command is used to mount the filesystem found on a device to big tree structure(Linux filesystem) rooted at '/'.

### Check the new attached disk storage is now available for use using 'df -h' command
Notice disk 300GiB is now mounted under /mynewdisk 
![check disk space](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/mynewdisk.png?raw=true)

End of document
