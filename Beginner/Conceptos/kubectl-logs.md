# kubectl logs

## Que es

`kubectl logs` permite leer logs de contenedores dentro de pods.

## Para que sirve

- validar arranque de una app
- detectar errores de runtime
- inspeccionar comportamiento reciente

## Patrones comunes

```bash
kubectl logs <pod-name>
kubectl logs -l app=hello-k8s --tail=50 --prefix=true
kubectl logs <pod-name> --previous
kubectl logs <pod-name> -c <container-name>
```

## Tip operativo

Cuando usas selector `-l`, `--prefix=true` ayuda a identificar de que pod viene cada linea.
