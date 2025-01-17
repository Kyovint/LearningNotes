Los pods en kubernetes tienen un ciclo de vida conformado por 4 fases

POD -> poststart -> prestop -> KILLPOD

Los lifecycle Hooks permiten ejecutar acciones en los momentos de poststart y prestop y estas acciones se definene en los manifiestos de los [[Pods]] de la siguiente manera

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
  namespace: default
spec:
  containers:
  - name: example-container
    image: nginx:latest
    lifecycle:
      postStart: # accion a ejecutar despues de levantar el pod
        exec:
          command: ["sh", "-c", "echo 'Container started at $(date)' > /var/log/startup.log"]
      preStop: # accion a ejecutar despues de parar
        exec:
          command: ["sh", "-c", "echo 'Container is stopping at $(date)' > /var/log/shutdown.log"]
    ports:
    - containerPort: 80
  volumes:
  - name: app-volume
    configMap:
      name: app-script

```

Los lifecycle hooks no permiten mostrar las salidas por la salida estandar (linea de comandos o logs) de los pods por lo que las salidas deben almacenarse en algun lado, por ejemplo un config map