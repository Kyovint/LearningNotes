- Ingresar a un contenedor especifico de un pod
  ```shell
  kubectl exec -it <POD_NAME> -c <CONTAINER_NAME> -- /bin/sh
```

- Aplicar las configuraciones de un manifiesto
  ```shell
  kubectl apply -f <FILENAME>.yml
```
- 