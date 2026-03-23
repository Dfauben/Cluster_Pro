# Probes

## Tipos

- `livenessProbe`: determina si el contenedor sigue vivo.
- `readinessProbe`: determina si puede recibir trafico.
- `startupProbe`: protege arranques lentos antes de activar las otras probes.

## Efecto operativo

- falla en liveness: Kubernetes reinicia el contenedor.
- falla en readiness: el pod se saca temporalmente de endpoints de servicio.

## Comandos base

```bash
kubectl describe pod <pod-name> -n <namespace>
kubectl get pods -n <namespace>
kubectl get events -n <namespace> --sort-by=.metadata.creationTimestamp
```
