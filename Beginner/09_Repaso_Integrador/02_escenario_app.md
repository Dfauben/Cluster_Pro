# Beginner 09 - Escenario 02: aplicacion expuesta y configurada


## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del repaso](README.md)
- [⬅️ Anterior](01_escenario_cluster.md)
- [➡️ Siguiente](03_escenario_debug.md)

## Contexto

Te dejan una aplicacion sencilla ya desplegada en el cluster. La pista inicial es que la app base se llama `hello-k8s`. Debes comprobar que entiendes como se ejecuta, como se expone y como recibe configuracion sin crear nada nuevo.

## Estado existente

- recursos ya creados en los bloques anteriores

## Tarea

- localizar el `Deployment` principal de la aplicacion
- localizar los `Pods` que estan detras del `Service`
- localizar el `Service` que da acceso estable
- comprobar la relacion entre `Service` y `Pods`
- localizar el `ConfigMap` y el `Secret`
- verificar que la configuracion entra al pod
- explicar como cambiar el numero de replicas sin romper el acceso

## Qué debes entregar

1. el nombre del `Deployment`
2. el `Service` que da acceso estable
3. los `Pods` que estan detras del service
4. el `ConfigMap` y el `Secret` que encontraste
5. la evidencia de que la configuracion externa llega al pod
6. una explicacion corta de que cambia y que no cambia al escalar

## Criterio de salida

Si puedes demostrar que sabes separar ejecucion, acceso y configuracion, el escenario esta resuelto.
<br>

## ➡️ Siguiente

Continua con [Escenario 03](03_escenario_debug.md).
