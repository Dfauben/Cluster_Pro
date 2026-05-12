# Beginner 02 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../03_Workloads_Basicos/README.md)

## Contexto

Ya sabes leer la fotografia base del cluster. Ahora vas a convertir `kubectl` en una herramienta de lectura rapida para no perderte entre salidas largas.

## Tarea

Primero sacas una foto general, luego bajas a detalle y por ultimo filtras una vista concreta para comprobar que entiendes lo que ves.

```bash
kubectl get all -A
```

Esto te da una vista amplia. No esperes que lo muestre todo; espera que te sirva para ubicarte.

```bash
kubectl get pods -A --show-labels
```

Aqui ya no miras solo estado. Fijate en las labels, porque despues seran la forma real de seleccionar recursos.

```bash
kubectl describe node kind-lab-k8s-control-plane
```

Ahora bajas al detalle de un nodo. Lo que importa no es repetir todo lo que sale, sino reconocer condiciones, capacidad y si el nodo esta sano.

```bash
kubectl get pods -A -l app=no-existe
```

Este comando te enseña una idea importante: un selector puede no devolver nada y eso no significa fallo del cluster. Significa que no hay coincidencia.

Si quieres una lectura mas util, piensa en esta secuencia:

```text
foto general -> detalle -> filtro
```

| Paso | Qué observas |
|---|---|
| `get all -A` | vista global y ubicacion general |
| `get pods --show-labels` | etiquetas reales para filtrar |
| `describe node` | estado y capacidad de un nodo |
| `-l app=no-existe` | selector vacio como comprobacion |

**[IMAGEN ASCII - reemplazar por imagen]**
```text
get all -> labels -> describe -> selector
```

## Criterio de salida

Si sabes usar `get` para ubicarte, `describe` para bajar al detalle y `-l` para filtrar sin perderte, la practica esta resuelta.
## ➡️ Siguiente

Continua con [Primeros deployments y servicios](../03_Workloads_Basicos/README.md).
