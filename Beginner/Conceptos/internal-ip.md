# IP interna

## Que es

La `internal IP` es la direccion interna usada dentro de la red del cluster o del host.

## Tipos de IP que veras en Kubernetes

- `Node Internal-IP`: IP interna del nodo.
- `Pod IP`: IP del pod dentro de la red de pods.
- `Service ClusterIP`: IP virtual estable del servicio.

## Diferencia clave

- Un pod puede morir y nacer con otra `Pod IP`.
- Un `Service` mantiene una `ClusterIP` estable para acceder al grupo de pods.

## Comandos utiles

```bash
kubectl get nodes -o wide
kubectl get pods -A -o wide
kubectl get svc -A
```

## Ejemplo mental rapido

Cliente dentro del cluster -> `Service ClusterIP` -> selector -> pod backend (con Pod IP dinamica).
