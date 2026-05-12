# DNS interno (CoreDNS)

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Kubernetes usa `CoreDNS` para resolver nombres de servicios y pods dentro del cluster.

## Como ayuda en la practica

Puedes llamar servicios por nombre en lugar de IP:
- `http://mi-servicio`
- `http://mi-servicio.mi-namespace.svc.cluster.local`

## Componente relacionado

- Pods de `coredns` en `kube-system`.
- Service `kube-dns` (ClusterIP).

## Comandos utiles

```bash
kubectl get pods -n kube-system -l k8s-app=kube-dns
kubectl get svc -n kube-system kube-dns
kubectl describe svc -n kube-system kube-dns
```
