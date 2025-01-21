Es un objeto de kubernetes que se encarga de almacenar datos importantes y sensibles dentro de nuestro cluster de kubernetes.

Los secrets se almacenan en el ETCD la cual es una base de datos dentro del control plane, con lo cual si la base de datos no esta encriptada todos los secretos no estaran encriptados, es por esto que los datos unicamente estaran codificados en base 64, lo cual no es muy seguro.

Los secretos en kubernetes se pueden crear mendiante comando o mediante manifiesto

```shell
kubectl create secret generic <SECRET_NAME> --from-literal=<KEY>=<VALUE> --from-literal=<KEY>=<VALUE>
```

> Esto guardara el valor del secreto en base 64 y esto se puede evidenciar por medio del comando `kubectl get secret <secretName> -o yaml`

Por otro lado, tambien es posible **usar un manifiesto**, de la siguiente manera
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: <SECRET_NAME>
type: Opaque
data:
  <KEY>: <VALUE_IN_BASE64>
```

> Es importante que si se usa el manifiesto de tipo Opaque que los valores del secreto ya esten codificados en base 64

Al igual que los configmaps es posible inyectar los secretos a los Pods y sus contenedores de la sigueinte manera
```shell
apiVersion: v1
kind: Pod
metadata:
  name: <POD_NAME>
spec:
  containers:
  - name: <CONTAINER_NAME>
    image: <IMAGE_NAME>
    env:
      - name: <ENV_NAME>
        valueFrom:
          secretKeyRef:
            name: <SECRET_NAME>
            key: <KEY_NAME>
```

Y de igualmanera es posible generar un archivo con los valores de un secreto, asi
```shell
apiVersion: v1
kind: Pod
metadata:
  name: <POD_NAME>
spec:
  containers:
  - name: <CONTAINER_NAME>
    image: <IMAGE_NAME>
    volumeMounts:
    - name: <MOUNT_NAME>
      mountPath: <MOUNT_PATH> #ruta dentro del contenedor donde se montara  
  volumes:
  - name: <VOLUME_NAME>
    secret:
	  name: <SECRET_NAME>
```

> La actualizacion de un secreto no hace que los pods se reinicien, exactamente el mismo comportamiento que los configmaps

> Existen diferentes tipos de secreto como basicAuth, ssh, y tls los cuales cumplen la funcion de guardar el secreto para una funcion especifica