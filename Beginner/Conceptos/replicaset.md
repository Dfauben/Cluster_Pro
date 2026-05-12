# ReplicaSet

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un ReplicaSet mantiene una cantidad estable de pods identicos en ejecucion.

## Relacion con Deployment

En uso diario, normalmente no creas ReplicaSet directo:
- el [Deployment](deployment.md) crea y gestiona ReplicaSets por ti.

## Para que sirve

- asegurar N replicas activas
- reemplazar pods que caen

## Comandos utiles

```bash
kubectl get rs -A
kubectl describe rs <replicaset-name> -n <namespace>
```
