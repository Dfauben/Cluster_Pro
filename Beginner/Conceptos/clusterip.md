# ClusterIP

## Que es

`ClusterIP` es el tipo de service por defecto en Kubernetes.

## Para que sirve

- expone una app solo dentro del cluster
- ofrece una IP virtual estable
- balancea trafico hacia pods seleccionados

## Cuando usarlo

- comunicacion entre servicios internos
- backends que no necesitan exposicion publica directa

## Comandos utiles

```bash
kubectl get svc
kubectl expose deployment hello-k8s --port=80 --target-port=80 --type=ClusterIP
kubectl describe svc hello-k8s
```
