# Labels

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que son

Las labels son pares `clave=valor` que describen y organizan recursos de Kubernetes.

## Para que sirven

- agrupar recursos
- filtrar con `kubectl`
- conectar `Service` con pods backend
- soportar reglas de despliegue y politicas

## Ejemplos

- `app=hello-k8s`
- `tier=backend`
- `component=kube-apiserver`

## Comandos utiles

```bash
kubectl get pods -A --show-labels
kubectl get pods -A -l k8s-app=kube-dns
kubectl label pod <pod-name> entorno=lab --overwrite
```
