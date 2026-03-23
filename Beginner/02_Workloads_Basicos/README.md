# Beginner 02 - Workloads basicos

## Indice

- [Modulo Beginner](../README.md)
    - [Submodulo 00 - Fundamentos del cluster](../00_Fundamentos/README.md)
    - [Submodulo 01 - Operacion diaria con kubectl](../01_Kubectl_Operacion/README.md)
    - [Submodulo 02 - Primeros deployments y servicios](../02_Workloads_Basicos/README.md)
    - [Submodulo 03 - Debug operativo inicial](../03_Debug_Operativo/README.md)

## Objetivo

Crear y maniobrar una aplicacion simple:
- crear deployment
- escalar replicas
- exponer servicio interno

## Prerrequisitos

- Cluster `kind-lab-k8s` activo.
- Modulos `Beginner/00_Fundamentos` y `Beginner/01_Kubectl_Operacion` revisados.

---

## Nace tu primera app en Kubernetes

### `kubectl create deployment hello-k8s --image=nginx:stable`

Que hace:
- Crea un [deployment](../Conceptos/deployment.md) llamado `hello-k8s` usando la imagen `nginx:stable`.

Output esperado:
```text
deployment.apps/hello-k8s created
```

Como interpretarlo:
- Kubernetes ya recibio el estado deseado.
- A partir de aqui, el deployment intentara mantener pods en ejecucion.

---

## Verifica que los pods esten aterrizando

### `kubectl get deployment,pods -l app=hello-k8s -o wide`

Que hace:
- Lista el deployment y sus [pods](../Conceptos/pod.md), filtrando por [labels](../Conceptos/labels.md).

Output esperado (ejemplo resumido):
```text
NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-k8s   0/1     1            0           0s

NAME                             READY   STATUS              NODE
pod/hello-k8s-74cc7cbf59-29zhb   0/1     ContainerCreating   lab-k8s-control-plane
```

Como interpretarlo:
- Es normal que al inicio veas `ContainerCreating`.
- Luego debe pasar a `Running` y el deployment a `AVAILABLE`.

---

## Expone la app dentro del cluster

### `kubectl expose deployment hello-k8s --port=80 --target-port=80 --type=ClusterIP`

Que hace:
- Crea un [service](../Conceptos/service.md) de tipo [ClusterIP](../Conceptos/clusterip.md) para acceder a los pods del deployment.

Output esperado:
```text
service/hello-k8s exposed
```

Como interpretarlo:
- Ya tienes un endpoint estable para tu app dentro del cluster.
- El service usa un [selector](../Conceptos/selector.md) para enrutar trafico a los pods correctos.

---

## Comprueba el endpoint estable

### `kubectl get svc hello-k8s`

Que hace:
- Muestra los datos del service creado.

Output esperado (ejemplo):
```text
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)
hello-k8s   ClusterIP   10.96.248.148   <none>        80/TCP
```

Como interpretarlo:
- `CLUSTER-IP` es la IP virtual interna del service.
- Esa IP permanece estable aunque los pods cambien.

---

## Escala de 1 a 3 replicas

### `kubectl scale deployment hello-k8s --replicas=3`

Que hace:
- Ajusta el deployment para mantener 3 [replicas](../Conceptos/replicas.md).

Output esperado:
```text
deployment.apps/hello-k8s scaled
```

Como interpretarlo:
- Kubernetes creara pods adicionales hasta llegar al numero deseado.

---

## Confirma que el cambio termino bien

### `kubectl rollout status deployment/hello-k8s`

Que hace:
- Muestra el progreso del [rollout](../Conceptos/rollout.md) del deployment.

Output esperado (ejemplo):
```text
deployment "hello-k8s" successfully rolled out
```

Como interpretarlo:
- El estado deseado se aplico correctamente.
- Si tarda, veras mensajes intermedios de progreso.

---

## Foto final del workload

### `kubectl get pods -l app=hello-k8s -o wide`

Que hace:
- Lista los pods finales de la app ya escalada.

Output esperado (ejemplo resumido):
```text
NAME                         READY   STATUS    RESTARTS   IP           NODE
hello-k8s-74cc7cbf59-29zhb   1/1     Running   0          10.244.0.5   lab-k8s-control-plane
hello-k8s-74cc7cbf59-m282z   1/1     Running   0          10.244.0.7   lab-k8s-control-plane
hello-k8s-74cc7cbf59-vw8cv   1/1     Running   0          10.244.0.6   lab-k8s-control-plane
```

Como interpretarlo:
- Debes ver 3 pods en `Running`.
- La app ya esta operativa internamente con balanceo via service.
