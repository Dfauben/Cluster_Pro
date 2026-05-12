# Beginner 01 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../02_Kubectl_Operacion/README.md)

## Proposito

Leer el cluster como una fotografia operativa y entender cada capa sin perderte.

## Antes de empezar

Asume que el cluster `kind-lab-k8s` ya existe y esta sano.

La idea aqui es simple: primero confirmas que hablas con el cluster correcto, luego miras la infraestructura, despues separas el sistema del espacio de usuario y por ultimo consultas la API cuando necesites leer mejor un recurso.

## Primero confirma el contexto

```bash
kubectl config current-context
```

Lo que deberias ver es el contexto del lab. Si no coincide, paras aqui porque todo lo demas estaria contaminado.

## Luego mira la capa de infraestructura

```bash
kubectl get nodes -o wide
```

Aqui no te interesa solo que exista un nodo. Fijate en:
- nombre del nodo
- estado `Ready`
- rol del control-plane

Si el control-plane aparece sano, ya tienes la base del cluster.

## Despues separa el cluster por namespaces

```bash
kubectl get namespaces
```

Reconoce lo basico en la salida:
- `default` para pruebas simples
- `kube-system` para componentes internos
- `kube-public` para informacion publica
- `kube-node-lease` para estado de nodos
- `local-path-storage` para storage local en kind

Cuando entiendas eso, la salida deja de ser una lista y pasa a ser una division funcional del cluster.

## Ahora mira lo que corre dentro de `kube-system`

```bash
kubectl get pods -n kube-system -o wide
```

Busca estos nombres y asocialos con su funcion:
- `coredns`
- `etcd`
- `kube-apiserver`
- `kube-controller-manager`
- `kube-scheduler`
- `kube-proxy`
- `kindnet`

Si alguno falta o no esta `Running`, ya tienes una pista de que la plataforma interna no esta completa.

## Revisa los servicios base

```bash
kubectl get svc -A
```

Aqui solo necesitas reconocer que hay servicios estables y que algunos pertenecen al sistema. No busques todavia una app de usuario; busca la capa de acceso estable del cluster.

## Por ultimo, explora la API

```bash
kubectl api-resources | head -n 25
kubectl explain pod
kubectl explain deployment
kubectl explain service
```

Qué debes fijarte:
- si el recurso vive dentro de un namespace o no
- si es de computo, red, config o almacenamiento
- si `explain` te enseña la forma del objeto para escribir YAML sin adivinar

**[IMAGEN ASCII - reemplazar por imagen]**
```text
cluster
├── contexto
├── nodes
├── namespaces
├── pods
├── services
└── API
```

## Lectura rapida por familias

### Computo y ciclo de vida

| Recurso | Idea rapida |
|---|---|
| `pods` | Lo que corre de verdad |
| `nodes` | Donde puede correr trabajo |
| `deployments` | Mantiene replicas y cambios |
| `replicasets` | Sostiene el numero de pods pedido |


<br>

### Red y acceso

| Recurso | Idea rapida |
|---|---|
| `services` | Acceso estable a pods |
| `endpoints` / `endpointslices` | IPs reales detras del service |
| `ingresses` | Entrada HTTP/HTTPS hacia services |
| `networkpolicies` | Reglas de trafico entre pods |


<br>

### Configuracion y seguridad

| Recurso | Idea rapida |
|---|---|
| `configmaps` | Configuracion no sensible |
| `secrets` | Datos sensibles |
| `serviceaccounts` | Identidad del pod en la API |


<br>

### Estado y observabilidad

| Recurso | Idea rapida |
|---|---|
| `events` | Pistas de lo que ha pasado |
| `leases` | Estado temporal de coordinacion |


<br>

### Almacenamiento

| Recurso | Idea rapida |
|---|---|
| `persistentvolumes` | Volumenes disponibles |
| `persistentvolumeclaims` | Peticiones de almacenamiento |
| `storageclasses` | Como se aprovisiona el storage |


<br>

### Extensibilidad

| Recurso | Idea rapida |
|---|---|
| `customresourcedefinitions` | Nuevos tipos de recurso |
| `apiservices` | APIs agregadas al cluster |


<br>

No hace falta memorizar toda la lista de `api-resources`.
Si sabes agruparla por familia, ya puedes leer el cluster con orden.

## Lo que debes quedarte

- si el contexto es correcto, hablas con el cluster esperado
- si el nodo esta `Ready`, el cluster base esta operativo
- si `kube-system` existe y sus pods estan vivos, la plataforma interna responde
- si `explain` funciona, puedes consultar la forma de cualquier recurso sin depender de memoria

## Verificacion rapida

- el contexto coincide con el cluster del lab
- ves `kube-system` y `default`
- identificas componentes del control-plane
- reconoces la familia de los recursos mas comunes
<br>
## ➡️ Siguiente

Continua con [Primeros comandos con kubectl](../02_Kubectl_Operacion/README.md).
