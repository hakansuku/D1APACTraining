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


### 11_1_5 Obatining connectivity infromation for AG (tenantUUID , tenantToken and communicationEndpoints) via API
from the linux terminal execute the below curl command.
> replace the URL with your tenant URL and authorization token with the download scope token generated from UI in previous step.


```
curl -X 'GET' \
  'https://<your tenant URL>/api/v1/deployment/installer/gateway/connectioninfo?defaultZoneFallback=false' \
  -H 'accept: application/json' \
  -H 'Authorization: Api-Token <Your download scope token>'
```
> Copy and save the values returned for "tenantUUID", "tenantToken" , and "communicationEndpoints"


### 11_1_6 Extracting the kube-system namespace UUID (k8s namespace UUID)

```
k get namespace kube-system -o jsonpath='{.metadata.uid}'
```

> Copy and Save the kube-system namespace UUID obtained


### 11_1_7 Creating a namespace for your AG
```
k create namespace dynatrace
```

### 11_1_8 Creating secret 
> replace with your obtained Tenant token and AG token from 11_1_5 and 11_1_3

```
 k -n dynatrace create secret generic dynatrace-tokens --from-literal="tenant-token=<YOUR TENANT token from 11_1_5> " --from-literal="auth-token=<YOUR AG token from 11_1_3>"
```

### 11_1_9 Create a ag-deployment-example.yaml file 
> reference from https://docs.dynatrace.com/docs/ingest-from/dynatrace-activegate/activegate-in-container#deployment

- copy the example configuration code from above link into a ag-deployment-example.yaml file.
```
vi ag-deployment-example.yaml
```


making sure to replace:

CPU_ARCHITECTURE with your CPU architecture. (Possible values are amd64, arm64, and s390x)

<REPOSITORY_URL> with one of the supported registries (example: public.ecr.aws/dynatrace/dynatrace-activegate:1.309.26.20250311-132824)

<YOUR_ENVIRONMENT_ID> with your environment ID (example: tax37822)

<YOUR_COMMUNICATION_ENDPOINTS> with the value of communicationEndpoints obtained in Prerequisites from the connectivity information (values obtained from 11_1_5)

<YOUR_KUBE-SYSTEM_NAMESPACE_UUID> with the kube-system namespace UUID (value obtained from 11_1_6)


- Execute below command to deploy the ag-deployment-example.yaml file
```
k apply -f ag-deployment-example.yaml
```


### 11_1_10 Check your activegate pod running
```
k get pods -A
```
![deploy](https://github.com/hakansuku/D1APACTraining/blob/main/images/containerAG/deploy.png)

> check in Dynatrace UI :  Deployment Status > Activegates

![status](https://github.com/hakansuku/D1APACTraining/blob/main/images/containerAG/status.png)





