# Beginner 03 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../04_Services_Exposicion/README.md)

## Contexto

Ahora vas a montar un workload real y ver como Kubernetes crea, conecta y escala la aplicacion sin que tengas que manejar los pods uno por uno.

## Tarea

Empiezas creando el estado deseado. Despues miras como nace el workload, lo expones con un service interno y por ultimo escalas para comprobar que la reconciliacion funciona.

```bash
kubectl create deployment hello-k8s --image=nginx:stable
```

Con esto defines la aplicacion base. Lo importante no es la linea exacta, sino que Kubernetes ha aceptado el estado deseado.

```bash
kubectl get deployment,pods -l app=hello-k8s -o wide
```

Ahora observas como aparece el workload. Al principio puedes ver `ContainerCreating`; eso no es un fallo, es parte normal del arranque.

```bash
kubectl expose deployment hello-k8s --port=80 --target-port=80 --type=ClusterIP
kubectl get svc hello-k8s
```

Aqui creas el acceso interno estable. Fijate en que el `Service` no depende de una IP de pod concreta; depende del selector y de la capa de servicio.

```bash
kubectl scale deployment hello-k8s --replicas=3
kubectl rollout status deployment/hello-k8s
kubectl get pods -l app=hello-k8s -o wide
```

En este punto Kubernetes debe converger al numero de replicas pedido. Si todo va bien, el rollout termina y ves tres pods activos.

| Paso | Qué debes observar |
|---|---|
| crear deployment | el estado deseado existe |
| mirar deployment/pods | el workload empieza a nacer |
| exponer service | aparece una entrada interna estable |
| escalar | Kubernetes crea o ajusta replicas |
| rollout status | la convergencia termina bien |

**[IMAGEN ASCII - reemplazar por imagen]**
```text
crear -> observar -> exponer -> escalar -> verificar
```

## Criterio de salida

La practica queda resuelta cuando puedes crear la app, verla nacer, exponerla internamente y dejarla en tres replicas con un rollout correcto.
## ➡️ Siguiente

Continua con [Services y exposicion basica](../04_Services_Exposicion/README.md).
