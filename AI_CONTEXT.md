# AI Context

Fecha de referencia: 2026-05-11

Este documento es un contexto vivo para mantener alineadas las decisiones de estructura, el estado real del repo y el plan de rework.

## Objetivo del repo

Repo de aprendizaje de Kubernetes con dos usos:
- laboratorio guiado desde cero
- referencia rapida para consulta

El enfoque debe ser:
- teoria clara
- practica guiada paso a paso
- lab sin ayuda como reto
- observacion de resultados
- fallo intencional y correccion

## Estructura objetivo por nivel

Cada tema debe seguir la misma estructura:
- `01_teoria.md`
- `02_practica_guiada.md` o `02_lab.md` segun el bloque
- `03_lab.md` o `03_scenario.md` segun el bloque

Regla funcional:
- `Teoria` = explicacion con tablas, modelo mental y puntos clave
- `Practica guiada` = comandos paso a paso con lectura de salida
- `Lab` = reto sin ayuda, solo con lo ya aprendido en este y otros modulos anteriores

## Principios de nivel

### Beginner

- contenido base
- conceptos esenciales
- lectura del cluster
- kubectl diario
- workloads simples
- services basicos
- config basica
- debug operativo inicial

### Fuera de Beginner

- RBAC avanzado
- admission controllers
- CRDs
- networking avanzado
- troubleshooting profundo
- storage avanzado
- Helm mas serio

## Estado actual del repo

### Ya existe

- `setup/` como entrada de bootstrap
- `Beginner/`
- `Intermediate/`
- `Pro/`
- `Beginner/Conceptos/` como apoyo de lectura rapida

### Ya se elimino

- `PROGRESS.md`

### Bloques revisados

- `Beginner/00_Prerrequisitos` es una guia unica de setup, no un bloque normal de teoria/lab
- `Beginner/01_Fundamentos` ya fue reworkeado al nuevo patrón
- `Beginner/04_Debug_Operativo` fue rebajado de nivel, pero probablemente aun necesite repaso fino

## Decisiones ya fijadas

- `00_Prerrequisitos` no sigue la estructura normal del resto de Beginner
- Beginner no debe llevar setup interno dentro de cada modulo
- `verify.md` ya no forma parte del flujo normal
- `k9s` no se documenta todavia en el repo
- los escenarios no deben sonar guiados; deben poner a prueba conocimientos
- `Service` no se asume en un escenario si el lab no lo crea antes

## Convenciones de contenido

- la teoria debe incluir esquemas, tablas y apoyo visual si ayudan a aprender
- las imagenes pueden ser:
  - ASCII placeholder cuando el contenido sea simple
  - prompt para generar una imagen en otro modelo de IA cuando el esquema merezca un apoyo visual real
- la teoria debe leerse como una explicacion natural, no como un formulario
- evita segmentar en demasiados titulos; usa pocos bloques y apoya con esquemas, tablas, listas o imagenes embebidas dentro del flujo
- cuando uses un placeholder visual, marcala siempre con una etiqueta visible como `[IMAGEN ASCII]` o `[PROMPT IMAGEN]` para que sea obvio que debe sustituirse por una imagen
- las imagenes de teoria en Beginner deben ir en un formato consistente de `1280 x 640 px` salvo que se indique otra cosa
- la practica guiada debe ser narrativa y accionable: paso a paso, con comandos concretos y una explicacion corta despues de cada uno sobre que se espera ver y por que importa
- la practica guiada debe mostrar observacion de salida, no solo lanzar comandos
- la practica guiada debe explicar lo que se observa despues de cada comando
- el lab debe ser un reto real, sin ayuda paso a paso, y solo puede apoyarse en conocimientos del mismo bloque o anteriores
- el lab debe sonar evaluativo, no guiado
- el lab debe plantear un reto factible con lo ya aprendido
- el lab se estructura en: contexto, tarea y criterio de salida
- no mezclar varios niveles de dificultad en el mismo bloque
- no meter contenido de etapas posteriores dentro de Beginner

## Esquema propuesto para Beginner

### 0. Setup del entorno

- Windows / WSL / Docker Desktop / kind / kubectl
- verificacion
- primer cluster
- limpieza basica

### 1. Fundamentos del cluster

- contexto
- nodos
- namespaces
- `kube-system`
- `api-resources`
- `kubectl explain`

### 2. kubectl y lectura operativa

- `get`
- `describe`
- labels
- selectors
- lectura rapida de estado

### 3. Pods y workloads basicos

- `Pod`
- `Deployment`
- `ReplicaSet`
- replicas
- rollout basico
- escala

### 4. Services y exposicion basica

- `Service`
- `ClusterIP`
- `NodePort`
- selectors de service

### 5. Configuracion basica de workloads

- `ConfigMap`
- `Secret`
- variables de entorno
- mounts simples

### 6. Debug operativo inicial

- `logs`
- `describe`
- `events`
- restart solo cuando procede

### 7. Almacenamiento basico

- `PV`
- `PVC`
- `StorageClass`

## Pendiente inmediato

- Reestructurar el resto de `Beginner` para que siga el mismo patrón que `01_Fundamentos`
- Revisar si `02_Kubectl_Operacion`, `03_Workloads_Basicos` y `04_Debug_Operativo` siguen el mismo nivel y forma
- Definir si `Beginner/04_Debug_Operativo` debe mantenerse o fusionarse con otro modulo
- Seguir con la segmentacion por temas antes de tocar `Intermediate`

## Regla de trabajo

Antes de implementar cambios grandes:
- revisar este documento
- revisar el modulo afectado
- mantener consistencia entre teoria, practica guiada y lab

## Navegacion entre md

- cada md debe ofrecer una ruta clara de subida al indice del bloque y una ruta lineal al bloque anterior/siguiente cuando exista
- los README de modulo deben enlazar con:
  - el README del nivel superior
  - el bloque anterior
  - el bloque siguiente
  - el indice interno del modulo
- los md de contenido deben enlazar con:
  - el README del modulo
  - el contenido anterior
  - el contenido siguiente
- la navegacion debe ser obvia sin obligar al usuario a volver al indice general para seguir avanzando
