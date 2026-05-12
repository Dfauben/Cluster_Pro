# Control Plane

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice de conceptos](README.md)

## Que es

El `control-plane` es el cerebro del cluster. Decide y coordina lo que debe ocurrir.

## Componentes clave (desarrollados)

### `kube-apiserver` (puerta de entrada)

Que hace:
- Recibe todas las peticiones de `kubectl` y de componentes internos.
- Valida autenticacion/autorizacion y esquema de recursos.
- Expone la API REST de Kubernetes.

Por que es critico:
- Si cae, no puedes crear/actualizar recursos (aunque algunos pods ya existentes sigan corriendo un tiempo).

Como participa en el flujo:
- Todo cambio pasa por aqui antes de guardarse en `etcd`.

---

### `etcd` (fuente de verdad del estado)

Que hace:
- Guarda el estado deseado y actual del cluster en formato clave-valor.
- Persiste configuracion, objetos y metadatos.

Por que es critico:
- Si se corrompe o pierde datos, el cluster pierde su estado.
- Backup y restauracion de `etcd` son operaciones de alta importancia.

Como participa en el flujo:
- El API server lee/escribe en `etcd`.
- Los demas componentes reaccionan a cambios observando la API.

---

### `kube-scheduler` (decisor de placement)

Que hace:
- Detecta pods sin nodo asignado (`Pending` sin `nodeName`).
- Selecciona el mejor nodo segun recursos, restricciones y politicas.

Por que es critico:
- Si cae, los pods nuevos pueden quedar en `Pending`.
- Lo ya ejecutandose sigue funcionando, pero no hay scheduling nuevo.

Como participa en el flujo:
- Lee pods pendientes desde la API.
- Publica la asignacion de nodo en el objeto pod.

---

### `kube-controller-manager` (motor de reconciliacion)

Que hace:
- Ejecuta controladores que mantienen el estado real alineado con el deseado.

Controladores importantes:
- `Deployment/ReplicaSet controller`: mantiene replicas.
- `Node controller`: gestiona estado de nodos.
- `Job controller`: controla ejecucion de jobs.
- `Endpoints/EndpointSlice controllers`: mantienen backends de services.

Por que es critico:
- Sin controllers, el cluster deja de autocorregirse.
- Ejemplo: cae un pod y no se recrea automaticamente.

Como participa en el flujo:
- Observa cambios en la API.
- Aplica acciones para cerrar la brecha entre estado deseado y real.

---

### (Opcional) `cloud-controller-manager`

Nota:
- En entornos cloud gestiona integraciones con proveedor (load balancers, rutas, nodos).
- En este lab local con `kind` normalmente no es protagonista.

## Flujo completo entre componentes

1. Ejecutas `kubectl apply ...`.
2. `kube-apiserver` valida y registra el objeto en `etcd`.
3. `kube-controller-manager` crea/ajusta recursos derivados (por ejemplo ReplicaSet/Pods).
4. `kube-scheduler` asigna nodo a pods pendientes.
5. `kubelet` en el nodo arranca contenedores y reporta estado.
6. Controladores siguen reconciliando continuamente.

## Como se ve en kind

En `kind`, estos componentes suelen verse como pods en `kube-system`.

## Comandos utiles

```bash
kubectl get pods -n kube-system
kubectl get pods -n kube-system -o wide
kubectl get pods -n kube-system | rg 'kube-apiserver|etcd|kube-scheduler|kube-controller-manager'
kubectl logs -n kube-system kube-apiserver-kind-lab-k8s-control-plane
kubectl logs -n kube-system etcd-kind-lab-k8s-control-plane
kubectl logs -n kube-system kube-scheduler-kind-lab-k8s-control-plane
kubectl logs -n kube-system kube-controller-manager-kind-lab-k8s-control-plane
```

Nota:
- Algunos pods son estaticos y estan atados al nodo control-plane.
