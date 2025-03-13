sudo su
install microk8s

``` snap install microk8s --classic ```

> root@ip-172-31-17-91:/home/ubuntu# snap install microk8s --classic
microk8s (1.32/stable) v1.32.2 from Canonical✓ installed


```vi ~/.bashrc```

alias k='microk8s kubectl'

execute to commit changes

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





