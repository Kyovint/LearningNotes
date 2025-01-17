En kubernetes un daemonset permite tener una copia de un pod en todos los nodos o en unos nodos especificados

```YAML
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: example-daemonset
  namespace: default
spec:
  selector:
    matchLabels:
      name: mi-app
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

**Al ser una replica en cada nodo especificado o todos los nodos no hace uso de replicas**

> Es importante que los nodos tengan el label del selector especificado en el DaemonSet, para que la seleccion se haga, de lo contrario el pod no se creara en ese nodo, para ello se pued editar el nodo con `kubectl edit node/<NODE_NAME>` 

