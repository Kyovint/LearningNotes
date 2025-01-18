> Entiendase como workload las cargas u objetos de kubernetes como pods, deployments, etcetera.

- Ingresar a un contenedor especifico de un pod
```shell
  kubectl exec -it <POD_NAME> -c <CONTAINER_NAME> -- /bin/sh
```

- Aplicar las configuraciones de un manifiesto
```shell
  kubectl apply -f <FILENAME>.yml
```

- Muestra los elementos de un workload especifico del cluster
```shell
kubectl get <WORKLOAD_IN_PLURAL>
```

- Muestra informacion detallada de un workload
```shell
kubectl describe <WORKLOAD>/<WORKLOAD_NAME>
# kubectl describe pod/my-pod
```