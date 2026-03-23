# Taints y Tolerations

## Que son

- `taint`: marca un nodo para rechazar pods que no lo toleren.
- `toleration`: permiso en el pod para ejecutarse en nodos taintados.

## Para que sirven

- aislar workloads sensibles
- reservar nodos dedicados
- controlar placement mas alla de labels

## Comandos base

```bash
kubectl taint nodes <node> dedicated=apps:NoSchedule
kubectl describe node <node>
kubectl describe pod <pod-name> -n <namespace>
```
