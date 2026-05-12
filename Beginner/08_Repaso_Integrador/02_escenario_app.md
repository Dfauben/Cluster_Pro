# Beginner 08 - Escenario 02: aplicacion expuesta y configurada


## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del repaso](README.md)
- [⬅️ Anterior](01_escenario_cluster.md)
- [➡️ Siguiente](03_escenario_debug.md)

## Contexto

Te dejan una aplicacion sencilla ya desplegada en el cluster. Debes comprobar que entiendes como se ejecuta, como se expone y como recibe configuracion sin rehacer la imagen.

## Estado existente

- un `Deployment` funcional
- un `Service` interno que apunta a la aplicacion
- un `ConfigMap` con valores no sensibles
- un `Secret` con valores sensibles
- pods levantados y en estado estable

## Tarea

- localizar el `Deployment`
- localizar los `Pods`
- localizar el `Service`
- comprobar la relacion entre `Service` y `Pods`
- verificar que la configuracion entra al pod
- explicar como cambiar el numero de replicas sin romper el acceso

## Qué debes entregar

1. el nombre del `Deployment`
2. el `Service` que da acceso estable
3. los `Pods` que estan detras del service
4. la evidencia de que la configuracion externa llega al pod
5. una explicacion corta de que cambia y que no cambia al escalar

## Criterio de salida

Si puedes demostrar que sabes separar ejecucion, acceso y configuracion, el escenario esta resuelto.
<br>

## ➡️ Siguiente

Continua con [Escenario 03](03_escenario_debug.md).
