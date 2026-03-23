# Requests y Limits

## Que son

- `requests`: recursos minimos reservados para un contenedor.
- `limits`: techo maximo de recursos que puede consumir.

## Por que importan

- influyen en scheduling
- evitan starvation y consumo descontrolado
- facilitan multitenancy

## Comandos base

```bash
kubectl describe pod <pod-name> -n <namespace>
kubectl top pod -n <namespace>
```
