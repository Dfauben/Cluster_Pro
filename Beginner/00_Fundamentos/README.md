# Beginner 00 - Fundamentos de gestion K8s

## Indice

- [Modulo Beginner](../README.md)
    - [Submodulo 00 - Fundamentos del cluster](../00_Fundamentos/README.md)
    - [Submodulo 01 - Operacion diaria con kubectl](../01_Kubectl_Operacion/README.md)
    - [Submodulo 02 - Primeros deployments y servicios](../02_Workloads_Basicos/README.md)
    - [Submodulo 03 - Debug operativo inicial](../03_Debug_Operativo/README.md)

## Objetivo

Manejar un cluster desde cero con `kubectl`:
- verificar contexto
- validar salud basica del cluster
- ubicar componentes de control-plane
- entender recursos base: pod, deployment, service

## Regla de ejecucion

Todo este modulo se ejecuta desde **WSL**.
Incluye tambien los comandos de `docker`.

## Prerrequisitos

- WSL2 con Ubuntu operativo.
- Docker con daemon levantado.
- `kubectl` instalado.
- `kind` instalado.
- Cluster `kind-lab-k8s` creado.

## Guia de prerrequisitos (paso a paso)

### 0) Actualiza el sistema primero

```bash
sudo apt update && sudo apt upgrade -y
```

### 1) Comprueba Docker

```bash
docker --version
docker info
```

Si falla:
- Si `docker --version` funciona, **no instales `docker.io`**.
- Solo levanta el servicio:
```bash
sudo service docker start
```
- Si `docker` no existe (`command not found`), instala Docker Engine:
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- Repite:
```bash
docker --version
docker info
```

### 2) Comprueba `kubectl`

```bash
kubectl version --client
```

Si falla:
- Instala `kubectl`:
```bash
sudo apt install -y kubectl
```
- Repite:
```bash
kubectl version --client
```

### 3) Comprueba `kind`

```bash
kind version
```

