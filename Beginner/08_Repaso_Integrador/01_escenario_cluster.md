# Beginner 08 - Escenario 01: fotografia completa del cluster


## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del repaso](README.md)
- [⬅️ Anterior](README.md)
- [➡️ Siguiente](02_escenario_app.md)

## Contexto

Tienes acceso a un cluster ya levantado en kind. El objetivo no es cambiar nada, sino sacar una fotografia base completa y explicar si reconoces lo esencial del entorno.

## Estado existente

- un cluster sano ya creado
- contexto de kubectl ya apuntando al cluster del lab
- namespaces del sistema y de usuario disponibles
- componentes de `kube-system` levantados

## Tarea

- confirmar el contexto activo
- identificar el nodo control-plane
- listar namespaces
- identificar los componentes de `kube-system`
- agrupar recursos de la API por familia

## Qué debes entregar

1. el contexto activo
2. el nodo o nodos principales del cluster
3. los namespaces que existen
4. una lectura breve de `kube-system`
5. una agrupacion de recursos de la API por tipo o familia

## Criterio de salida

Si puedes describir el cluster por capas sin abrir YAML ni perderte en la salida, el escenario esta resuelto.
## ➡️ Siguiente

Continua con [Escenario 02](02_escenario_app.md).
