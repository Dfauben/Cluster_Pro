# Cordon, Drain y Uncordon

## Que hacen

- `cordon`: marca un nodo como no elegible para nuevos pods.
- `drain`: evacua pods de un nodo para mantenimiento.
- `uncordon`: vuelve a habilitar scheduling en el nodo.

## Cuando usarlos

- mantenimiento de nodo
- cambios de runtime o kernel
- simulacion de operacion real en laboratorio

## Comandos base

```bash
kubectl cordon <node>
kubectl drain <node> --ignore-daemonsets --delete-emptydir-data
kubectl uncordon <node>
```
