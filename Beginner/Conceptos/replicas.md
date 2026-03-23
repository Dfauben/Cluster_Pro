# Replicas

## Que son

Las replicas son la cantidad deseada de pods para una aplicacion.

## Para que sirven

- alta disponibilidad
- repartir carga
- tolerancia a fallos de pod

## Donde se definen

Normalmente en un `Deployment`:
- `spec.replicas: N`

## Comandos utiles

```bash
kubectl get deploy
kubectl scale deployment hello-k8s --replicas=3
kubectl get pods -l app=hello-k8s
```
