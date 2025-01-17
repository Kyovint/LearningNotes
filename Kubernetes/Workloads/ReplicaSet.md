Es un recurso de kubernetes que permite crear replicas de pods los cuales tendran los mismos contenedores, recursos y caracteristicas
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: example-replicaset
  namespace: default
spec:
  replicas: <NUMBER_OF_REPLICAS> #Numero de replicas
  selector:
    matchLabels:
      app: example-app
  template:
    metadata:
      labels:
        app: example-app
    spec: # Definicion de los contenedores
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80

```

Esto crea un recurso que se puede obtener con `kubectl get rs/<NAME>` ademas, crea n pods dentro del cluster con el nombre rs/HASH para diferenciar cada una de las replicas creadas