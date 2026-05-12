# Intermediate 04 - Persistencia (PV/PVC)

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Intermediate](../README.md)
- [Anterior](../03_Networking_e_Ingress/README.md)
- [Siguiente](../05_Helm_Base/README.md)
- [Conceptos](../Conceptos/README.md)


## Objetivo

Trabajar persistencia de datos:
- `PersistentVolume`
- `PersistentVolumeClaim`
- `StorageClass`

## Prerrequisitos

- Cluster activo con storage class por defecto (en kind suele ser `standard`).
- Namespace de pruebas libre (usaremos `int-storage`).

---

## Crea namespace de trabajo

### `kubectl create namespace int-storage --dry-run=client -o yaml | kubectl apply -f -`

Que hace:
- Crea namespace para pruebas de persistencia.

---

## Verifica storage classes disponibles

### `kubectl get storageclass`

Que hace:
- Muestra clases de almacenamiento y default.

Output esperado (ejemplo):
```text
NAME                 PROVISIONER
standard (default)   rancher.io/local-path
```

Como interpretarlo:
- Debe existir al menos una `StorageClass` utilizable.

---

## Crea PVC y deployment que monta volumen

### `cat <<'EOF' | kubectl apply -n int-storage -f -`

Comando completo:
```bash
cat <<'EOF' | kubectl apply -n int-storage -f -
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: data-demo-pvc
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: data-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: data-demo
  template:
    metadata:
      labels:
        app: data-demo
    spec:
      containers:
      - name: app
        image: nginx:stable
        volumeMounts:
        - name: data
          mountPath: /data
      volumes:
      - name: data
        persistentVolumeClaim:
          claimName: data-demo-pvc
EOF
```

Que hace:
- Crea [PVC](../Conceptos/pv-pvc-storageclass.md) y app que monta ese volumen en `/data`.

Output esperado:
- `persistentvolumeclaim/data-demo-pvc created`
- `deployment.apps/data-demo created`

---

## Verifica binding y estado

### `kubectl get pvc,pv -n int-storage`

Output esperado (ejemplo):
```text
PVC ... STATUS Bound
PV  ... STATUS Bound
```

Como interpretarlo:
- `Bound` confirma asignacion correcta `PVC -> PV`.

---

### `kubectl rollout status deployment/data-demo -n int-storage`

Que hace:
- Espera a que el pod este disponible.

---

## Escribe y valida datos persistentes

### `POD=$(kubectl get pod -n int-storage -l app=data-demo -o jsonpath='{.items[0].metadata.name}')`

### `kubectl exec -n int-storage "$POD" -- sh -c "echo 'persistencia-ok' > /data/test.txt && cat /data/test.txt"`

Que hace:
- Escribe archivo en volumen persistente y lo lee.

Output esperado:
```text
persistencia-ok
```

---

## Simula recreacion de pod y comprueba persistencia

### `kubectl delete pod -n int-storage "$POD"`

### `kubectl rollout status deployment/data-demo -n int-storage`

### `POD_NEW=$(kubectl get pod -n int-storage -l app=data-demo -o jsonpath='{.items[0].metadata.name}')`

### `kubectl exec -n int-storage "$POD_NEW" -- cat /data/test.txt`

Como interpretarlo:
- Si devuelve `persistencia-ok`, los datos sobreviven al reemplazo del pod.

---

## Limpieza opcional

```bash
kubectl delete namespace int-storage
```
