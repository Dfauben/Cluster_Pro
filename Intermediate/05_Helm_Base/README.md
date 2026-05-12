# Intermediate 05 - Helm base

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Intermediate](../README.md)
- [Anterior](../04_Storage_Persistencia/README.md)
- [Siguiente](../../Pro/README.md)
- [Conceptos](../Conceptos/README.md)


## Objetivo

Introducir gestion de aplicaciones con Helm:
- instalar chart
- listar releases
- upgrade/rollback

## Prerrequisitos

- `helm` instalado y cluster accesible.
- Namespace de pruebas libre (usaremos `int-helm`).

---

## Crea namespace de trabajo

### `kubectl create namespace int-helm --dry-run=client -o yaml | kubectl apply -f -`

Que hace:
- Crea namespace para release Helm.

---

## Configura repositorio de charts

### `helm repo add bitnami https://charts.bitnami.com/bitnami`

Que hace:
- Agrega repositorio oficial Bitnami.

Output esperado:
```text
"bitnami" has been added to your repositories
```

---

### `helm repo update`

Que hace:
- Actualiza indice local de charts.

---

## Instala primera release

### `helm install demo-nginx bitnami/nginx -n int-helm`

Que hace:
- Instala chart como release `demo-nginx`.

Output esperado:
```text
NAME: demo-nginx
NAMESPACE: int-helm
STATUS: deployed
```

Como interpretarlo:
- Release activa y gestionada por Helm.

---

## Inspecciona release y recursos

### `helm list -n int-helm`

Que hace:
- Lista releases del namespace.

---

### `kubectl get all -n int-helm`

Que hace:
- Muestra recursos creados por la release.

---

## Aplica upgrade controlado

### `helm upgrade demo-nginx bitnami/nginx -n int-helm --set replicaCount=2`

Que hace:
- Ejecuta upgrade de release cambiando replicas.

Output esperado:
```text
Release "demo-nginx" has been upgraded.
```

---

### `kubectl get deployment -n int-helm`

Que hace:
- Verifica nuevo numero de replicas.

---

## Consulta historial y ejecuta rollback

### `helm history demo-nginx -n int-helm`

Que hace:
- Muestra revisiones de la [release](../Conceptos/helm-release.md).

---

### `helm rollback demo-nginx 1 -n int-helm`

Que hace:
- Revierte release a la revision 1.

Output esperado:
```text
Rollback was a success! Happy Helming!
```

---

## Limpieza opcional

```bash
helm uninstall demo-nginx -n int-helm
kubectl delete namespace int-helm
```
