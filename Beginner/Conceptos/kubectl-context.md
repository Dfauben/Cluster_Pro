# Contexto de kubectl

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

Un `context` define con que cluster, usuario y namespace trabaja `kubectl` por defecto.

## Por que importa

Si el contexto activo no es el correcto, puedes aplicar cambios en otro cluster por error.

## Comandos utiles

```bash
kubectl config current-context
kubectl config get-contexts
kubectl config use-context kind-lab-k8s
kubectl config set-context --current --namespace=default
```

## Interpretacion rapida

- `current-context`: objetivo actual de tus comandos.
- `get-contexts`: inventario de contextos disponibles.
- `use-context`: cambia de cluster/credenciales.
- `set-context --current --namespace=...`: cambia namespace por defecto para el contexto activo.
