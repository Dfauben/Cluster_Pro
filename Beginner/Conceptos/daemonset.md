# DaemonSet

## Que es

Un DaemonSet asegura que exista un pod en cada nodo (o en un subconjunto seleccionado).

## Uso comun

- agentes de red
- colectores de logs
- agentes de monitoreo

## Ejemplo en este lab

`kube-proxy` y `kindnet` corren como DaemonSet en `kube-system`.

## Comandos utiles

```bash
kubectl get ds -A
kubectl describe ds kube-proxy -n kube-system
```
