# Intermediate - Operacion con criterio de produccion

Este modulo sube el nivel desde la operacion basica hacia patrones reales de plataforma.

## Regla de ejecucion

Todo `Intermediate` se ejecuta desde **WSL**, incluyendo `docker`.

## Ruta de aprendizaje

1. [00 Cluster y Nodos](00_Cluster_y_Nodos/README.md)
2. [01 Probes de salud](01_Probes_Salud/README.md)
3. [02 Recursos y Scheduling](02_Recursos_y_Scheduling/README.md)
4. [03 Networking e Ingress](03_Networking_e_Ingress/README.md)
5. [04 Persistencia (PV/PVC)](04_Storage_Persistencia/README.md)
6. [05 Helm base](05_Helm_Base/README.md)

## Biblioteca de conceptos

- [Indice de conceptos](Conceptos/README.md)
- [Cordon, Drain y Uncordon](Conceptos/cordon-drain-uncordon.md)
- [Probes](Conceptos/probes.md)
- [Requests y Limits](Conceptos/requests-limits.md)
- [NodeSelector](Conceptos/nodeselector.md)
- [Taints y Tolerations](Conceptos/taints-tolerations.md)
- [Ingress](Conceptos/ingress.md)
- [PV, PVC y StorageClass](Conceptos/pv-pvc-storageclass.md)
- [Release de Helm](Conceptos/helm-release.md)

## Decision de ubicacion (cluster y nodos)

La creacion de cluster y gestion de nodos queda en `00_Cluster_y_Nodos` para que:
- `Beginner` siga enfocado en uso de Kubernetes desde un cluster ya operativo.
- `Intermediate` cubra responsabilidad de infraestructura local y topologia multinodo.