Si falla:
- Instala `kind`:
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```
- Repite:
```bash
kind version
```

### 4) Crea el cluster de laboratorio

```bash
kind create cluster --name lab-k8s
kubectl wait --for=condition=Ready node/lab-k8s-control-plane --timeout=120s
kubectl -n kube-system wait deployment/coredns --for=condition=Available --timeout=120s
```

### 5) Confirmacion final antes de empezar Beginner 00

```bash
kubectl config current-context
kubectl get nodes -o wide
kubectl get pods -n kube-system
```

Resultado esperado:
- Contexto: `kind-lab-k8s`
- Nodo `lab-k8s-control-plane` en `Ready`
- Pods base en `Running` en `kube-system`

### Si algo no sale como arriba

Pasa el error tal cual y seguimos con correccion guiada.

---

## Antes de tocar nada: valida tu contexto

### `kubectl config current-context`

Que hace:
- Muestra el [contexto de kubectl](../Conceptos/kubectl-context.md) activo (el [cluster](../Conceptos/cluster.md) sobre el que estas operando).

Output esperado (ejemplo):
```text
kind-lab-k8s
```

Como interpretarlo:
- Si ves `kind-lab-k8s`, estas en el lab correcto.
- Si ves otro nombre, podrias ejecutar comandos en el cluster equivocado.

---

## Pulso del [cluster](../Conceptos/cluster.md): estado del nodo

### `kubectl get nodes -o wide`

Que hace:
- Lista [nodes](../Conceptos/node.md) del [cluster](../Conceptos/cluster.md) con informacion ampliada.

Output esperado (ejemplo):
```text
NAME                    STATUS   ROLES           AGE   VERSION   INTERNAL-IP   CONTAINER-RUNTIME
lab-k8s-control-plane   Ready    control-plane   ...   v1.35.0   172.18.0.2    containerd://2.2.0
```

Como interpretarlo:
- `STATUS=Ready`: nodo sano.
- `ROLES=control-plane`: nodo de [control-plane](../Conceptos/control-plane.md).
- `INTERNAL-IP`: [IP interna](../Conceptos/internal-ip.md) de ese nodo.

---

## Mapa logico: espacios de trabajo

### `kubectl get namespaces`

Que hace:
- Lista [namespaces](../Conceptos/namespace.md) (segmentacion logica del cluster).

Output esperado (ejemplo):
```text
NAME                 STATUS   AGE
default              Active   ...
kube-node-lease      Active   ...
kube-public          Active   ...
kube-system          Active   ...
local-path-storage   Active   ...
```

Como interpretarlo:
- `kube-system`: componentes internos de Kubernetes.
- `default`: namespace por defecto para pruebas iniciales.

---

## Vida interna del sistema: pods en ejecucion

### `kubectl get pods -A -o wide`

Que hace:
- Lista todos los [pods](../Conceptos/pod.md) de todos los namespaces.

Output esperado (ejemplo resumido):
```text
NAMESPACE     NAME                                   READY   STATUS    NODE
kube-system   coredns-...                            1/1     Running   lab-k8s-control-plane
kube-system   kube-apiserver-lab-k8s-control-plane   1/1     Running   lab-k8s-control-plane
kube-system   kube-controller-manager-...            1/1     Running   lab-k8s-control-plane
kube-system   kube-scheduler-...                     1/1     Running   lab-k8s-control-plane
kube-system   kube-proxy-...                         1/1     Running   lab-k8s-control-plane
```

Como interpretarlo:
- `READY 1/1` y `STATUS Running`: pod sano.
- Aqui confirmas que el plano de control y [DNS interno](../Conceptos/dns-interno.md) estan levantados.

---

## Como se habla dentro del cluster: servicios base

### `kubectl get svc -A`

Que hace:
- Lista [services](../Conceptos/service.md) (endpoints estables) en todos los namespaces.

Output esperado (ejemplo):
```text
NAMESPACE     NAME         TYPE        CLUSTER-IP   PORT(S)
default       kubernetes   ClusterIP   10.96.0.1    443/TCP
kube-system   kube-dns     ClusterIP   10.96.0.10   53/UDP,53/TCP,9153/TCP
```

Como interpretarlo:
- `kubernetes`: servicio de la [API de Kubernetes](../Conceptos/api-kubernetes.md) del [cluster](../Conceptos/cluster.md).
- `kube-dns`: servicio DNS interno para resolucion entre pods/servicios.

---

## Diccionario de Kubernetes: que recursos existen

### `kubectl api-resources | head -n 25`

Que hace:
- Muestra tipos de recursos disponibles en la API de Kubernetes.

Output esperado (ejemplo resumido):
```text
NAME            SHORTNAMES   APIVERSION   NAMESPACED   KIND
pods            po           v1           true         Pod
services        svc          v1           true         Service
deployments                  apps/v1      true         Deployment
nodes           no           v1           false        Node
namespaces      ns           v1           false        Namespace
```

Como interpretarlo:
- `NAMESPACED=true`: recurso vive dentro de un namespace.
- `NAMESPACED=false`: recurso a nivel cluster (ejemplo: `nodes`).

---

## Anatomia de un pod desde la API

### `kubectl explain pod`

Que hace:
- Describe para que sirve `Pod` y sus campos principales.

Output esperado (inicio):
```text
KIND:       Pod
VERSION:    v1
DESCRIPTION:
    Pod is a collection of containers that can run on a host.
```

Como interpretarlo:
- Te da la definicion oficial y estructura del recurso.
- Es tu referencia rapida antes de crear YAML.

---

## Quien mantiene [replicas](../Conceptos/replicas.md) y [rollout](../Conceptos/rollout.md)

### `kubectl explain deployment`

Que hace:
- Explica el recurso [Deployment](../Conceptos/deployment.md).

Output esperado (inicio):
```text
GROUP:      apps
KIND:       Deployment
VERSION:    v1
DESCRIPTION:
    Deployment enables declarative updates for Pods and ReplicaSets.
```

Como interpretarlo:
- `Deployment` gestiona [replicas](../Conceptos/replicas.md) y actualizaciones de [rollout](../Conceptos/rollout.md) para pods.

---

## Como publicas una app de forma estable

### `kubectl explain service`

Que hace:
- Explica el recurso [Service](../Conceptos/service.md).

Output esperado (inicio):
```text
KIND:       Service
VERSION:    v1
DESCRIPTION:
    Service is a named abstraction of software service...
```

Como interpretarlo:
- `Service` da acceso estable a pods aunque cambien sus IPs.
