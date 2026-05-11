# API de Kubernetes

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

La API de Kubernetes es la interfaz central del cluster.

Todo pasa por aqui:
- creacion y consulta de recursos
- cambios de estado deseado
- lectura de estado real

## Componente principal

- `kube-apiserver`: servidor que expone la API.

## Como se usa en la practica

- `kubectl` envia peticiones a la API.
- Controladores, scheduler y otros componentes tambien consumen esta API.

## Comandos utiles

```bash
kubectl cluster-info
kubectl get --raw /healthz
kubectl api-resources
kubectl api-versions
```