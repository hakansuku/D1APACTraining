# 10_1 Environment preparation

Install kubernetes cluster using microk8s

> Refer to workshop 1_2 Cloud environment preparation.md to create a spot instance. 

- Create a AWS Spot instance , with the 
  OS : Ubuntu 24.04 LTS
  Instance type m5.xlarge  (4 vCPU , 16 GB RAM)

- connect via SSH

Run updates to update to latest version
```
sudo su
apt update -y
apt upgrade -y
```

sudo install microk8s

``` sudo snap install microk8s --classic ```

> root@ip-172-31-17-91:/home/ubuntu# snap install microk8s --classic
microk8s (1.32/stable) v1.32.2 from Canonical✓ installed

to check installation status run ```microk8s.status```

![microk8s](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/microk8s.jpg)


open bash configuration for editing
```vi ~/.bashrc```

add following line into below other aliases
``` alias k='microk8s kubectl' ```

save changes with command :wq

![microk8s](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/alias.jpg)

reload bashrc with command
```. ~/.bashrc```

now you should be able to use k instead of kubectl.


-end of document-



