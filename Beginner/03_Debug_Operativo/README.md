# Beginner 03 - Debug operativo base

## Indice

- [Modulo Beginner](../README.md)
    - [Submodulo 00 - Fundamentos del cluster](../00_Fundamentos/README.md)
    - [Submodulo 01 - Operacion diaria con kubectl](../01_Kubectl_Operacion/README.md)
    - [Submodulo 02 - Primeros deployments y servicios](../02_Workloads_Basicos/README.md)
    - [Submodulo 03 - Debug operativo inicial](../03_Debug_Operativo/README.md)

## Objetivo

Aprender troubleshooting minimo para operacion diaria.

## Prerrequisitos

- Haber completado `Beginner/02_Workloads_Basicos` (deployment `hello-k8s` existente).
- Cluster `kind-lab-k8s` activo.

---

## Primera evidencia: logs de la app

### `kubectl logs -l app=hello-k8s --tail=50 --prefix=true`

Que hace:
- Obtiene logs de los pods seleccionados por label, mostrando prefijo de origen.
- Usa [kubectl logs](../Conceptos/kubectl-logs.md) para inspeccion rapida.

Output esperado (ejemplo):
```text
[pod/hello-k8s-74cc7cbf59-29zhb/nginx] 2026/02/16 ... start worker process ...
[pod/hello-k8s-74cc7cbf59-m282z/nginx] 2026/02/16 ... start worker process ...
```

Como interpretarlo:
- Si hay lineas de arranque sin errores, los contenedores estan iniciando bien.
- El prefijo te ayuda a saber que pod emitio cada linea.

---

## Inspeccion profunda de pods

### `kubectl describe pod -l app=hello-k8s`

Que hace:
- Muestra detalle completo de pods: estado, imagen, condiciones y eventos.
- Es la herramienta principal de diagnostico con [kubectl describe](../Conceptos/kubectl-describe.md).

Output esperado (ejemplo resumido):
```text
Name:             hello-k8s-...
Status:           Running
Controlled By:    ReplicaSet/hello-k8s-...
Containers:
  nginx:
    Image:        nginx:stable
    Ready:        True
Events:
  Type    Reason     Message
  Normal  Started    Container started
```

Como interpretarlo:
- `Ready: True` y eventos `Normal` indican arranque correcto.
- Si falla, aqui veras motivos concretos (`ImagePullBackOff`, `CrashLoopBackOff`, etc.).

---

## Cronologia de lo ocurrido

### `kubectl get events --sort-by=.metadata.creationTimestamp`

Que hace:
- Lista [events](../Conceptos/events.md) del namespace actual en orden cronologico.

Output esperado:
```text
No resources found
```
o bien:
```text
LAST SEEN   TYPE     REASON              OBJECT
...         Normal   Scheduled           pod/hello-k8s-...
...         Normal   Pulled              pod/hello-k8s-...
```

Como interpretarlo:
- `No resources found` puede ser normal si no hubo eventos recientes.
- Si hay `Warning`, prioriza revisar esos primero.

---

## Historial de cambios del deployment

### `kubectl rollout history deployment/hello-k8s`

Que hace:
- Muestra historial de revisiones de rollout del deployment.

Output esperado (ejemplo):
```text
deployment.apps/hello-k8s
REVISION  CHANGE-CAUSE
1         <none>
```

Como interpretarlo:
- Cada revision representa un estado aplicado.
- Es la base para rollback cuando haga falta.

---

## Reinicio controlado sin borrar manualmente pods

### `kubectl rollout restart deployment/hello-k8s`

Que hace:
- Fuerza un nuevo [rollout](../Conceptos/rollout.md), recreando pods de forma controlada.

Output esperado:
```text
deployment.apps/hello-k8s restarted
```

Como interpretarlo:
- Kubernetes inicia pods nuevos y retira los antiguos gradualmente.
- Sirve para refrescar la app tras cambios de config o problemas transitorios.

---

## Verificacion final del reinicio

### `kubectl rollout status deployment/hello-k8s`

Que hace:
- Sigue el avance del rollout hasta completarse.

Output esperado (ejemplo):
```text
deployment "hello-k8s" successfully rolled out
```

Como interpretarlo:
- Si termina en `successfully rolled out`, la app se recupero correctamente tras el reinicio.
