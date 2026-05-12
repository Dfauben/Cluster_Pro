# Node

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un `node` es una maquina (virtual o fisica) donde Kubernetes ejecuta pods.

## Que componentes tiene un node

- `kubelet`: agente que habla con el API server.
- `container runtime` (containerd, cri-o): ejecuta contenedores.
- `kube-proxy`: maneja reglas de red para servicios.

## Estados frecuentes

- `Ready`: nodo saludable para recibir pods.
- `NotReady`: nodo temporalmente no utilizable.

## Comandos utiles

```bash
kubectl get nodes -o wide
kubectl describe node kind-lab-k8s-control-plane
kubectl top node
```

Nota:
- `kubectl top node` requiere metrics server.
