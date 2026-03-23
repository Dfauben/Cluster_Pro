# K8s Lab - Bitacora

Fecha de inicio: 2026-02-12
Entorno: WSL2 Ubuntu 24.04.3 LTS

## Estado tecnico actual

- `kubectl`: `v1.35.0`
- `docker`: `v29.2.0` (daemon operativo)
- `kind`: `v0.23.0`
- `helm`: `v3.20.0`
- Cluster activo: `kind-lab-k8s` (Kubernetes `v1.35.0`)

## Estructura del laboratorio

- `Beginner/00_Fundamentos`
- `Beginner/01_Kubectl_Operacion`
- `Beginner/02_Workloads_Basicos`
- `Beginner/03_Debug_Operativo`
- `Intermediate`
- `Pro`

## Registro de progreso

### Base de entorno (completado)
Comandos:
```bash
uname -a
cat /etc/os-release
docker --version
kubectl version --client --output=yaml
kind version
helm version
docker info --format '{{.ServerVersion}}'
```

Resultado:
- Entorno WSL listo para laboratorio.
- Tooling de Kubernetes operativo.

### Cluster local con kind (completado)
Comandos:
```bash
kind create cluster --name lab-k8s --image kindest/node:v1.35.0
kubectl wait --for=condition=Ready node/lab-k8s-control-plane --timeout=120s
kubectl -n kube-system wait deployment/coredns --for=condition=Available --timeout=120s
kubectl version --output=yaml
```

Resultado:
- Cluster creado y estable.
- Nodo `Ready`.
- CoreDNS disponible.
- Version cliente/servidor alineadas.

### Beginner 00 - Fundamentos (comandos validados, listo para practica guiada)
Ruta: `Beginner/00_Fundamentos/README.md`

Objetivo:
- Entender cluster, node, namespace, pod, deployment y service.
- Aprender comandos de inspeccion basicos para maniobra diaria.

Comandos de inicio:
```bash
kubectl config current-context
kubectl get nodes -o wide
kubectl get namespaces
kubectl get pods -A -o wide
kubectl get svc -A
kubectl api-resources | head -n 25
kubectl explain pod
kubectl explain deployment
kubectl explain service
```

Validacion tecnica realizada:
- Contexto actual: `kind-lab-k8s`
- Nodo: `lab-k8s-control-plane` en `Ready`
- Pods de sistema en `Running` en `kube-system`
- Servicios base presentes: `kubernetes` y `kube-dns`
- README mejorado con formato por comando: que hace, output esperado e interpretacion.

Actualizacion de estructura (2026-02-12):
- Creado `Beginner/README.md` como indice principal del modulo.
- Creada biblioteca `Beginner/Conceptos/` con documentos separados para:
  - `cluster`
  - `kubectl context`
  - `node`
  - `control-plane`
  - `internal-ip`
  - `namespace`
  - `pod`
  - `deployment`
  - `service`
  - `dns interno`
- Enlaces agregados desde `Beginner/00_Fundamentos/README.md` y `README.md`.

Mejora editorial (2026-02-12):
- En `Beginner/00_Fundamentos/README.md` se elimino el bloque `Lectura de apoyo`.
- Los conceptos ahora se enlazan en la primera aparicion de cada termino dentro del contenido.
- Los titulos de seccion `Comando N` se cambiaron por titulos mas narrativos y operativos.

Ajuste adicional (2026-02-12):
- Eliminado bloque `Flujo recomendado` en `Beginner/00_Fundamentos/README.md`.
- Eliminados bloques `Mini resumen de conceptos` y `Criterios de completado`.
- Regla de enlaces ajustada: primera aparicion enlazada a partir de `Prerrequisitos`.
- Nuevos conceptos creados:
  - `Beginner/Conceptos/api-kubernetes.md`
  - `Beginner/Conceptos/replicas.md`
  - `Beginner/Conceptos/rollout.md`

Ajuste de enlaces (2026-02-12):
- Confirmado que `Prerrequisitos` no cuenta para primera aparicion enlazada.
- Relacionado `cluster` en secciones operativas de `Beginner/00_Fundamentos/README.md`.
- Reforzada relacion entre `Service` y `API de Kubernetes` en el flujo de explicacion.

### Beginner 01 - Kubectl Operacion (comandos validados, documentacion mejorada)
Ruta: `Beginner/01_Kubectl_Operacion/README.md`

Validacion tecnica realizada:
- `kubectl get all -A` muestra recursos base en estado saludable.
- `kubectl get pods -A --show-labels` muestra labels de sistema correctamente.
- `kubectl describe node lab-k8s-control-plane` refleja nodo `Ready` y recursos asignados.
- `kubectl get events -A --sort-by=.metadata.creationTimestamp` devuelve `No resources found` (normal sin eventos recientes).
- `kubectl get pods -A -o custom-columns=...` genera vista operativa limpia.

