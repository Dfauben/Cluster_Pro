# Service

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un `service` expone pods con un endpoint estable.

## Por que existe

Las IP de pods cambian. El service ofrece una direccion fija y balancea trafico entre pods que coinciden con su selector.

## Tipos mas comunes

- `ClusterIP`: solo accesible dentro del cluster.
- `NodePort`: expone puerto en cada nodo.
- `LoadBalancer`: usa balanceador externo (si el entorno lo soporta).

## Comandos utiles

```bash
kubectl get svc -A
kubectl describe svc hello-k8s
kubectl get endpoints hello-k8s
```

## Relacion clave

`Service` selecciona pods por labels (ejemplo: `app=hello-k8s`).