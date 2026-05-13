# Beginner - Tu primer laboratorio real de Kubernetes

## Navegacion

- [🏠 Inicio del repositorio](../README.md)
- [🧰 Setup - Entorno base](../setup/README.md)
- [🪟 Setup Windows 10/11](../setup/windows/README.md)
- [📘 00 - Prerrequisitos](00_Prerrequisitos/README.md)
- [📘 01 - Fundamentos del cluster](01_Fundamentos/README.md)
- [📘 02 - Operacion diaria con kubectl](02_Kubectl_Operacion/README.md)
- [📘 03 - Despliegues imperativos](03_Workloads_Basicos/README.md)
- [📘 04 - Despliegues declarativos](04_Workloads_Declarativos/README.md)
- [📘 05 - Services y exposicion basica](05_Services_Exposicion/README.md)
- [📘 06 - Configuracion basica](06_Configuracion_Basica/README.md)
- [📘 07 - Almacenamiento basico](07_Almacenamiento_Basico/README.md)
- [📘 08 - Debug operativo inicial](08_Debug_Operativo/README.md)
- [🧩 09 - Repaso integrador](09_Repaso_Integrador/README.md)
- [🗂️ Indice de conceptos](Conceptos/README.md)

## Descripcion general

Este modulo te lleva de la base operativa a un primer manejo real de Kubernetes desde terminal.
El foco es:

- practicar con comandos concretos
- observar la salida
- provocar fallos controlados cuando aporte valor
- corregir y verificar antes de seguir

Si partes desde un Windows 10/11 limpio y todavia no tienes WSL, empieza por [Setup Windows 10/11](../setup/windows/README.md).

Estructura de los bloques regulares:

1. Teoria para entender el tema con apoyo visual.
2. Practica guiada para ejecutar paso a paso y observar.

El bloque final `09 - Repaso integrador` agrupa escenarios largos para consolidar lo aprendido.

Formato visual de este modulo:

- Banner del README del modulo: `1280 x 640 px`
- Banner de cada submodulo: `1280 x 160 px`

## A quien va dirigido y dificultad

Orientado a:

- personas que empiezan en Kubernetes
- perfiles de desarrollo/DevOps que quieren base operativa solida
- aprendizaje practico en laboratorio local

Nivel de dificultad:

- Bajo a medio
- Requiere comodidad basica con terminal Linux

Al terminar este modulo deberias poder:

- validar un entorno WSL listo para Kubernetes
- validar salud de cluster y nodos
- inspeccionar recursos y diagnosticar problemas iniciales
- desplegar una app basica con comandos directos
- describir un workload basico en YAML y aplicarlo
- exponer y escalar una app simple cuando toque

## Resumen del modulo

| Tema | Que cubre | Enlace |
|---|---|---|
| 00 - Prerrequisitos | Base del entorno y primer cluster | [Abrir](00_Prerrequisitos/README.md) |
| 01 - Fundamentos del cluster | Contexto, nodos, namespaces, pods y API | [Abrir](01_Fundamentos/README.md) |
| 02 - Operacion diaria con kubectl | Lectura rapida con `kubectl` | [Abrir](02_Kubectl_Operacion/README.md) |
| 03 - Despliegues imperativos | Crear y escalar una app con comandos directos | [Abrir](03_Workloads_Basicos/README.md) |
| 04 - Despliegues declarativos | YAML, `apply` y estado deseado | [Abrir](04_Workloads_Declarativos/README.md) |
| 05 - Services y exposicion basica | `Service`, `ClusterIP` y `EndpointSlice` | [Abrir](05_Services_Exposicion/README.md) |
| 06 - Configuracion basica | `ConfigMap`, `Secret` y variables de entorno | [Abrir](06_Configuracion_Basica/README.md) |
| 07 - Almacenamiento basico | `PV`, `PVC` y `StorageClass` | [Abrir](07_Almacenamiento_Basico/README.md) |
| 08 - Debug operativo inicial | `logs`, `describe`, `events` y reinicio controlado | [Abrir](08_Debug_Operativo/README.md) |
| 09 - Repaso integrador | Escenarios largos de consolidacion | [Abrir](09_Repaso_Integrador/README.md) |

## Apoyo conceptual

Si necesitas reforzar conceptos, usa la biblioteca:

- [Indice de conceptos](Conceptos/README.md)