Mejoras aplicadas:
- README reescrito con formato narrativo por comando (que hace, output esperado, como interpretarlo).
- Regla de enlaces mantenida: primera aparicion enlazada despues de `Prerrequisitos`.
- Nuevos conceptos agregados para operacion diaria:
  - `labels`
  - `kubectl describe`
  - `events`
  - `custom columns`
  - `replicaset`
  - `daemonset`

### Beginner 02 - Workloads Basicos (comandos validados, documentacion mejorada)
Ruta: `Beginner/02_Workloads_Basicos/README.md`

Validacion tecnica realizada:
- `kubectl create deployment hello-k8s --image=nginx:stable` crea deployment correctamente.
- `kubectl expose deployment ... --type=ClusterIP` crea service interno estable.
- `kubectl scale deployment hello-k8s --replicas=3` ajusta replicas sin incidencia.
- `kubectl rollout status deployment/hello-k8s` confirma rollout exitoso.

Mejoras aplicadas:
- README reescrito con formato narrativo por comando.
- Explicacion operativa de fases (`ContainerCreating` -> `Running`).
- Enlaces de conceptos en primera aparicion despues de `Prerrequisitos`.
- Nuevos conceptos agregados:
  - `clusterip`
  - `selector`

### Beginner 03 - Debug Operativo (comandos validados, documentacion mejorada)
Ruta: `Beginner/03_Debug_Operativo/README.md`

Validacion tecnica realizada:
- `kubectl logs -l app=hello-k8s --tail=50 --prefix=true` muestra logs con origen por pod.
- `kubectl describe pod -l app=hello-k8s` muestra condiciones y eventos de arranque.
- `kubectl get events --sort-by=.metadata.creationTimestamp` valida cronologia de eventos.
- `kubectl rollout history`, `rollout restart` y `rollout status` operan correctamente.

Mejoras aplicadas:
- README reescrito con formato narrativo por comando.
- Flujo de troubleshooting ordenado: evidencia -> diagnostico -> cronologia -> recuperacion.
- Nuevo concepto agregado:
  - `kubectl logs`

Nota de ejecucion:
- Las validaciones de `Beginner 02/03` se hicieron en namespace temporal `beginner-lab`.
- El namespace temporal fue eliminado al finalizar para no dejar residuos en el cluster.

### Preparacion de Intermediate (estructura inicial completada)
Ruta: `Intermediate/README.md`

Decision de diseño:
- El tema de creacion de cluster y nodos se ubica en `Intermediate/00_Cluster_y_Nodos`.
- Motivo: separar uso basico de Kubernetes (Beginner) de operacion de infraestructura (Intermediate).

Estructura creada:
- `Intermediate/00_Cluster_y_Nodos/README.md`
- `Intermediate/01_Probes_Salud/README.md`
- `Intermediate/02_Recursos_y_Scheduling/README.md`
- `Intermediate/03_Networking_e_Ingress/README.md`
- `Intermediate/04_Storage_Persistencia/README.md`
- `Intermediate/05_Helm_Base/README.md`
- `Intermediate/kind-configs/multi-node.yaml`

Resultado:
- Ruta Intermediate preparada para continuar despues de Beginner.
- Base multinodo lista para practicas reales de nodos (`cordon`, `drain`, `uncordon`).

### Mejora de conceptos Beginner (control-plane)
Ruta: `Beginner/Conceptos/control-plane.md`

Cambios aplicados:
- Desarrollo detallado de componentes:
  - `kube-apiserver`
  - `etcd`
  - `kube-scheduler`
  - `kube-controller-manager`
- Explicacion de rol, impacto operativo si falla y participacion en el flujo.
- Seccion adicional de flujo completo de control-plane de extremo a extremo.
- Comandos de observacion ampliados por componente (logs especificos en `kube-system`).

### Desarrollo de Intermediate al estilo Beginner (completado)
Ruta: `Intermediate/README.md`

Cambios aplicados:
- Reescritos todos los READMEs de Intermediate con formato narrativo por comando:
  - objetivo
  - prerrequisitos
  - secciones operativas
  - output esperado
  - interpretacion
  - limpieza opcional
- Modulos actualizados:
  - `Intermediate/00_Cluster_y_Nodos/README.md`
  - `Intermediate/01_Probes_Salud/README.md`
  - `Intermediate/02_Recursos_y_Scheduling/README.md`
  - `Intermediate/03_Networking_e_Ingress/README.md`
  - `Intermediate/04_Storage_Persistencia/README.md`
  - `Intermediate/05_Helm_Base/README.md`
- Creada biblioteca de conceptos para Intermediate:
  - `Intermediate/Conceptos/README.md`
  - `Intermediate/Conceptos/cordon-drain-uncordon.md`
  - `Intermediate/Conceptos/probes.md`
  - `Intermediate/Conceptos/requests-limits.md`
  - `Intermediate/Conceptos/nodeselector.md`
  - `Intermediate/Conceptos/taints-tolerations.md`
  - `Intermediate/Conceptos/ingress.md`
  - `Intermediate/Conceptos/pv-pvc-storageclass.md`
  - `Intermediate/Conceptos/helm-release.md`

