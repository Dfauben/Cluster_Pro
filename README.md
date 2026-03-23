# K8s Lab - Gestion y Maniobra desde 0

Este repositorio esta organizado para aprender Kubernetes paso a paso, con foco en operacion real con `kubectl`.

## Entorno oficial del laboratorio

Todo se ejecuta **siempre desde WSL**:
- comandos `kubectl`
- comandos `kind`
- comandos `helm`
- comandos `docker` (tambien desde WSL)

## Formato de imagenes en README

Estandar acordado para este repositorio:
- Imagen de presentacion del README de cada modulo: `1280 x 640 px`
- Imagen de presentacion de cada submodulo: `1280 x 160 px`

## Estructura

- `Beginner/`: base operativa desde cero.
- `Intermediate/`: operacion intermedia y patrones de produccion.
- `Pro/`: seguridad, GitOps, observabilidad y operacion avanzada.
- `PROGRESS.md`: bitacora viva del laboratorio.

## Accesos rapidos

- [Beginner - README principal](Beginner/README.md)
- [Beginner - Conceptos](Beginner/Conceptos/README.md)
- [Intermediate - README principal](Intermediate/README.md)
- [Intermediate - Conceptos](Intermediate/Conceptos/README.md)
- [Intermediate - Cluster y Nodos](Intermediate/00_Cluster_y_Nodos/README.md)

## Orden recomendado

1. `Beginner/00_Fundamentos`
2. `Beginner/01_Kubectl_Operacion`
3. `Beginner/02_Workloads_Basicos`
4. `Beginner/03_Debug_Operativo`
5. `Intermediate/00_Cluster_y_Nodos`
6. `Intermediate/01_Probes_Salud`
7. `Intermediate/02_Recursos_y_Scheduling`
8. `Intermediate/03_Networking_e_Ingress`
9. `Intermediate/04_Storage_Persistencia`
10. `Intermediate/05_Helm_Base`
11. `Pro`

## Regla de trabajo

En cada bloque:
1. Ejecutar comandos.
2. Entender salida.
3. Documentar resultado en `PROGRESS.md`.
