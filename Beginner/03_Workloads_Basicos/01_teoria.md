# Beginner 03 - Primeros deployments y servicios


## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](README.md)
- [➡️ Siguiente](02_lab.md)

Cuando creas una aplicacion en Kubernetes, no piensas solo en [pods](../Conceptos/pod.md). Piensas en el estado que quieres mantener, en cuantas copias necesitas y en como vas a acceder a ellas sin depender de una IP fragil.

**[IMAGEN ASCII - reemplazar por imagen]**
```text
Deployment -> ReplicaSet -> Pods
                    \
                     -> Service
```

La pieza importante aqui es que cada objeto hace un trabajo distinto. El [`Deployment`](../Conceptos/deployment.md) describe el estado deseado y controla los cambios. El [`ReplicaSet`](../Conceptos/replicaset.md) sostiene el numero de copias que deben existir. Los [pods](../Conceptos/pod.md) son la ejecucion real. Y el [`Service`](../Conceptos/service.md) ofrece una entrada estable para llegar a esos pods sin engancharte a una IP concreta.

| Concepto | Qué representa | Qué debes entender |
|---|---|---|
| [`Deployment`](../Conceptos/deployment.md) | estado deseado | decide cuantas copias debe haber y como evolucionan |
| [`ReplicaSet`](../Conceptos/replicaset.md) | copia controlada | mantiene el numero exacto de pods |
| [`Pod`](../Conceptos/pod.md) | ejecucion real | puede cambiar o recrearse |
| [`Service`](../Conceptos/service.md) | acceso estable | mantiene una entrada fija hacia los pods correctos |
| [`ClusterIP`](../Conceptos/clusterip.md) | acceso interno | expone el service dentro del cluster |


<br>

Cuando escalas o actualizas, Kubernetes no inventa una nueva regla cada vez. Reconcilia el estado hasta volver a lo que pediste. Por eso es importante separar lo que se gestiona de forma estable de lo que puede desaparecer y volver a salir. El [pod](../Conceptos/pod.md) puede cambiar; la idea del workload debe seguir viva.

```text
estado deseado -> reconciliacion -> pods vivos -> acceso estable
```

Si lo llevas a operacion real, la pregunta correcta no es "que pod tengo ahora". La pregunta es "que controlador lo mantiene, cuantos deberia haber y como accedo a el sin depender de una IP concreta". Esa diferencia es la base de casi todo lo que haces despues en Kubernetes.

**[IMAGEN ASCII - reemplazar por imagen]**
```text
app estable
├── controlador
├── replicas
├── ejecucion efimera
└── acceso interno
```

**Errores tipicos**
- pensar que el pod es la unidad principal de gestion
- confundir la IP del pod con una IP estable
- creer que escalar es crear pods a mano
- no comprobar que el [rollout](../Conceptos/rollout.md) termino bien

**Qué debes retener**
- el deployment describe y sostiene el estado deseado
- los pods son la parte que cambia
- el service da una entrada estable
- `ClusterIP` es la forma basica de acceso interno
- Kubernetes reconcilia, no improvisa

> **[PROMPT IMAGEN - generar fuera del repo]**
> Genera un diagrama educativo sobre el ciclo de vida de una app en Kubernetes: `Deployment` -> `ReplicaSet` -> `Pods`, con un `Service` apuntando a los pods. Estilo limpio, pocas cajas, flechas claras y etiquetas sencillas, fondo simple y didáctico.

## ➡️ Siguiente

Continua con [Practica guiada](02_lab.md).
