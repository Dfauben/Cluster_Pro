# Cluster

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un `cluster` de Kubernetes es el conjunto completo:
- API de Kubernetes
- control-plane
- uno o mas nodos donde corren workloads

## Como funciona (flujo simple)

1. Envias un comando con `kubectl`.
2. `kube-apiserver` recibe el estado deseado.
3. `scheduler` decide en que nodo correr pods.
4. `kubelet` en el nodo crea/ajusta contenedores.
5. `controllers` reconcilian diferencias entre estado real y deseado.

## Por que importa

Todo en Kubernetes ocurre dentro de un cluster. Si no entiendes su estado global, puedes diagnosticar mal un problema local.

## Comandos utiles

```bash
kubectl cluster-info
kubectl get nodes
kubectl get componentstatuses
kubectl get pods -n kube-system
```

Nota:
- En versiones nuevas, `componentstatuses` puede no ser la mejor fuente de salud.
- En `kind`, muchos componentes se observan como pods en `kube-system`.
