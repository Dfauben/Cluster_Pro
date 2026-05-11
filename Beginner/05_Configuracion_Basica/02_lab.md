# Beginner 05 - Practica guiada

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Inicio de Beginner](../README.md)
- [Indice del modulo](README.md)
- [Anterior](01_teoria.md)
- [Siguiente](03_scenario.md)

## Contexto

Ahora vas a separar configuracion del contenedor para que veas como una app puede cambiar sin tocar la imagen.

## Tarea

Primero creas un `ConfigMap`, luego un `Secret` y despues los consumes desde un pod sencillo.

```bash
kubectl create configmap hello-config --from-literal=APP_MODE=lab --from-literal=APP_NAME=hello-k8s
kubectl create secret generic hello-secret --from-literal=APP_TOKEN=secret123
```

Con esto ya tienes la configuracion separada del workload.

```bash
kubectl get configmap hello-config -o yaml
kubectl get secret hello-secret -o yaml
```

Aqui no necesitas memorizar el contenido del secret; basta con reconocer que Kubernetes lo guarda de forma distinta.

```bash
kubectl run config-check --image=busybox:1.36 --restart=Never --env-from=configmap/hello-config --command -- sh -c 'env | sort | grep -E "APP_"'
kubectl logs config-check
```

La idea es comprobar que la configuracion llega al contenedor sin editar la imagen.

| Paso | Qué debes observar |
|---|---|
| crear configmap | aparecen valores no sensibles |
| crear secret | aparece un objeto separado |
| leer yaml | ves que Kubernetes los trata distinto |
| ejecutar pod de prueba | la config entra al runtime |

**[IMAGEN ASCII - reemplazar por imagen]**
```text
config -> pod -> comportamiento
```

## Criterio de salida

La practica queda resuelta cuando sabes crear configuracion separada, verla en Kubernetes y comprobar que el pod la consume sin rehacer la imagen.

