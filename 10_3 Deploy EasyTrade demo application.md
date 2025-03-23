# 10_2 Deploy - EasyTrade demo application

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/login.jpg)

> We will install Easytrade demo application

reference: https://github.com/Dynatrace/easytrade/blob/main/README.md

- Git clone EasyTrade repository 
```git clone https://github.com/Dynatrace/easytrade```

![gitclone](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/gitclone.jpg)

- chage directory to easytrade
```cd easytrade```

- create a easytrade namespace
```k create namespace easytrade```

- deploy easytrade 
```k -n easytrade apply -f ./kubernetes-manifests/release ```

![deploy](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/deploy.jpg)

- validate all pods are running
```k get pods -A```

![validate](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/easytradevalidate.jpg)

- Observe the deployment pods from kubernetes app
![app](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/easytrade.jpg)

- Get external nodeport of frontend service
```k -n easytrade get svc```

![port](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/nodeport.jpg)

- Go to your instance , security tab and allow inbound traffic for the port discovered in previous step

![inbound](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/inbound.jpg)

- Open a browser , type in the ip address & port number
  ```http://http://43.203.165.232:31146/```
  
![login](https://github.com/hakansuku/D1APACTraining/blob/main/images/classicfullstack/login.jpg)
