# Beginner - Tu primer laboratorio real de Kubernetes

## Navegacion

- [🏠 Inicio del repositorio](../README.md)
- [🧰 Setup - Entorno base](../setup/README.md)
- [🪟 Setup Windows 10/11](../setup/windows/README.md)
- [📘 00 - Prerrequisitos](00_Prerrequisitos/README.md)
- [📘 01 - Fundamentos del cluster](01_Fundamentos/README.md)
- [📘 02 - Operacion diaria con kubectl](02_Kubectl_Operacion/README.md)
- [📘 03 - Primeros deployments y servicios](03_Workloads_Basicos/README.md)
- [📘 04 - Services y exposicion basica](04_Services_Exposicion/README.md)
- [📘 05 - Configuracion basica](05_Configuracion_Basica/README.md)
- [📘 06 - Almacenamiento basico](06_Almacenamiento_Basico/README.md)
- [📘 07 - Debug operativo inicial](07_Debug_Operativo/README.md)
- [🧩 08 - Repaso integrador](08_Repaso_Integrador/README.md)
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

El bloque final `08 - Repaso integrador` agrupa escenarios largos para consolidar lo aprendido.

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
- desplegar una app basica y exponerla internamente
- operar cambios simples en una app

## Resumen del modulo

| Tema | Que cubre | Enlace |
|---|---|---|
| 00 - Prerrequisitos | Base del entorno y primer cluster | [Abrir](00_Prerrequisitos/README.md) |
| 01 - Fundamentos del cluster | Contexto, nodos, namespaces, pods y API | [Abrir](01_Fundamentos/README.md) |
| 02 - Operacion diaria con kubectl | Lectura rapida con `kubectl` | [Abrir](02_Kubectl_Operacion/README.md) |
| 03 - Primeros deployments y servicios | `Deployment`, `ReplicaSet`, `Pod` y `Service` | [Abrir](03_Workloads_Basicos/README.md) |
| 04 - Services y exposicion basica | `Service`, `ClusterIP` y endpoints | [Abrir](04_Services_Exposicion/README.md) |
| 05 - Configuracion basica | `ConfigMap`, `Secret` y variables de entorno | [Abrir](05_Configuracion_Basica/README.md) |
| 06 - Almacenamiento basico | `PV`, `PVC` y `StorageClass` | [Abrir](06_Almacenamiento_Basico/README.md) |
| 07 - Debug operativo inicial | `logs`, `describe`, `events` y reinicio controlado | [Abrir](07_Debug_Operativo/README.md) |
| 08 - Repaso integrador | Escenarios largos de consolidacion | [Abrir](08_Repaso_Integrador/README.md) |

## Apoyo conceptual

Si necesitas reforzar conceptos, usa la biblioteca:

- [Indice de conceptos](Conceptos/README.md)
