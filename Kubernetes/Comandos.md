- Ingresar a un contenedor especifico de un pod
```shell
  kubectl exec -it <POD_NAME> -c <CONTAINER_NAME> -- /bin/sh
```

- Aplicar las configuraciones de un manifiesto
```shell
  kubectl apply -f <FILENAME>.yml
```

- Muestra los nodos del cluster
```shell
kubectl get <WORKLOAD_IN_PLURAL>
# pods, nodes, jobs, deployments
```

- Muestra informacion detallada de un 