# Jobs
Los jobs en kubernetes permiten ejecutar tareas unicas controladas que no son persistentes dentro del cluster, esto lo hace por medio de la creacion de pods y dentro de ellos ejecuta la tarea definida.

```Yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: example-job
  namespace: default
spec:
  parallelism: <CANTIDAD> # Cantidad de pods para ejecutar el job
  backoffLimit: <CANTIDAD> #se limpian los pods luego de x segundos
  template:
    metadata:
      labels:
        app: example-app
    spec:
      containers:
      - name: example-container
        image: busybox
        command: ["echo", "Hello, Kubernetes!"]
      restartPolicy: <CONDITION> # se reinicia el pod cuando...

```


# Cronjobs
Permiten configurar la ejecucion de un job en un momento especifico
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: example-cronjob
  namespace: default
spec:
  schedule: "0 0 * * *"  # Ejecutar a medianoche todos los días
  jobTemplate:
    spec:
      template:
        metadata:
          labels:
            app: example-app
        spec:
          containers:
          - name: example-container
            image: busybox
            command: ["echo", "Hello, Kubernetes!"]
          restartPolicy: OnFailure
```