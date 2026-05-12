# Beginner 02 - Operacion diaria con kubectl


## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](README.md)
- [➡️ Siguiente](02_lab.md)

[`kubectl`](../Conceptos/kubectl-context.md) no es una lista de trucos. Es la forma mas directa de preguntarle al cluster que esta pasando. Cuando aprendes a usarlo bien, dejas de mirar pantallas completas y empiezas a leer solo lo que importa.

**[IMAGEN ASCII - reemplazar por imagen]**
```text
usuario -> kubectl -> [API server](../Conceptos/api-kubernetes.md) -> recursos del cluster
```

La idea operativa es simple: unas veces quieres una foto rapida, otras un detalle concreto y otras un filtro muy especifico. `kubectl` cambia de herramienta segun la pregunta, no segun la costumbre.

| Si quieres saber... | Usa... | Qué te aporta |
|---|---|---|
| que hay en el cluster | `get` | una foto rapida |
| como esta algo por dentro | [`describe`](../Conceptos/kubectl-describe.md) | contexto, condiciones y eventos |
| solo lo que encaja con una etiqueta | [`-l`](../Conceptos/labels.md) | filtrado exacto |
| si un filtro no devuelve nada | selector vacio | confirmacion de que no hay coincidencia |
| como leer mejor una salida | [`custom-columns`](../Conceptos/custom-columns.md) | una vista adaptada a lo que te interesa |

Cuando usas `get`, piensas en amplitud. Cuando usas [`describe`](../Conceptos/kubectl-describe.md), piensas en detalle. Cuando usas [labels](../Conceptos/labels.md) o [selectors](../Conceptos/selector.md), piensas en seleccionar lo minimo necesario para no perderte. Esa es la diferencia entre mirar Kubernetes y entenderlo.

```text
foto general -> detalle -> filtro -> lectura propia
```

En este nivel no buscas exprimir la API. Buscas aprender a elegir la vista correcta.
Si ves una salida larga, no la des por buena solo porque sea completa. Preguntate si realmente responde a lo que querias saber. En operacion real, un comando mas corto y mejor pensado suele aportar mas que una salida enorme.

**[IMAGEN ASCII - reemplazar por imagen]**
```text
get        -> lo que hay
describe   -> como esta
-l         -> que coincide
columns    -> como lo quiero ver
```

**Errores tipicos**
- usar `get all` como respuesta universal
- confundir labels con decoracion
- pedir demasiada informacion cuando solo necesitas una foto
- no distinguir entre salida util y salida larga

**Qué debes retener**
- `kubectl` sirve para leer, no solo para ejecutar
- `get` y `describe` responden preguntas distintas
- labels y selectors son la forma real de filtrar recursos
- una buena lectura de salida ahorra tiempo y errores

> **[PROMPT IMAGEN - generar fuera del repo]**
> Genera un diagrama didáctico sobre `kubectl` como herramienta de lectura del cluster. Debe mostrar el flujo usuario -> kubectl -> API server -> recursos, y una segunda capa con `get`, `describe`, `labels/selectors` y `custom-columns`. Estilo limpio, educativo, fondo simple y sin ruido visual.

## ➡️ Siguiente

Continua con [Practica guiada](02_lab.md).
