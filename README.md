# kube-10
## Задание 1
Первым делом устанавливаю Helm. Дальше подготавливаю чарты (все в папке sp-chart)
```
version.BuildInfo{Version:"v3.16.1", GitCommit:"5a5449dc42be07001fd5771d56429132984ab3ab", GitTreeState:"clean", GoVersion:"go1.22.7"}

kubectl config view --raw > ~/.kube/config - конфиг для подключения к кластеру
```
## Задание 2
Создаем namespaces  
```
kubectl create namespace app1
kubectl create namespace app2
```
Далее создаем приложения  

App1:  
```
helm install sp-app1 --namespace app1 --set image.tag="1.18.0" --set replicaCount=2 sp-chart

NAME: sp-app1
LAST DEPLOYED: Wed Oct  9 18:32:31 2024
NAMESPACE: app1
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
---------------------------------------------------------

Content of NOTES.txt appears after deploy.
Deployed version 1.18.0.

---------------------------------------------------------
```
App2:  
```
[root@skillpropilserv-01 kube-10]# helm install sp-app2 --namespace app2 --set image.tag="1.19.0" --set replicaCount=1 sp-chart
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /root/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /root/.kube/config
NAME: sp-app2
LAST DEPLOYED: Wed Oct  9 18:33:04 2024
NAMESPACE: app2
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
---------------------------------------------------------
```
Проверяем деплой:
App1:  
```
[root@skillpropilserv-01 kube-10]# kubectl get pod -n app1
NAME                      READY   STATUS    RESTARTS   AGE
sp-app-6896b4bc6c-8rd9t   1/1     Running   0          37m
sp-app-6896b4bc6c-jszdd   1/1     Running   0          37m
```
App2:  
```
NAME                     READY   STATUS    RESTARTS   AGE
sp-app-7c8b4f68d-s4fv7   1/1     Running   0          37m
```
