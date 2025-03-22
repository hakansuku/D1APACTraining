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

- create secret 
```k -n dynatrace create secret generic dynakube --from-literal="apiToken=<OPERATOR_TOKEN>"```


