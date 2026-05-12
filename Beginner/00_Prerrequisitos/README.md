# Beginner 00 - Prerrequisitos del laboratorio

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [➡️ Siguiente: 01 - Fundamentos del cluster](../01_Fundamentos/README.md)

## Proposito

Este bloque es una guia de setup.
Su objetivo es dejar una base limpia y conocida para el resto del laboratorio.
No enseña Kubernetes en profundidad; prepara el terreno y valida que el entorno responde bien.

## Modelo mental

Piensa en el setup como una cadena de dependencias:

1. Windows arranca y ofrece virtualizacion.
2. WSL2 aporta una distro Linux usable.
3. Docker Desktop conecta el motor de contenedores con WSL.
4. `kubectl` y `kind` quedan disponibles en el shell correcto.
5. El cluster local se crea sobre una base ya validada.

Si una pieza falla, el resto deja de ser fiable como laboratorio.

## Por que importa

- Evita mezclar errores de instalacion con errores de configuracion de Kubernetes.
- Te obliga a trabajar siempre sobre un estado conocido.
- Hace repetible el resto del aprendizaje.

## Errores tipicos

- usar `kubectl` en Windows y luego seguir la sesion en WSL
- instalar herramientas duplicadas en varios sitios
- crear clusters sobre una base no verificada
- asumir que Docker Desktop esta integrado con WSL sin comprobarlo

## Guia paso a paso

### Paso 1: actualiza la base del sistema

Esto solo confirma que tu Ubuntu de WSL no arranca sobre paquetes viejos o rotos.

```bash
sudo apt update && sudo apt upgrade -y
```

Si este paso falla, el problema no es Kubernetes. Corrige WSL o el acceso a internet antes de seguir.

### Paso 2: valida Docker desde WSL

Primero comprueba que el cliente responde y luego que el daemon realmente esta accesible.

```bash
docker --version
docker info
```

Si `docker --version` funciona pero `docker info` no, el problema no es el binario; es la integracion con Docker Desktop.

### Paso 3: valida las herramientas de Kubernetes

Aqui solo buscas confirmar que `kubectl` y `kind` existen en el shell correcto.

```bash
kubectl version --client --output=yaml
kind version
```

### Paso 4: crea el primer cluster del laboratorio

Este es el punto donde compruebas que todo el setup anterior sirve para algo real.

```bash
kind create cluster --name kind-lab-k8s
kubectl wait --for=condition=Ready node/kind-lab-k8s-control-plane --timeout=120s
kubectl -n kube-system wait deployment/coredns --for=condition=Available --timeout=120s
```

Ahora ya deberias ver el nodo control-plane listo y CoreDNS disponible.

### Paso 5: confirma el contexto y la foto base

La salida de estos tres comandos es la prueba de que el entorno ya quedo utilizable.

```bash
kubectl config current-context
kubectl get nodes -o wide
kubectl get pods -n kube-system
```

## Verificacion rapida

- el contexto activo es `kind-lab-k8s`
- el nodo control-plane esta en `Ready`
- `kube-system` muestra los componentes base en `Running`

## Si algo falla

Si el fallo es de instalacion o PATH, vuelve a [Setup Windows 10/11](../../setup/windows/README.md).

## Cierre

Estar en una maquina limpia y dejarla lista sin depender de instrucciones paso a paso.

### Contexto

No te piden crear aplicaciones todavia.
Te piden llegar a un punto donde el resto del laboratorio ya no pelee con la base.

### Lo que debes conseguir

- una terminal WSL usable
- Docker funcionando en WSL
- herramientas de Kubernetes accesibles
- un cluster local activo y sano

### Lo que debes poder explicar

1. Como sabes que el contexto activo es el correcto.
2. Como distingues un problema de herramienta de un problema de cluster.
3. Que valida `Ready` en el nodo control-plane.

### Criterio de salida

Si no puedes explicar la diferencia entre fallo de instalacion, fallo de contexto y fallo de cluster, no conviene seguir.

## ➡️ Siguiente

Cuando termines, continua con [Beginner 01 - Fundamentos del cluster](../01_Fundamentos/README.md).
