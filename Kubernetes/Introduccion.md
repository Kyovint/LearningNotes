# Que es kubernetes?
- Es un sistema de orquestacion de contenedores de codigo abierto que facilita el despliegue, escalado y mantenimiento de contenedores
- Los contenedores dejan de ser elementos estaticos
- Kubernetes organiza los contendores en pods

> **"Un pod es un contendores de contenedores, y puede tener mas de un contenedor"**

- El cluster es un conjunto de maquinas que ejecutan aplicaciones y existen dos tipos de maquinas.
1. **Masters**
2. **Workers**

# Caracteristicas de Kubernetes
- **Autocuracion**: Detecta faalos o anomalias en los contenedores y tomar acciones que solcuionen el problema automaticamente
- **Escalado Automatico**: Genera replicas o destruye segun la demanda de la aplicacion automaticamente
- **Despliegue y actualizaciones continuas**: Facilita el despliegue de nuevos cambios sin sacrificar disponiblidad o trafico.

# Arquitectura de Kubernetes
## Control Plane
Conjunto que administra y controla el estado del cluster
- **Api server**: (Es el punto de entrada al cluster) procesa y recibe peticiones de kubectl tambien actualiza el estado del cluster en la ETDC
- **ETDC**: (Base de datos) Es una DB distribuida y altamente disponible almacena la configuracion y el estado del cluster, cada master tiene una copia del ETDC.
- **Control Manager**: Ejecuta los controladores que garantizan el estado del cluster deseado.
- **Scheduler**: determina en que nodos crear determinado pod segun la disponibilidad de recursos y relgas establecidas.

## Workers
Ejecutan aplicaciones, pods, deployments y demas
- **Kubelet**: agente que se comunica con el API server.
- **Kube proxy**: garatniza las configuraciones de red y realiza el balance de carga de los pods.
- **Container Runtime**: software que ejecuta los contenedores.

