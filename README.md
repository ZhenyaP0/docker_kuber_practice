# docker_kuber_practice
1. Создание Dockerfile
2. Собираем Docker image `docker build -t zhenyap/server:1.0.0 -t zhenyap/server:latest server`
3. Добавление image на Docker Hub `docker push zhenyap/server:1.0.0`
4. Создание Kubernetes Deployment manifest 
5. Установка манифеста в кластер Kubernetes `kubectl apply -f web-deployment.yaml`
6. Проверка, успешного создания Deployment и запущенных реплик `kubectl get deployments` `kubectl get pods`
7. Обеспечение доступа к web-приложению внутри кластера Kubernetes `kubectl port-forward --address 0.0.0.0 deployment/web 8080:8000`
8. Проверка работоспособности и текущего состояния Deployment'а `kubectl describe deployment web`

```Name:                   web
Namespace:              default
CreationTimestamp:      Mon, 22 May 2023 02:06:43 +0300
Labels:                 app=server
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=server
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=server
  Containers:
   server:
    Image:        zhenyap/server:1.0.0
    Port:         8000/TCP
    Host Port:    0/TCP
    Liveness:     http-get http://:8000/hello.html delay=3s timeout=1s period=3s #success=1 #failure=3
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   web-77c48d7f8d (2/2 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  11m   deployment-controller  Scaled up replica set web-77c48d7f8d to 2
  ```

