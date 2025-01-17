En kubernetes Es una calificacion automatica que hace k8s al crear un pod y depende de como hayan sido definidos sus recursos
- **Guaranteed**: Un por obtiene esta calificacion cuando tiene definidos sus recursos request y limit con el mismo valor
- **Burstable**: Un por obtiene esta calificacion cuando al menos uno de sus contendores definido un limit y un request pero sus valores son diferentes
- **BestEffort**: Un pod obtiene esta califiacion cuando nignuno de sus contenedores tiene recursos definidos

> Cuando un nodo se queda sin recursos este expulsara los recursos segun su QoS en el orden: BestEffort -> Burstable -> Guaranteed y esta tarea es realizada por el Kubelet
