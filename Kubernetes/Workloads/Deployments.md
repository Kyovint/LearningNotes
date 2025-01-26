Los deployments son plantillas para la creacion de pods, estos garantizan que kubernetes busque siempre tener el estado deseado definido en el manifiesto, es decir, si un elemento definido en el deployment se borra K8S lo volvera a crear.

- Los deployments crean o llaman a las [[ReplicaSet]] quienes a su vez crean [[Pods]] y esto se puede verificar al usar `kubectl get replicaSet` despues de crear un deployment
- Con los deployments es posible modificar los replicaset directamente en el cluster con el comando `kubectl edit deployment/<NAME>`
- Con los deployments se pueden hacer rollbacks con el comando `kubectl rollout undo deployment/<NAME> --to-revision=<REVISION_NUMBER>`
- Los deployments permiten trabajar con replicas al usar replicaset y sus replicas tendran un hash unico
```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
  namespace: default
spec:
  replicas: <NUMBER_OF_REPLCIAS>
  strategy:
    rollingUpdate:
      maxSurge: <PODS_NUMBER> # Cuantos pods levanta inmediatamente
      maxUnavailable: <PODS_NUMBER> # Cuantas replicas pueden estar muertas
  selector:
    matchLabels:
      app: example-app
  template:
    metadata:
      labels:
        app: example-app
    spec:
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80
```
