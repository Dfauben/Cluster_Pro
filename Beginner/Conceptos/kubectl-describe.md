# kubectl describe

## Que es

`kubectl describe` es un comando de inspeccion detallada para un recurso especifico.

## Que muestra

- metadata (labels, annotations)
- estado y condiciones
- configuracion efectiva
- eventos asociados

## Cuando usarlo

- un pod no arranca
- un nodo esta `NotReady`
- un deployment no progresa

## Comandos utiles

```bash
kubectl describe node lab-k8s-control-plane
kubectl describe pod <pod-name> -n <namespace>
kubectl describe deployment <deployment-name> -n <namespace>
```
