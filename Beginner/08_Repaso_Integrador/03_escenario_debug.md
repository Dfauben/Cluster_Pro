# Beginner 08 - Escenario 03: diagnostico de una app que no arranca


## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del repaso](README.md)
- [⬅️ Anterior](02_escenario_app.md)
- [➡️ Siguiente](README.md)

## Contexto

Te dan una aplicacion que no termina de arrancar del todo. No te piden rehacerla: te piden diagnosticarla con orden y decidir si reiniciar ayuda o no.

## Estado existente

- un `Deployment` creado
- pods del workload con estado anomalo o no estable
- logs disponibles
- eventos disponibles

## Tarea

- sacar la primera pista con logs
- revisar el estado del pod con describe
- usar events si sigue faltando contexto
- decidir si un reinicio tiene sentido

## Qué debes entregar

1. la primera causa o pista util que has encontrado
2. el estado del pod
3. el evento o detalle que aclara el problema
4. una decision razonada sobre si reiniciar ayuda

## Criterio de salida

Si puedes seguir el orden correcto, identificar la causa util y decidir con criterio si reiniciar aporta algo, el escenario esta resuelto.
## ➡️ Siguiente

Continua con [Indice del repaso](../README.md).
