# Beginner 04 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../05_Services_Exposicion/README.md)

## Contexto

Ya sabes crear workloads de forma imperativa. Ahora vas a describir el mismo tipo de recurso en YAML para que Kubernetes lo aplique y lo mantenga.

## Tarea

Vas a crear dos archivos:
- `deployment.yaml`
- `service.yaml`

Un archivo YAML es un fichero de texto plano donde describes el estado deseado. Lo editas con `nano` o `vim`, lo guardas y despues lo aplicas con `kubectl apply -f`.

Empieza creando una carpeta de trabajo:

```bash
mkdir -p ~/k8s-beginner/despliegues-declarativos
cd ~/k8s-beginner/despliegues-declarativos
```

### 1. Crea el `Deployment`

Abre `nano deployment.yaml` o `vim deployment.yaml` y escribe esto:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-declarativo
  labels:
    app: hello-declarativo
spec:
  replicas: 2
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: hello-declarativo
  template:
    metadata:
      labels:
        app: hello-declarativo
    spec:
      containers:
        - name: app
          image: nginx:stable
          ports:
            - containerPort: 80
```

Este fichero describe el estado deseado de la aplicacion. Kubernetes usa `spec` para saber cuantas replicas quiere, que imagen debe correr y como debe recrearlas cuando cambie algo.

### 2. Crea el `Service`

Abre `nano service.yaml` o `vim service.yaml` y escribe esto:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-declarativo
  labels:
    app: hello-declarativo
spec:
  type: ClusterIP
  selector:
    app: hello-declarativo
  ports:
    - port: 80
      targetPort: 80
```

Este fichero declara la entrada estable para llegar a los pods. Las `metadata.labels` ayudan a filtrar y organizar recursos, y el `selector` une el `Service` con el `Deployment` a traves de las labels del pod.

### 3. Aplica los archivos

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get deploy,pods,svc -l app=hello-declarativo -o wide
```

Con eso declaras el workload y su acceso estable. Kubernetes crea los objetos y los reconcilia con lo que has escrito.

### 4. Cambia el estado desde el YAML

Ahora abre otra vez `deployment.yaml` y cambia:

```yaml
replicas: 2
```

por:

```yaml
replicas: 3
```

Guarda el archivo y vuelve a aplicar:

```bash
kubectl apply -f deployment.yaml
kubectl rollout status deployment/hello-declarativo
kubectl get pods -l app=hello-declarativo -o wide
```

Aqui ves la ventaja del enfoque declarativo: cambias el fichero, lo reaplicas y Kubernetes ajusta el cluster al nuevo estado.

| Paso | Qué debes observar |
|---|---|
| crear deployment.yaml | describes la app en un fichero |
| crear service.yaml | describes el acceso estable en otro fichero |
| aplicar archivos | Kubernetes crea objetos reales |
| cambiar replicas | el YAML manda sobre el estado deseado |
| rollout status | el cluster converge al nuevo valor |

## Criterio de salida

La practica queda resuelta cuando sabes describir un workload en YAML, aplicarlo y cambiarlo sin depender de comandos imperativos para cada paso.

## ➡️ Siguiente

Continua con [Services y exposicion basica](../05_Services_Exposicion/README.md).
