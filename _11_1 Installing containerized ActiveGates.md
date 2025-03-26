# Installing Environment Activegate in Kubernetes container

### 11_1_1 Prepare a kubernettes environment
- Refer to 10.1 to prepare a kubernetes environment, make sure you add alias k='microk8s kubectl' into the ~/.bashrc file.

### 11_1_2 Generating an Access Token to create AG token

- In your SaaS tenant , open Acces Tokens app and Click GENERATE NEW TOKEN button.

![accesstoken](https://github.com/hakansuku/D1APACTraining/blob/main/images/containerAG/accesstoken.png)

> Copy and Save the generated token, this will be used in the next step

### 11_1_3 Generating Active Gate token via Dynatrace API (AG TOKEN)
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

>Copy and Save the Activegate token Generated from the API returned


### 11_1_4 Generating an Access Token to get connectivity information for AG

- In your SaaS tenant , open Acces Tokens app and Click GENERATE NEW TOKEN button.

![accesstoken](https://github.com/hakansuku/D1APACTraining/blob/main/images/containerAG/downloadtoken.png)

> Copy and Save the generated download scope token, this will be used in the next step to get connectivity information for AG


### 11_2_5 Obatining connectivity infromation for AG (tenantUUID , tenantToken and communicationEndpoints) via API
from the linux terminal execute the below curl command.
> replace the URL with your tenant URL and authorization token with the download scope token generated from UI in previous step.


```
curl -X 'GET' \
  'https://<your tenant URL>/api/v1/deployment/installer/gateway/connectioninfo?defaultZoneFallback=false' \
  -H 'accept: application/json' \
  -H 'Authorization: Api-Token <Your download scope token>'
```
> Copy and save the values returned for "tenantUUID", "tenantToken" , and "communicationEndpoints"


### Extracting the kube-system namespace UUID (k8s namespace UUID)

```
k get namespace kube-system -o jsonpath='{.metadata.uid}'
```

> Copy and Save the kube-system namespace UUID obtained


### Creating a namespace for your AG
```
k create namespace dynatrace
```







