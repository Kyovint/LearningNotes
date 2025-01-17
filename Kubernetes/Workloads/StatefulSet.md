En kubernetes los statefulset son unos elementos que funcionan muy similares a los deployments con unas pequeñas diferencias dirigidas a aplicaciones que almacenan un estado (Como una base de datos).

1. Los st nombras las replicas por numeracion ordenada, diferente a como lo hace un deployment el cual asigna un hash unico a las replicas.
   
   Statefulset crea las replicas `my-pod-01` y `my-pod-02` mientras que deployment crearia `my-pod-zsdw-dsvgw-ad` y `my-pod-zsdw-dsvgw-ad` **Esto hace que cuando un pod se reinicie en statefulset los pods mantengan sus mismos nombres, mientras que en deployment sus nombres cambiaran con un nuevo hash**.

2. Statefulset cuenta con los persistent volume claims (PVC) los cuales aseguran la persistencia de los datos generados por un pod especifico, ademas se garantiza que el pod con determinado nombre vuelva a tener el acceso al PVC.
   
   **PVC** -> Es un enalce logico de un pod a un persisten Volume (PV como en un statefulset los nombres de las replicoas no cambian se asegura que el pod tenga acceso auqnue sea reiniciado o creado.
   
   Con un volumen normal puede que un pod pierda el acceso a un volumen y PVC garantiza que no sea asi.

3. La creacion y borrado de las replicas es ordenada mientras que en un deployment se hace de forma aleatoria.

```yml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: example-statefulset
  namespace: default
spec:
  serviceName: "example"
  replicas: 3
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
  volumeClaimTemplates: #Creacion o enalce de un vpc
  - metadata:
      name: example-pvc
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
      storageClassName: <driver> #Permite usar driver para crear volumen cloud
```

## Cuando usar statefulset o deployment?

Se usa statefulset cuando:
- Se necesitan nombre de los pods staticos para ser referenciados
- Se requeire persistencia de estado
- se requere controlar la creacion o eliminacion de replicas

Se usa deplyoments cuando
- No se requiere saber el nombre del pod
- Los pods no requieren guardar estados