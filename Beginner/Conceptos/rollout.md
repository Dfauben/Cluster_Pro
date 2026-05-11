# Rollout

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un rollout es el proceso de aplicar una nueva version de un workload (por ejemplo un `Deployment`) de forma controlada.

## Que incluye

- creacion gradual de nuevos pods
- retiro gradual de pods antiguos
- seguimiento del estado de despliegue

## Operaciones comunes

- ver progreso
- ver historial
- reiniciar despliegue
- deshacer cambios (rollback)

## Comandos utiles

```bash
kubectl rollout status deployment/hello-k8s
kubectl rollout history deployment/hello-k8s
kubectl rollout restart deployment/hello-k8s
kubectl rollout undo deployment/hello-k8s
```