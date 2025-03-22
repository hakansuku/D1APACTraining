# 10_2 Deploy - EasyTrade demo application

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

