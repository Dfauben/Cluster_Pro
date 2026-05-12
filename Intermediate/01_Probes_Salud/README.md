# Intermediate 01 - Probes de salud

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Intermediate](../README.md)
- [Anterior](../00_Cluster_y_Nodos/README.md)
- [Siguiente](../02_Recursos_y_Scheduling/README.md)
- [Conceptos](../Conceptos/README.md)


## Objetivo

Configurar y validar:
- `livenessProbe`
- `readinessProbe`
- `startupProbe`

## Prerrequisitos

- Cluster activo.
- Namespace de pruebas libre (usaremos `int-probes`).

---

## Crea namespace de trabajo

### `kubectl create namespace int-probes --dry-run=client -o yaml | kubectl apply -f -`

Que hace:
- Crea namespace idempotente para este lab.

Output esperado:
```text
namespace/int-probes created
```
o
```text
namespace/int-probes configured
```

Como interpretarlo:
- Ya tienes entorno aislado para pruebas de salud.

---

## Despliega app con probes

### `cat <<'EOF' | kubectl apply -n int-probes -f -`

Que hace:
- Aplica un deployment con `startupProbe`, `livenessProbe` y `readinessProbe`.

Comando completo:
```bash
cat <<'EOF' | kubectl apply -n int-probes -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: probe-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: probe-demo
  template:
    metadata:
      labels:
        app: probe-demo
    spec:
      containers:
      - name: app
        image: nginx:stable
        ports:
        - containerPort: 80
        startupProbe:
          httpGet:
            path: /
            port: 80
          periodSeconds: 5
          failureThreshold: 12
        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 2
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 10
          periodSeconds: 10
EOF
```

Output esperado:
```text
deployment.apps/probe-demo created
```

Como interpretarlo:
- Kubernetes comenzara a chequear salud y disponibilidad del contenedor.

---

## Observa transicion de estado

### `kubectl get pods -n int-probes -w`

Que hace:
- Muestra en vivo estado del pod mientras arrancan probes.

Output esperado (ejemplo):
```text
probe-demo-...   0/1   Running
probe-demo-...   1/1   Running
```

Como interpretarlo:
- `0/1` a `1/1` indica que readiness termino satisfactoriamente.

---

## Inspecciona eventos y probes en detalle

### `kubectl describe pod -n int-probes -l app=probe-demo`

Que hace:
- Muestra estado de probes y eventos asociados.

Output esperado (ejemplo resumido):
```text
Liveness:   http-get http://:80/
Readiness:  http-get http://:80/
Startup:    http-get http://:80/
Events:
  Normal  Started  ...
```

Como interpretarlo:
- Si una probe falla, aqui aparece motivo y frecuencia.

---

## Revisa cronologia de eventos

### `kubectl get events -n int-probes --sort-by=.metadata.creationTimestamp`

Que hace:
- Lista [events](../Conceptos/probes.md) del namespace en orden temporal.

Output esperado:
- Eventos `Normal` de scheduled, pull, create, start.

Como interpretarlo:
- Te ayuda a ordenar causa/efecto en incidentes de arranque.

---

## Limpieza opcional

```bash
kubectl delete namespace int-probes
```
