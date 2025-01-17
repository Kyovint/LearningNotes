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
  database_url: "postgres://user:password@host:5432/dbname"
  redis_host: "redis.example.com"
  redis_port: "6379"
  feature_flag_enabled: "true"
```

Los configmaps se crean en el cluster pero deben ser usados por los pods de la siguiente maneras