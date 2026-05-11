# Setup Windows 10/11 - Desde cero hasta WSL listo para el lab

## Navegacion

- [Inicio del repositorio](../../README.md)
- [Setup - Entorno base](../README.md)
- [Beginner 00 - Prerrequisitos](../../Beginner/00_Prerrequisitos/README.md)


Este documento parte de una maquina Windows 10/11 que todavia no tiene WSL.
La meta es dejar preparado el host para trabajar con Kubernetes desde WSL sin mezclar herramientas en distintos entornos.

## Objetivo

Al terminar esta guia deberias tener:

- WSL2 instalado
- Ubuntu listo para usar
- Docker Desktop configurado con backend WSL 2
- `kubectl`, `kind` y `helm` instalados en WSL
- una base limpia para continuar con el laboratorio

## Principios del setup

- Windows sirve para instalar y administrar.
- WSL es el entorno de trabajo real del lab.
- El repositorio debe vivir dentro del filesystem de Linux, no en `/mnt/c`, cuando empieces a trabajar en serio.

## Requisitos previos

- Windows 10 version 2004 o superior, o Windows 11
- permisos de administrador en Windows
- acceso a internet
- virtualizacion activada en BIOS/UEFI

## Paso 0 - Confirmar que puedes usar WSL

Abre PowerShell como administrador y ejecuta:

```powershell
wsl --status
```

Si el comando no existe o falla, no pasa nada: en el siguiente paso se instala WSL.

## Paso 1 - Instalar WSL

Desde PowerShell como administrador:

```powershell
wsl --install
```

Luego:

1. Reinicia el equipo cuando Windows lo pida.
2. Abre de nuevo PowerShell.
3. Verifica el estado de las distros:

```powershell
wsl -l -v
```

4. Asegura WSL2 como version por defecto:

```powershell
wsl --set-default-version 2
```

Referencia oficial:

- [Instalar WSL en Windows](https://learn.microsoft.com/en-us/windows/wsl/install)

## Paso 2 - Abrir Ubuntu y preparar la distro

Lanza Ubuntu desde el menu de inicio y completa la creacion del usuario Linux.

Dentro de Ubuntu, actualiza la base:

```bash
sudo apt update
sudo apt upgrade -y
```

Comprueba que estas dentro de WSL:

```bash
uname -a
cat /etc/os-release
```

## Paso 3 - Instalar Docker Desktop

Instala Docker Desktop para Windows desde la pagina oficial y deja activo el backend WSL 2.

Puntos de configuracion:

1. Instala Docker Desktop para Windows.
2. Abre Docker Desktop.
3. Ve a `Settings > General`.
4. Activa `Use WSL 2 based engine`.
5. Ve a `Settings > Resources > WSL Integration`.
6. Habilita la integracion con tu Ubuntu.
7. Aplica cambios y reinicia Docker Desktop si hace falta.

Verificacion desde WSL:

```bash
docker version
docker info
```

Si quieres una prueba rapida:

```bash
docker run --rm hello-world
```

Referencias oficiales:

- [Docker Desktop en Windows](https://docs.docker.com/desktop/setup/install/windows-install/)
- [Backend WSL 2 de Docker Desktop](https://docs.docker.com/desktop/features/wsl/)

## Paso 4 - Instalar `kubectl` en WSL

Usa la documentacion oficial de Kubernetes para Linux y descarga el binario actual.

Ejemplo de instalacion:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Verificacion:

```bash
kubectl version --client --output=yaml
```

Referencia oficial:

- [Instalar y configurar kubectl en Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

## Paso 5 - Instalar `kind` en WSL

`kind` necesita Docker o Podman. En este laboratorio usamos Docker Desktop con WSL 2.

Instala la release binaria desde la pagina oficial de `kind` y coloca el binario en tu `PATH`.

Ejemplo:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

Si la release estable cambia, reemplaza `v0.31.0` por la version actual que marque la pagina oficial.

Verificacion:

```bash
kind version
```

Referencia oficial:

- [kind Quick Start](https://kind.sigs.k8s.io/docs/user/quick-start/)

## Paso 6 - Instalar `helm` en WSL

Usa el instalador oficial del proyecto Helm:

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

Verificacion:

```bash
helm version
```

Referencia oficial:

- [Installing Helm](https://helm.sh/docs/v3/intro/install/)

## Paso 7 - Comprobacion final

Antes de pasar al lab, confirma que las herramientas responden:

```bash
docker version
kubectl version --client --output=yaml
kind version
helm version
```

Resultado esperado:

- Docker responde desde WSL
- `kubectl` esta en el `PATH`
- `kind` esta en el `PATH`
- `helm` esta en el `PATH`

## Siguiente paso

Cuando esto funcione, continua con [Beginner 00 - Prerrequisitos del laboratorio](../../Beginner/00_Prerrequisitos/README.md).
