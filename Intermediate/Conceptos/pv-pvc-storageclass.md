# PV, PVC y StorageClass

## Relacion

- `StorageClass`: define forma de aprovisionar almacenamiento.
- `PVC`: solicitud de almacenamiento por parte de una app.
- `PV`: volumen concreto que satisface esa solicitud.

## Flujo normal

pod usa PVC -> PVC se vincula a PV -> datos persisten fuera del ciclo de vida del pod.

## Comandos base

```bash
kubectl get storageclass
kubectl get pvc,pv -n <namespace>
kubectl describe pvc <pvc-name> -n <namespace>
```
