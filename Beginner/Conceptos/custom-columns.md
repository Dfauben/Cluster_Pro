# Custom Columns

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

`custom-columns` es una forma de personalizar salida de `kubectl get` mostrando solo campos relevantes.

## Para que sirve

- crear vistas operativas rapidas
- evitar ruido de columnas que no necesitas
- adaptar salida para troubleshooting

## Ejemplo

```bash
kubectl get pods -A -o custom-columns='NAMESPACE:.metadata.namespace,NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName'
```

## Tip

Puedes descubrir rutas JSON de campos con:

```bash
kubectl get pod <pod-name> -n <namespace> -o yaml
```