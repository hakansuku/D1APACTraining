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

open bash configuration for editing
```vi ~/.bashrc```

add following line into below other aliases
``` alias k='microk8s kubectl' ```

save changes with :wq

reload bashrc
```. ~/.bashrc```


```k get all```

root@ip-172-31-17-91:/home/ubuntu# k get all
NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.152.183.1   <none>        443/TCP   6m45s

```k cluster-info```
> Kubernetes control plane is running at https://127.0.0.1:16443
CoreDNS is running at https://127.0.0.1:16443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

```k create namespace dynatrace```

```k get namespaces```
> NAME              STATUS   AGE
> default           Active   10m
> dynatrace         Active   3m38s
> kube-node-lease   Active   10m
> kube-public       Active   10m
> kube-system       Active   10m


```k apply -f https://github.com/Dynatrace/dynatrace-operator/releases/download/v1.4.1/kubernetes-csi.yaml```

vi mkDynakube.yaml





