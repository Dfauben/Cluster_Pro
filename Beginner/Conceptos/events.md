# Events

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que son

Los events son mensajes de diagnostico que Kubernetes registra cuando ocurre algo relevante sobre un recurso.

## Para que sirven

- detectar fallos de scheduling
- ver errores de imagen
- seguir reinicios y cambios de estado
- entender por que un pod no arranca

## Comandos utiles

```bash
kubectl get events -A --sort-by=.metadata.creationTimestamp
kubectl get events -n kube-system
kubectl describe pod <pod-name> -n <namespace>
```

## Nota operativa

Los events tienen retencion limitada. Es normal ver `No resources found` en momentos de baja actividad.
