# 10_2 Install Dynatrace Operator - ClassicFullStack deployment mode 

> Note this workshop uses microk8s cluster for simplicity, unfortunately it is not a supported environment and CSI Driver does not work and CloudNativeFullStack deployment mode is not possible.

We will be instrumenting the cluster via ClassicFullStack deployment method. 
reference: https://docs.dynatrace.com/docs/ingest-from/setup-on-k8s/deployment/other/classic-full-stack

- Go to access tokens app and click generate a token from your tenant 

![token](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/token.png)

1) type in name 
2) choose template as Kubernetes Dynatrace Operator
3) Click Generate token

save the generated token
![generate](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/template.png)


- Create a Dynatrace namespace
``` sudo su```

``` k create namespace dynatrace ```

- create a secret 
```k -n dynatrace create secret generic dynakube --from-literal="apiToken=<OPERATOR_TOKEN>"```

![secret](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/namespace.png)

- Install latest version of operator
```k apply -f https://github.com/Dynatrace/dynatrace-operator/releases/download/v1.4.1/kubernetes.yaml```

check pods status by typing ```k get pods -A```
![pods](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/pods.png)

- Download the DynaKube custom resource sample for classic full-stack from GitHub 
https://github.com/Dynatrace/dynatrace-operator/blob/v1.3.2/assets/samples/dynakube/v1beta2/classicFullStack.yaml

> modify the line  apiUrl: https://ENVIRONMENTID.live.dynatrace.com/api with your environment tenant URL

Run the command below to apply the DynaKube custom resource, making sure to replace <your-DynaKube-CR> with your file from your previous step. 
```k apply -f <your-DynaKube-CR>.yaml```

![apiul](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/apiurl.png)

- Wait and validate by running 
```k get pods  -A```

![getpods](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/dynakube.jpg)

- Open kubernetes app

> Observe the new deployed cluster being monitored.
![cluster](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/cluster.jpg)




