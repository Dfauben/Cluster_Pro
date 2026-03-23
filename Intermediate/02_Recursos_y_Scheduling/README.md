# Intermediate 02 - Recursos y Scheduling

## Objetivo

Aprender control de placement y capacidad:
- `requests` y `limits`
- `nodeSelector`
- `taints` y `tolerations`

## Prerrequisitos

- Haber completado `Intermediate/00_Cluster_y_Nodos` (cluster multinodo disponible).
- Namespace de pruebas libre (usaremos `int-scheduling`).

---

## Crea namespace de trabajo

### `kubectl create namespace int-scheduling --dry-run=client -o yaml | kubectl apply -f -`

Que hace:
- Crea namespace para este laboratorio.

Output esperado:
```text
namespace/int-scheduling created
```

Como interpretarlo:
- Aislas pruebas de scheduling del resto.

---

## Prepara un worker dedicado

### `kubectl get nodes`

Que hace:
- Lista nodos disponibles para elegir worker.

---

### `kubectl label node int-lab-worker workload=apps --overwrite`

Que hace:
- Etiqueta worker para usar [nodeSelector](../Conceptos/nodeselector.md).

Output esperado:
```text
node/int-lab-worker labeled
```

---

### `kubectl taint nodes int-lab-worker dedicated=apps:NoSchedule`

Que hace:
- Aplica [taint](../Conceptos/taints-tolerations.md) que bloquea pods sin toleration.

Output esperado:
```text
node/int-lab-worker tainted
```

---

## Crea pod con nodeSelector pero sin toleration (debe fallar scheduling)

### `cat <<'EOF' | kubectl apply -n int-scheduling -f -`

Comando completo:
```bash
cat <<'EOF' | kubectl apply -n int-scheduling -f -
apiVersion: v1
kind: Pod
metadata:
  name: scheduling-demo-no-toleration
  labels:
    app: scheduling-demo
spec:
  nodeSelector:
    workload: apps
  containers:
  - name: app
    image: nginx:stable
    resources:
      requests:
        cpu: "100m"
        memory: "128Mi"
      limits:
        cpu: "250m"
        memory: "256Mi"
EOF
```

Que hace:
- Crea pod con [requests/limits](../Conceptos/requests-limits.md) y nodeSelector al nodo taintado, sin toleration.

Output esperado:
```text
pod/scheduling-demo-no-toleration created
```

Como interpretarlo:
- Se crea el objeto, pero el pod quedara `Pending` por taint.

---

## Confirma el motivo del Pending

### `kubectl get pod scheduling-demo-no-toleration -n int-scheduling`

Output esperado:
```text
STATUS   Pending
```

---

### `kubectl describe pod scheduling-demo-no-toleration -n int-scheduling`

Que hace:
- Muestra la razon precisa de scheduling fallido.

Output esperado (ejemplo):
```text
Warning  FailedScheduling  ...  node(s) had taint {dedicated: apps}, that the pod didn't tolerate
```

Como interpretarlo:
- Confirmas que falta toleration.

---

## Aplica version correcta con toleration

### `cat <<'EOF' | kubectl apply -n int-scheduling -f -`

Comando completo:
```bash
cat <<'EOF' | kubectl apply -n int-scheduling -f -
apiVersion: v1
kind: Pod
metadata:
  name: scheduling-demo-ok
  labels:
    app: scheduling-demo
spec:
  nodeSelector:
    workload: apps
  tolerations:
  - key: "dedicated"
    operator: "Equal"
    value: "apps"
    effect: "NoSchedule"
  containers:
  - name: app
    image: nginx:stable
    resources:
      requests:
        cpu: "100m"
        memory: "128Mi"
      limits:
        cpu: "250m"
        memory: "256Mi"
EOF
```

Que hace:
- Crea pod con misma afinidad al worker, ahora con toleration valida.

Output esperado:
```text
pod/scheduling-demo-ok created
```

Como interpretarlo:
- Este pod si debe arrancar en `int-lab-worker`.

---

## Verifica placement final

### `kubectl get pods -n int-scheduling -o wide`

Output esperado (ejemplo):
```text
scheduling-demo-no-toleration   Pending   ...
scheduling-demo-ok              Running   ...   int-lab-worker
```

Como interpretarlo:
- Diferencia clara entre bloqueo por taint y scheduling permitido por toleration.

---

## Limpieza opcional

```bash
kubectl delete namespace int-scheduling
kubectl taint nodes int-lab-worker dedicated=apps:NoSchedule-
kubectl label node int-lab-worker workload-
```
