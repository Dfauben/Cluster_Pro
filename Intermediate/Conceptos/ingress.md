# Ingress

## Que es

Recurso que define reglas HTTP/HTTPS para enrutar trafico externo a servicios internos.

## Requiere

- un Ingress Controller activo (por ejemplo ingress-nginx)

## Flujo

cliente -> ingress controller -> service -> pod

## Comandos base

```bash
kubectl get ingress -A
kubectl describe ingress <ingress-name> -n <namespace>
kubectl get svc -n ingress-nginx
```
