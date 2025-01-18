Los configMaps son objetos de Kubernetes que permiten almacenar valores de configuracion clave valor de forma persistente. Se pueden crear por manifiestos o por comando.

```shell
kubectl create configmap name--from-literal=<KEY>=<VALUE>
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  <KEY>: "VALUE"
  <KEY>: "VALUE"
```

Los configmaps se crean en el cluster pero deben ser usados por los pods de la siguiente manera agregando `spec.containers.<container>.env.<value>.valueFrom.configMapRef`

```yml
apiVersion: v1
kind: Pod
metadata:
  name: <POD_NAME>
spec:
  containers:
  - name: <CONTAINER_NAME>
    image: <IMAGE_NAME>
    env:
      - name: <VALUE_NAME
	    valueFrom:
	      configMapKeyRef:
	        name: <CONFIGMAP_NAME>
	        key: <KEY_NAME>
```

Con los configamps tambien es posible generar un archivo de valores dentro del pod mediante el uso de volumenes de la siguiente manera

```yml
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
    configMap:
	  name: app-config
```

El archivo se creara en la ruta especificada con todo el contenido de llave valor del configmap

> La actualizacion de un configmap no actualiza, reinicia o mata ningun workload que lo este usando, lo que hace dinamico el uso de los valores de los configmap