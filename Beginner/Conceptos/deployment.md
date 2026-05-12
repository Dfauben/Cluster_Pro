# Deployment

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un `deployment` es un controlador declarativo para pods.

Define:
- imagen
- replicas deseadas
- estrategia de actualizacion

## Como funciona

El deployment crea y gestiona un `ReplicaSet`, y este mantiene la cantidad de pods deseada.

## Ventajas operativas

- escalado simple
- rollout controlado
- rollback rapido

## Comandos utiles

```bash
kubectl get deployment
kubectl scale deployment hello-k8s --replicas=3
kubectl rollout status deployment/hello-k8s
kubectl rollout history deployment/hello-k8s
kubectl rollout undo deployment/hello-k8s
```
