# Intermediate 03 - Networking e Ingress

## Objetivo

Cubrir exposicion y enrutamiento:
- Services avanzados
- Ingress
- reglas host/path

## Prerrequisitos

- Cluster activo.
- Namespace de pruebas libre (usaremos `int-net`).

---

## Crea namespace de trabajo

### `kubectl create namespace int-net --dry-run=client -o yaml | kubectl apply -f -`

Que hace:
- Crea namespace para pruebas de red.

---

## Despliega app backend y service

### `kubectl create deployment hello-net --image=nginx:stable -n int-net`

Que hace:
- Crea backend de prueba.

Output esperado:
```text
deployment.apps/hello-net created
```

---

### `kubectl expose deployment hello-net -n int-net --port=80 --target-port=80 --type=ClusterIP`

Que hace:
- Crea service interno para el backend.

Output esperado:
```text
service/hello-net exposed
```

---

## Instala Ingress Controller (si no existe)

### `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml`

Que hace:
- Instala ingress-nginx para kind.

Output esperado:
- Multiples recursos creados en `ingress-nginx`.

---

### `kubectl wait --namespace ingress-nginx --for=condition=ready pod --selector=app.kubernetes.io/component=controller --timeout=180s`

Que hace:
- Espera a que el controller este operativo.

Output esperado:
```text
pod/... condition met
```

---

## Crea regla Ingress para host local

### `cat <<'EOF' | kubectl apply -n int-net -f -`

Comando completo:
```bash
cat <<'EOF' | kubectl apply -n int-net -f -
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: hello-net-ingress
spec:
  ingressClassName: nginx
  rules:
  - host: hello.int.local
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: hello-net
            port:
              number: 80
EOF
```

Que hace:
- Define [Ingress](../Conceptos/ingress.md) host-based hacia el service.

Output esperado:
```text
ingress.networking.k8s.io/hello-net-ingress created
```

---

## Valida enrutamiento

### `kubectl get ingress -n int-net`

Output esperado:
- Recurso ingress visible con host `hello.int.local`.

---

### `kubectl describe ingress hello-net-ingress -n int-net`

Que hace:
- Muestra reglas y backend asociado.

---

### `kubectl -n ingress-nginx port-forward service/ingress-nginx-controller 8080:80`

Que hace:
- Abre puerto local para prueba HTTP.

En otra terminal:
```bash
curl -H "Host: hello.int.local" http://127.0.0.1:8080
```

Como interpretarlo:
- Si responde HTML de nginx, el flujo funciona: cliente -> ingress -> service -> pod.

---

## Limpieza opcional

```bash
kubectl delete namespace int-net
```
