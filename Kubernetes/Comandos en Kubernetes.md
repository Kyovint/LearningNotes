> Entiendase como workload las cargas u objetos de kubernetes como pods, deployments, etcetera.

- ✨ Ingresar a un contenedor especifico de un pod ✨
```shell
  kubectl exec -it <POD_NAME> -c <CONTAINER_NAME> -- /bin/sh
  # Si no se especifica el contenedor kubectl ingresara al primer contenedor definido en el manifiesto del pod
```

- Aplicar las configuraciones de un manifiesto
```shell
  kubectl apply -f <FILENAME>.yml
```

- Mostrar los elementos de un workload especifico del cluster
```shell
kubectl get <WORKLOAD_IN_PLURAL>
```

- Mostrar informacion detallada de un workload
```shell
kubectl describe <WORKLOAD>/<WORKLOAD_NAME>
# kubectl describe pod/my-pod
```

- Eliminar un workload aplicado al cluster
```shell
kubectl delete <WORKLOAD>/<WORKLOAD_NAME>
```

- Editar un workload creado
```shell
kubectl edit <WORKLOAD>/<WORKLOAD_NAME>
```

- ✨ Ver las versiones/Revisiones (historial) de los deployments con su numero de version ✨
```shell
kubectl rollout history deployment/<DEPLOYMENT_NAME>
```

- ✨ Hacer Rollback de los deployments ✨
```shell
kubectl rollout unde deployment/<DEPLOYMENT_NAME> --to-revision=<VERSION_NUMBER>
# la version se obtiene del comando anterior
```

- Mostrar los logs de un workload
```shell
kubectl logs <WORKLOAD>/<WORKLOAD_NAME>
```

- Muestra mas detalle de un workload
```shell
kubectl get <WORKLOAD> -o wide
```

- ✨ Setear un tiempo de gracia antes de eliminar un pod del cluster ✨
```shell
kubectl delete pod <POD_NAME> --grace-period=<SECONDS>
```

- ✨Muestra el manifiesto (YAML) de un workload ✨
```shell
kubectl get <WORKLOAD>/<WORKLOAD_NAME> -o yaml
```

- Hacer el port forward de un pod a la maquina local
```shell
kubectl port-forward pod/<POD_NAME> <LOCAL_PORT>:<CONTAINER_PORT>
```