Resultado:
- `Intermediate` ahora mantiene la misma experiencia de lectura y ejecucion que `Beginner`.
- Navegacion actualizada desde `README.md` con acceso rapido a conceptos de Intermediate.

### Rework Beginner 00 (prerrequisitos guiados)
Ruta: `Beginner/00_Fundamentos/README.md`

Cambios aplicados:
- Seccion de prerrequisitos expandida (no solo checklist).
- Guia paso a paso añadida:
  - validacion WSL/distro
  - validacion Docker
  - instalacion/verificacion de `kubectl`
  - instalacion/verificacion de `kind`
  - creacion del cluster `kind-lab-k8s`
  - bloque de confirmacion final antes del modulo

Resultado:
- `Beginner 00` ahora incluye onboarding completo para preparar entorno desde cero.

Ajuste de estilo (Beginner 00):
- Guia de prerrequisitos simplificada para que sea mas paso a paso y menos tecnica/especifica.
- Menos detalle de instalacion avanzada y mas foco en verificacion + accion rapida.

Regla global de entorno (confirmada):
- Todo el laboratorio se ejecuta desde WSL.
- Incluye comandos de Docker ejecutados tambien desde WSL.
- Reflejado en `README.md`, `Beginner/00_Fundamentos/README.md` e `Intermediate/README.md`.
- Eliminada referencia explicita a Docker Desktop en `Beginner/00_Fundamentos/README.md`.

Actualizacion Beginner 00:
- La guia de prerrequisitos ahora incluye instalacion rapida de `docker`, `kubectl` y `kind` si no estan presentes.
- Se añade como paso inicial obligatorio: `sudo apt update && sudo apt upgrade -y`.
- Se elimina repeticion de `apt update` en pasos posteriores de instalacion.
- Ajustada instalacion de Docker para evitar conflicto `docker.io` vs `containerd.io` cuando ya existe `docker-ce`.

Rework de `Beginner/README.md`:
- Titulo principal renovado con tono mas ameno.
- Nueva estructura por bloques:
  - descripcion general
  - orientacion y dificultad
  - nivel esperado al finalizar con ejemplos
- Tabla de submodulos creada con 3 columnas:
  - nombre submodulo
  - descripcion breve
  - check (`[ ]`) para seguimiento.

Ajuste de redaccion en `Beginner/README.md`:
- Eliminados titulos tipo "Bloque x".
- Titulos de seccion simplificados y mas naturales.
- Nombres visibles de submodulos normalizados a lenguaje natural (manteniendo enlaces originales).
- Columna `Check` actualizada a sintaxis checklist Markdown (`- [ ]`).

Estandar visual acordado:
- Imagen principal en README de modulo: `1280 x 640 px`.
- Imagen en README de submodulos: `1280 x 160 px`.
- Convencion reflejada en `README.md` y `Beginner/README.md`.

Rework visual de contenido en `Beginner/README.md`:
- Eliminada tabla de submodulos.
- Reemplazada por bloques individuales separados por imagenes (`1280 x 160 px`) al estilo SRI.
- Cada bloque contiene:
  - banner clicable al submodulo
  - titulo natural
  - descripcion breve
  - checklist `- [ ] Completado`
- Añadido `Beginner/img/README.md` con nombres de archivos esperados.

Refinado de seccion "Nivel esperado" en `Beginner/README.md`:
- Eliminados los ejemplos inline.
- Titulo simplificado a `Nivel esperado al completar Beginner`.

Ajuste final en `Beginner/README.md`:
- Eliminado tambien el encabezado de la seccion de nivel esperado.
- Se mantiene solo el texto con capacidades objetivo al finalizar Beginner.

Mejora de navegacion en `Beginner/README.md`:
- Añadido `Indice de submodulos` con enlaces directos a:
  - `00_Fundamentos`
  - `01_Kubectl_Operacion`
  - `02_Workloads_Basicos`
  - `03_Debug_Operativo`

Rework de indice en `Beginner/README.md`:
- `Indice de submodulos` sustituido por `Indice` jerarquico.
- Formato aplicado: `modulo -> submodulos`.
- Añadidos accesos a `Inicio`, `Modulo Intermediate` y `Modulo Pro`.

Ajuste de estructura en `Beginner/README.md`:
- La seccion `Indice` se movio para quedar inmediatamente despues del titulo principal.

Estandar de indice aplicado en submodulos Beginner:
- Actualizados:
  - `Beginner/00_Fundamentos/README.md`
  - `Beginner/01_Kubectl_Operacion/README.md`
  - `Beginner/02_Workloads_Basicos/README.md`
  - `Beginner/03_Debug_Operativo/README.md`
- Formato comun:
  - enlace al `Modulo Beginner`
  - lista anidada con todos los submodulos del modulo

Placeholder temporal de banners:
- En `Beginner/README.md`, los 4 banners de submodulo ahora apuntan a `../rsc/img/banner_template.png`.
