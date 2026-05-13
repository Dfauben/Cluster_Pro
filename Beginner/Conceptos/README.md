# Conceptos Beginner

Esta carpeta ya no funciona como un glosario aislado. Ahora acompana a los bloques de aprendizaje de `Beginner` y te sirve para repasar la teoria que necesitas en cada tema.

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [00 - Prerrequisitos](../00_Prerrequisitos/README.md)
- [01 - Fundamentos del cluster](../01_Fundamentos/README.md)
- [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md)
- [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md)
- [04 - Despliegues declarativos](../04_Workloads_Declarativos/README.md)
- [05 - Services y exposicion basica](../05_Services_Exposicion/README.md)
- [06 - Configuracion basica](../06_Configuracion_Basica/README.md)
- [07 - Almacenamiento basico](../07_Almacenamiento_Basico/README.md)
- [08 - Debug operativo inicial](../08_Debug_Operativo/README.md)

## Como usar estos conceptos

Usa esta carpeta como apoyo del bloque que estes trabajando. La primera columna te dice el concepto y la segunda donde aparece por primera vez en Beginner.

## 01 - Fundamentos del cluster

| Concepto | Primera aparición |
|---|---|
| [Cluster](cluster.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |
| [API de Kubernetes](api-kubernetes.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |
| [Contexto de kubectl](kubectl-context.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |
| [Node](node.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |
| [Control Plane](control-plane.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |
| [IP interna](internal-ip.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |
| [Namespace](namespace.md) | [01 - Fundamentos del cluster](../01_Fundamentos/README.md) |

## 02 - Operacion diaria con kubectl

| Concepto | Primera aparición |
|---|---|
| [Labels](labels.md) | [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md) |
| [Selector](selector.md) | [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md) |
| [kubectl describe](kubectl-describe.md) | [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md) |
| [kubectl logs](kubectl-logs.md) | [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md) |
| [Events](events.md) | [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md) |
| [Custom Columns](custom-columns.md) | [02 - Operacion diaria con kubectl](../02_Kubectl_Operacion/README.md) |

## 03 - Despliegues imperativos

| Concepto | Primera aparición |
|---|---|
| [Pod](pod.md) | [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md) |
| [Replicas](replicas.md) | [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md) |
| [ReplicaSet](replicaset.md) | [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md) |
| [Deployment](deployment.md) | [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md) |
| [Rollout](rollout.md) | [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md) |
| [DaemonSet](daemonset.md) | [03 - Despliegues imperativos](../03_Workloads_Basicos/README.md) |

## 04 - Despliegues declarativos

Este bloque no añade conceptos nuevos al glosario. Reutiliza `Deployment`, `Service` y `Rollout` para trabajar en YAML con `apply`.

## 05 - Services y exposicion basica

| Concepto | Primera aparición |
|---|---|
| [Service](service.md) | [05 - Services y exposicion basica](../05_Services_Exposicion/README.md) |
| [ClusterIP](clusterip.md) | [05 - Services y exposicion basica](../05_Services_Exposicion/README.md) |
| [DNS interno (CoreDNS)](dns-interno.md) | [05 - Services y exposicion basica](../05_Services_Exposicion/README.md) |

## Lectura recomendada

Si estas empezando el nivel, lee por orden de aparicion:

1. `cluster.md`
2. `api-kubernetes.md`
3. `kubectl-context.md`
4. `node.md`
5. `control-plane.md`
6. `namespace.md`
7. `labels.md`
8. `selector.md`
9. `kubectl-describe.md`
10. `kubectl-logs.md`
11. `pod.md`
12. `replicas.md`
13. `replicaset.md`
14. `deployment.md`
15. `service.md`
16. `clusterip.md`
17. `dns-interno.md`

## Nota

No hace falta leerlo todo de golpe. Usa esta carpeta como referencia asociada al tema que estes trabajando en el modulo.
