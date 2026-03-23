# Intermediate 00 - Cluster y Nodos

## Objetivo

Crear y operar un cluster multinodo local para practicar maniobras reales de infraestructura:
- creacion y borrado de cluster
- topologia con control-plane y workers
- operaciones de nodo con [cordon/drain/uncordon](../Conceptos/cordon-drain-uncordon.md)

## Prerrequisitos

- Docker operativo en WSL.
- `kind` y `kubectl` instalados.

## Escenario recomendado

Usaremos un cluster dedicado para Intermediate:
- nombre: `int-lab`
- configuracion: `../kind-configs/multi-node.yaml`

---

## Arranca un cluster multinodo limpio

### `kind delete cluster --name int-lab 2>/dev/null || true`

Que hace:
- Elimina cluster previo `int-lab` si existia.

Output esperado:
```text
Deleting cluster "int-lab" ...
```
o sin salida si no existia.

Como interpretarlo:
- Garantiza un inicio limpio para la practica.

---

### `kind create cluster --name int-lab --image kindest/node:v1.35.0 --config Intermediate/kind-configs/multi-node.yaml`

Que hace:
- Crea cluster multinodo usando el archivo de configuracion.

Output esperado (ejemplo resumido):
```text
Creating cluster "int-lab" ...
Set kubectl context to "kind-int-lab"
```

Como interpretarlo:
- Se crea un control-plane y dos workers.
- El contexto de `kubectl` cambia a `kind-int-lab`.

---

### `kubectl config use-context kind-int-lab`

Que hace:
- Asegura que los siguientes comandos apunten al cluster correcto.

Output esperado:
```text
Switched to context "kind-int-lab".
```

Como interpretarlo:
- Evitas operar por error en otro cluster.

---

### `kubectl cluster-info --context kind-int-lab`

Que hace:
- Muestra endpoints principales del cluster.

Output esperado (ejemplo):
```text
Kubernetes control plane is running at https://127.0.0.1:...
```

Como interpretarlo:
- Confirma que la API esta alcanzable.

---

### `kubectl get nodes -o wide`

Que hace:
- Lista nodos y estado.

Output esperado (ejemplo resumido):
```text
NAME                       STATUS   ROLES           VERSION
int-lab-control-plane      Ready    control-plane   v1.35.0
int-lab-worker             Ready    <none>          v1.35.0
int-lab-worker2            Ready    <none>          v1.35.0
```

Como interpretarlo:
- Debes ver 3 nodos `Ready`.
- Si un nodo esta `NotReady`, espera un poco y revisa pods en `kube-system`.

---

## Bloquea scheduling en un worker (sin apagarlo)

### `kubectl cordon int-lab-worker`

Que hace:
- Marca el nodo como no elegible para nuevos pods.

Output esperado:
```text
node/int-lab-worker cordoned
```

Como interpretarlo:
- Los pods existentes siguen, pero no se agendan pods nuevos ahi.

---

### `kubectl get nodes`

Que hace:
- Verifica estado del nodo tras cordon.

Output esperado (ejemplo):
```text
int-lab-worker   Ready    <none>   ...   SchedulingDisabled
```

Como interpretarlo:
- `SchedulingDisabled` confirma que el cordon esta activo.

---

### `kubectl uncordon int-lab-worker`

Que hace:
- Revierte el cordon y reabre scheduling.

Output esperado:
```text
node/int-lab-worker uncordoned
```

Como interpretarlo:
- El nodo vuelve a recibir pods nuevos.

---

## Simula mantenimiento real con drain

### `kubectl drain int-lab-worker --ignore-daemonsets --delete-emptydir-data`

Que hace:
- Evacua pods reubicables del nodo para mantenimiento.

Output esperado (ejemplo resumido):
```text
node/int-lab-worker already cordoned
evicting pod ...
node/int-lab-worker drained
```

Como interpretarlo:
- El nodo queda vaciado de workloads movibles.
- DaemonSets no se eliminan por diseno.

---

### `kubectl get pods -A -o wide`

Que hace:
- Comprueba reubicacion de pods tras drain.

Output esperado:
- Pods de tus apps en otros nodos disponibles.

Como interpretarlo:
- Si hay pods pendientes, revisa restricciones de scheduling.

---

### `kubectl uncordon int-lab-worker`

Que hace:
- Rehabilita nodo tras mantenimiento.

Notas importantes:
- No drenar el `control-plane` en este lab.
- `drain` reubica cargas; en entorno productivo requiere plan de impacto.

---

## Limpieza opcional

```bash
kind delete cluster --name int-lab
```
