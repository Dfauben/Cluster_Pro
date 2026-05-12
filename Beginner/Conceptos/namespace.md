# Namespace

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un `namespace` separa recursos logicamente dentro del mismo cluster.

## Para que sirve

- organizar aplicaciones por equipo/proyecto/entorno
- evitar mezclar recursos
- aplicar politicas (cuotas, RBAC, limites) por grupo

## Namespaces comunes

- `default`: uso general inicial.
- `kube-system`: componentes internos de Kubernetes.
- `kube-public`: recursos publicos del cluster.
- `kube-node-lease`: informacion de heartbeats de nodos.

## Comandos utiles

```bash
kubectl get namespaces
kubectl get pods -n kube-system
kubectl create namespace demo
kubectl config set-context --current --namespace=demo
```
