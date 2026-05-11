# Pod

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

El `pod` es la unidad minima desplegable en Kubernetes.

Un pod puede contener uno o varios contenedores que comparten:
- red (IP y puertos)
- almacenamiento efimero local

## Punto importante

Un pod no esta pensado como entidad "permanente". Si cae, Kubernetes crea otro para mantener el estado deseado.

## Estados comunes

- `Pending`
- `Running`
- `Succeeded`
- `Failed`
- `CrashLoopBackOff` (problema recurrente de arranque)

## Comandos utiles

```bash
kubectl get pods -A
kubectl describe pod <pod-name> -n <namespace>
kubectl logs <pod-name> -n <namespace>
```