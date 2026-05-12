# Beginner 07 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../08_Repaso_Integrador/README.md)

## Contexto

Tienes un workload basico en marcha y quieres aprender a leer un fallo sin empezar reiniciando a ciegas.

## Tarea

Primero miras la evidencia mas barata, luego bajas al detalle del pod, despues usas events si falta contexto y al final haces un reinicio controlado solo si sigue teniendo sentido.

```bash
kubectl logs -l app=hello-k8s --tail=50 --prefix=true
```

Esto suele darte la primera pista. No busques una solucion aqui; busca si hay arranque normal, error claro o silencio sospechoso.

```bash
kubectl describe pod -l app=hello-k8s
```

Ahora bajas al estado del pod. Aqui suelen aparecer el motivo util del fallo, las condiciones y la pista que faltaba en los logs.

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

Si logs y describe no bastan, eventos te ordena la cronologia. Te ayuda a ver si el fallo empezo antes, durante o despues del arranque.

```bash
kubectl rollout restart deployment/hello-k8s
kubectl rollout status deployment/hello-k8s
```

Solo haces este paso cuando ya has entendido que reiniciar puede ayudar de verdad. El objetivo no es reiniciar por costumbre, sino comprobar que el rollout vuelve a converger.

| Paso | Qué debes observar |
|---|---|
| logs | primera pista de ejecucion |
| describe | motivo util del fallo |
| events | secuencia temporal |
| restart | convergencia tras la correccion |


<br>

**[IMAGEN ASCII - reemplazar por imagen]**
```text
logs -> describe -> events -> restart
```

## Criterio de salida

La practica queda resuelta cuando sabes leer el fallo en orden y entiendes por que reiniciar antes de tiempo no arregla nada.
<br>
## ➡️ Siguiente

Continua con [Repaso integrador](../08_Repaso_Integrador/README.md).
