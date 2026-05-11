# Beginner - Tu primer laboratorio real de Kubernetes

## Navegacion

- [Inicio del repositorio](../README.md)
- [Setup - Entorno base](../setup/README.md)
- [Setup Windows 10/11](../setup/windows/README.md)
- [00 - Prerrequisitos](00_Prerrequisitos/README.md)
- [01 - Fundamentos del cluster](01_Fundamentos/README.md)
- [02 - Operacion diaria con kubectl](02_Kubectl_Operacion/README.md)
- [03 - Primeros deployments y servicios](03_Workloads_Basicos/README.md)
- [04 - Services y exposicion basica](04_Services_Exposicion/README.md)
- [05 - Configuracion basica](05_Configuracion_Basica/README.md)
- [06 - Almacenamiento basico](06_Almacenamiento_Basico/README.md)
- [07 - Debug operativo inicial](07_Debug_Operativo/README.md)
- [Indice de conceptos](Conceptos/README.md)


## Indice

- [Inicio](../README.md)
- [Setup - Entorno base](../setup/README.md)
- [Setup Windows 10/11](../setup/windows/README.md)
- [Modulo Beginner](#indice)
  - [Indice de conceptos (Beginner)](Conceptos/README.md)
  - [Submodulo 00 - Prerrequisitos](00_Prerrequisitos/README.md)
  - [Submodulo 01 - Fundamentos del cluster](01_Fundamentos/README.md)
  - [Submodulo 02 - Operacion diaria con kubectl](02_Kubectl_Operacion/README.md)
  - [Submodulo 03 - Primeros deployments y servicios](03_Workloads_Basicos/README.md)
  - [Submodulo 04 - Services y exposicion basica](04_Services_Exposicion/README.md)
  - [Submodulo 05 - Configuracion basica](05_Configuracion_Basica/README.md)
  - [Submodulo 06 - Almacenamiento basico](06_Almacenamiento_Basico/README.md)
  - [Submodulo 07 - Debug operativo inicial](07_Debug_Operativo/README.md)
- [Modulo Intermediate](../Intermediate/README.md)
- [Modulo Pro](../Pro/README.md)

## Descripcion general

Este modulo te lleva de la base operativa a un primer manejo real de Kubernetes desde terminal.
El foco es:

- practicar con comandos concretos
- observar la salida
- provocar fallos controlados cuando aporte valor
- corregir y verificar antes de seguir

Si partes desde un Windows 10/11 limpio y todavia no tienes WSL, empieza por [Setup Windows 10/11](../setup/windows/README.md).

Estructura de cada bloque:

1. Teoria para entender el tema con apoyo visual.
2. Practica guiada para ejecutar paso a paso y observar.
3. Lab para resolver un reto sin ayuda.

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

## Contenido del modulo

<br>

[<img src="../rsc/img/banner_template.png" alt="Prerrequisitos del laboratorio" width="1280" height="160">](00_Prerrequisitos/README.md)

### Prerrequisitos del laboratorio

Validacion de la base ya preparada: WSL, Docker Desktop, `kubectl` y `kind`.
Este bloque tambien crea el primer cluster del laboratorio.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Fundamentos del cluster" width="1280" height="160">](01_Fundamentos/README.md)

### Fundamentos del cluster

Base del cluster: contexto, nodos, namespaces, pods, servicios y recursos API.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Operacion diaria con kubectl" width="1280" height="160">](02_Kubectl_Operacion/README.md)

### Operacion diaria con kubectl

Operacion diaria con `kubectl`: listar, describir, labels, eventos y vistas personalizadas.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Primeros deployments y servicios" width="1280" height="160">](03_Workloads_Basicos/README.md)

### Primeros deployments y servicios

Crear deployment, exponer service, escalar replicas y validar rollout.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Services y exposicion basica" width="1280" height="160">](04_Services_Exposicion/README.md)

### Services y exposicion basica

Exposicion interna con `Service`: selector, ClusterIP y endpoints.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Configuracion basica" width="1280" height="160">](05_Configuracion_Basica/README.md)

### Configuracion basica

Separar configuracion y secretos del contenedor.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Almacenamiento basico" width="1280" height="160">](06_Almacenamiento_Basico/README.md)

### Almacenamiento basico

PVC, PV y StorageClass en un flujo simple.

- [ ] Completado

<br>
<br>

[<img src="../rsc/img/banner_template.png" alt="Debug operativo inicial" width="1280" height="160">](07_Debug_Operativo/README.md)

### Debug operativo inicial

Troubleshooting inicial: logs, describe, eventos y reinicio controlado.

- [ ] Completado

## Apoyo conceptual

Si necesitas reforzar conceptos, usa la biblioteca:

- [Indice de conceptos](Conceptos/README.md)
