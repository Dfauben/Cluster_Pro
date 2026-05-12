# Beginner 04 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../05_Configuracion_Basica/README.md)

## Contexto

Ya sabes crear workloads basicos. Ahora vas a ver como se exponen dentro del cluster con un `Service` y por qué la entrada estable no depende de la IP de un pod.

## Tarea

Primero creas el service, luego compruebas que apunta a los pods correctos y por ultimo observas que la exposicion sigue viva aunque cambien las replicas.

```bash
kubectl expose deployment hello-k8s --port=80 --target-port=80 --type=ClusterIP
```

Con esto creas la entrada interna estable. El `Service` queda asociado al `Deployment` mediante el selector.

```bash
kubectl get svc hello-k8s
kubectl get endpoints hello-k8s
```

Aqui debes ver la IP estable del service y las IPs reales de los pods detras.

```bash
kubectl scale deployment hello-k8s --replicas=2
kubectl get pods -l app=hello-k8s -o wide
kubectl get endpoints hello-k8s
```

Al cambiar las replicas, el service no deberia romperse. Lo que cambia son los pods y, si hace falta, los endpoints.

| Paso | Qué debes observar |
|---|---|
| crear service | aparece un `ClusterIP` estable |
| revisar endpoints | ves los pods reales detras |
| escalar | cambian las replicas, no la idea del acceso |


<br>

**[IMAGEN ASCII - reemplazar por imagen]**
```text
deployment -> service -> endpoints -> pods
```

## Criterio de salida

La practica queda resuelta cuando sabes crear un service interno, leer su selector y comprobar que el acceso sigue existiendo aunque cambien los pods.
<br>
## ➡️ Siguiente

Continua con [Configuracion basica](../05_Configuracion_Basica/README.md).
