# Beginner 06 - Practica guiada

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](01_teoria.md)
- [➡️ Siguiente](../07_Debug_Operativo/README.md)

## Contexto

Ya sabes que un pod no es un buen sitio para guardar datos importantes. Ahora vas a pedir almacenamiento persistente y montar un volumen en una app simple.

## Tarea

Primero creas una `PVC`, luego la asocias a un pod y por ultimo compruebas que el volumen esta disponible.

```bash
kubectl get storageclass
```

Antes de pedir volumen, mira que clase de almacenamiento tienes disponible. En kind suele aparecer `local-path`.

```bash
cat <<'EOF' | kubectl apply -f -
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: hello-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
EOF
```

```bash
kubectl get pvc hello-pvc
```

Aqui compruebas que la solicitud existe y que Kubernetes la enlaza con el volumen correcto.

```bash
cat <<'EOF' | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: hello-storage
spec:
  containers:
    - name: app
      image: busybox:1.36
      command: ["sh", "-c", "echo hola > /data/msg && sleep 3600"]
      volumeMounts:
        - name: data
          mountPath: /data
  volumes:
    - name: data
      persistentVolumeClaim:
        claimName: hello-pvc
  restartPolicy: Never
EOF
```

```bash
kubectl get pod hello-storage -o wide
kubectl exec hello-storage -- cat /data/msg
```

Si todo va bien, el pod monta el volumen y puedes leer el dato que has escrito.

| Paso | Qué debes observar |
|---|---|
| ver storageclass | sabes qué aprovisionamiento hay |
| crear pvc | aparece la solicitud de volumen |
| crear pod | el pod monta el volumen |
| leer dato | el contenido persiste dentro del volumen |


<br>

**[IMAGEN ASCII - reemplazar por imagen]**
```text
pvc -> volumen -> pod -> dato
```

## Criterio de salida

La practica queda resuelta cuando sabes pedir almacenamiento, montarlo en un pod y comprobar que el dato vive en el volumen y no solo en la ejecucion del contenedor.
<br>
## ➡️ Siguiente

Continua con [Debug operativo inicial](../07_Debug_Operativo/README.md).
