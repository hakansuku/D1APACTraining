# Installing Enviornment Activegates in Kubernetes containers

### Prepare a kubernettes environment
- Refer to 10.1 to prepare a kubernetes environment, make sure you add alias k='microk8s kubectl' into the ~/.bashrc file.

### Generating Pre-requisite Access Token

- In your SaaS tenant , open Acces Tokens app and Click GENERATE NEW TOKEN button.

![accesstoken](https://github.com/hakansuku/D1APACTraining/blob/main/images/containerAG/accesstoken.png)

> Copy and Save the generated token, this will be used in the next step

### Generating Active Gate token via Dynatrace API (AG TOKEN)
- from the liux terminal execute below curl command . 

> replace the URL with your tenant URL and authorization token with the token generated from UI in previous step.

```
curl -X 'POST' \
  'https://<your tenant URL>/api/v2/activeGateTokens' \
  -H 'accept: application/json; charset=utf-8' \
  -H 'Authorization: Api-Token <YOUR ACCESS TOKEN GENERATED>' \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d '{
  "activeGateType": "ENVIRONMENT",
  "expirationDate": "now+6M",
  "name": "myToken",
  "seedToken": false
}'
```

>Copy and Save the Activegate token Generated from the API all returned

### Extracting the kube-system namespace UUID (k8s namespace UUID)

```
k get namespace kube-system -o jsonpath='{.metadata.uid}'
```

> Copy and Save the kube-system namespace UUID obtained


### Creatinga namespace for your AG
```
k create namespace dynatrace
```





