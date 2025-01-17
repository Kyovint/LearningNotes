Los limit range en Kubernetes permiten definir recursos ([[Pods|Request y limits]]) por defecto para todos los recursos de un namespace especifico, estas configuraciones se aplicaran solo si los contenedores No tienen definidos sus recursos ya que en el **caso de que si lo tengan se aplicaran los definidos y se omitiran las definiciones en el limit range** para el pod donde se definieron los recursos.

Para agregar este recurso se debe crear el manifiesto a continuacion y aplicarlo
```YAML
apiVersion: v1
kind: LimitRange
metadata:
  name: example-limits
  namespace: default
spec:
  limits:
  type: Container # recurso al que se le aplican los limites
  - default: # limite por defecto
      memory: "<CANTIDAD>Mi"
      cpu: "<CANTIDAD>"
    defaultRequest: #Request por defecto
      memory: "<CANTIDAD>Mi"
      cpu: "<CANTIDAD>"
```