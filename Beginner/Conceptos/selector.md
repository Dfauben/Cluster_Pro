# Selector

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un selector es una regla de labels para elegir que recursos coinciden.

## Donde se usa

- `Service` para encontrar pods backend
- `Deployment` / `ReplicaSet` para controlar pods
- comandos `kubectl` con `-l`

## Ejemplo

Si un service tiene selector `app=hello-k8s`, solo enviara trafico a pods con esa label.

## Comandos utiles

```bash
kubectl get pods -l app=hello-k8s
kubectl get svc hello-k8s -o yaml
kubectl describe svc hello-k8s
```
