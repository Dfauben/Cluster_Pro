# NodeSelector

## Que es

Mecanismo simple para forzar que un pod se ejecute en nodos con labels especificos.

## Como funciona

- etiquetas nodo: `kubectl label node ...`
- pod con `spec.nodeSelector`

## Comandos base

```bash
kubectl get nodes --show-labels
kubectl label node <node> workload=apps
kubectl get pods -o wide -n <namespace>
```
