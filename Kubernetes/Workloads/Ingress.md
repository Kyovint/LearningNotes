Ingress en Kubernetes es una regla de trafico que se encarga centralizar multiples servicios del cluster en una sola IP publica.

Este proceso lo realiza por medio de un nginx controller, haciendo uso de un patron basado en paths donde cada path redigira a un servicio diferente, de esta manera con la misma IP y unicamente asignado un sub path a la ip se puede apuntar a diferentes servicios.

> dependiendo del cluster el nginx controller puede o no venir instalado por defecto.

Al crear un ingress lo que sucede es el siguiente paso a paso.

1. Se crea en el namespace un [[3. LoadBalancer]] al cual se le asignara una IP y que se encargara de recibir todo el trafico y enviarlo a ingress
2. Este loadbalancer contiene la misma IP publica que el ingress creado, cuando recibe un trafico el load balancer le envia la peticion a ingress y este lo resolvera por medio del controlador ingress

Cabe destacar que para poder crear el ingress es necesario que los servicios ya sea de nodePort, Cluster IP o Loadbalancer que vayan a ser asociados a ingress ya esten creados. Para crear un Ingress se hace de la sigueinte manera

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: <INGRESS_NAME>
spec:
  rules:
  - http:
    paths:
    - path: <PATH> # por ejemplo /login
      pathType: Prefix
      backend:
        service:
          name: <SERVICE_NAME> # nombre del servicio que se le asignara
          port:
            number: 8080 # http
    - path:
    .....
```

Cuando se crea el ingres se debe esperar que el loadbalancer le asigne la ip a ingress y una vez este proceso se realice se debe apuntar a `http://<INGRERSS_IP>/<PATH>` y esto comunicara al servicio haciendo el balanceo de carga correspondiente segun el servicio asociado a ese path.
