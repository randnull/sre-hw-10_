# Recreate
Манифест приложен в deployemnt_RECREATE.yaml

![Иллюстрация к проекту](https://github.com/randnull/sre-hw-10_/blob/main/photos/recreate.png)

Видим, что предыдущие поды terminate, новые running

# Rolling update

Манифест приложен в deployemnt_ROLLING_UPDATE.yaml

![Иллюстрация к проекту](https://github.com/randnull/sre-hw-10_/blob/main/photos/rolling.png)

Видим, что terminate поочередно для старых подов

# Blue Green

Манифест приложен в /blue_green

Шаги:

1. создание deployment_green:
   ```
       matchLabels:
      app.kubernetes.io/name: oncall
      app.kubernetes.io/component: web
      version: green
   ```
2. создание deployment_blue:
   ```
       matchLabels:
      app.kubernetes.io/name: oncall
      app.kubernetes.io/component: web
      version: blue
   ```

3.  kubectl apply -f deployment_green.yaml
4.  указать в service:
   ```
spec:
  type: NodePort
  selector:
    app.kubernetes.io/name: oncall
    version: green
```

5. kubectl apply -f deployment_blue.yaml

6. указать в service:
```
spec:
  type: NodePort
  selector:
    app.kubernetes.io/name: oncall
    version: blue
```
7. удалим deployment_green

![Иллюстрация к проекту](https://github.com/randnull/sre-hw-10_/blob/main/photos/blue_green.png)
