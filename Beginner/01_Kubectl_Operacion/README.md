# Beginner 01 - Kubectl para operacion diaria

## Indice

- [Modulo Beginner](../README.md)
    - [Submodulo 00 - Fundamentos del cluster](../00_Fundamentos/README.md)
    - [Submodulo 01 - Operacion diaria con kubectl](../01_Kubectl_Operacion/README.md)
    - [Submodulo 02 - Primeros deployments y servicios](../02_Workloads_Basicos/README.md)
    - [Submodulo 03 - Debug operativo inicial](../03_Debug_Operativo/README.md)

## Objetivo

Dominar comandos de gestion basicos:
- listar
- describir
- filtrar por labels
- ver eventos

## Prerrequisitos

- Cluster `kind-lab-k8s` activo.
- Modulo `Beginner/00_Fundamentos` revisado.

---

## Vista panoramica del cluster

### `kubectl get all -A`

Que hace:
- Lista recursos basicos en todos los [namespaces](../Conceptos/namespace.md) del [cluster](../Conceptos/cluster.md): [pods](../Conceptos/pod.md), [services](../Conceptos/service.md), [deployments](../Conceptos/deployment.md), [replicasets](../Conceptos/replicaset.md) y [daemonsets](../Conceptos/daemonset.md).

Output esperado (ejemplo resumido):
```text
NAMESPACE            NAME                                                READY   STATUS
kube-system          pod/kube-apiserver-lab-k8s-control-plane            1/1     Running

NAMESPACE     NAME                 TYPE        CLUSTER-IP   PORT(S)
default       service/kubernetes   ClusterIP   10.96.0.1    443/TCP

NAMESPACE     NAME                        DESIRED   CURRENT   READY
kube-system   daemonset.apps/kube-proxy   1         1         1

NAMESPACE            NAME                                     READY   UP-TO-DATE   AVAILABLE
kube-system          deployment.apps/coredns                  2/2     2            2
```

Como interpretarlo:
- Es tu foto rapida del estado general.
- `get all` no muestra todos los tipos de recurso (por ejemplo `configmaps`), solo un subconjunto util para operacion diaria.

---

## Identidad de pods: labels visibles

### `kubectl get pods -A --show-labels`

Que hace:
- Muestra pods y sus [labels](../Conceptos/labels.md).

Output esperado (ejemplo resumido):
```text
NAMESPACE    NAME                                 STATUS    LABELS
kube-system  coredns-...                          Running   k8s-app=kube-dns,pod-template-hash=...
kube-system  kube-apiserver-lab-k8s-control-plane Running   component=kube-apiserver,tier=control-plane
```

Como interpretarlo:
- Las labels son pares `clave=valor`.
- Sirven para seleccionar recursos (`-l app=...`) y para que los [services](../Conceptos/service.md) encuentren pods backend.

---

## Radiografia del nodo de control

### `kubectl describe node lab-k8s-control-plane`

Que hace:
- Ejecuta una inspeccion profunda del [node](../Conceptos/node.md) usando [kubectl describe](../Conceptos/kubectl-describe.md): condiciones, capacidad, recursos asignados y metadatos.

Output esperado (ejemplo resumido):
```text
Name:               lab-k8s-control-plane
Roles:              control-plane
Conditions:
  Ready            True
Addresses:
  InternalIP:      172.18.0.2
Capacity:
  cpu:             12
Allocated resources:
  cpu              950m (7%)
Events:            <none>
```

Como interpretarlo:
- `Ready=True` indica nodo utilizable.
- `Capacity` vs `Allocated resources` te dice margen disponible.
- `Events` ayuda a detectar presion de recursos o problemas recientes.

---

## Linea de tiempo operativa: eventos

### `kubectl get events -A --sort-by=.metadata.creationTimestamp`

Que hace:
- Lista [eventos](../Conceptos/events.md) del cluster, ordenados de mas antiguos a mas recientes.

Output esperado:
```text
No resources found
```
o bien:
```text
NAMESPACE  LAST SEEN  TYPE     REASON      OBJECT     MESSAGE
...
```

Como interpretarlo:
- `No resources found` no implica error; solo que no hay eventos recientes almacenados.
- Si hay eventos, revisa especialmente `Warning` y razones repetidas.

---

## Tu propia tabla de control

### `kubectl get pods -A -o custom-columns='NAMESPACE:.metadata.namespace,NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName'`

Que hace:
- Crea una salida personalizada con [custom columns](../Conceptos/custom-columns.md) para enfocarte en campos operativos clave.

Output esperado (ejemplo):
```text
NAMESPACE            NAME                                            STATUS    NODE
kube-system          kube-apiserver-lab-k8s-control-plane            Running   lab-k8s-control-plane
local-path-storage   local-path-provisioner-67b8995b4b-s4cdv         Running   lab-k8s-control-plane
```

Como interpretarlo:
- Esta vista simplificada acelera chequeos diarios.
- Puedes agregar columnas adicionales segun tu necesidad (por ejemplo IP o reinicios).
