# K8s Lab - Gestion y Maniobra desde 0

Este repositorio esta organizado para aprender Kubernetes paso a paso, con foco en operacion real con `kubectl`.

## Entorno oficial del laboratorio

Primero se prepara el host Windows y WSL.
Despues, todo el trabajo del laboratorio se hace desde WSL:

- comandos `kubectl`
- comandos `kind`
- comandos `helm`
- comandos `docker`

## Formato de imagenes en README

Estandar acordado para este repositorio:
- Imagen de presentacion del README de cada modulo: `1280 x 640 px`
- Imagen de presentacion de cada submodulo: `1280 x 160 px`

## Estructura

- `setup/`: instalacion y validacion del entorno desde cero.
- `Beginner/`: base operativa desde cero.
- `Intermediate/`: operacion intermedia y patrones de produccion.
- `Pro/`: seguridad, GitOps, observabilidad y operacion avanzada.

## Accesos rapidos

- [Setup - Entorno base](setup/README.md)
- [Setup Windows 10/11](setup/windows/README.md)
- [Beginner - README principal](Beginner/README.md)
- [Beginner - Conceptos](Beginner/Conceptos/README.md)
- [Intermediate - README principal](Intermediate/README.md)
- [Intermediate - Conceptos](Intermediate/Conceptos/README.md)
- [Intermediate - Cluster y Nodos](Intermediate/00_Cluster_y_Nodos/README.md)

## Orden recomendado

1. `setup/windows`
2. `Beginner/00_Prerrequisitos`
3. `Beginner/01_Fundamentos`
4. `Beginner/02_Kubectl_Operacion`
5. `Beginner/03_Workloads_Basicos`
6. `Beginner/04_Services_Exposicion`
7. `Beginner/05_Configuracion_Basica`
8. `Beginner/06_Almacenamiento_Basico`
9. `Beginner/07_Debug_Operativo`
10. `Beginner/08_Repaso_Integrador`
11. `Intermediate/00_Cluster_y_Nodos`
12. `Intermediate/01_Probes_Salud`
13. `Intermediate/02_Recursos_y_Scheduling`
14. `Intermediate/03_Networking_e_Ingress`
15. `Intermediate/04_Storage_Persistencia`
16. `Intermediate/05_Helm_Base`
17. `Pro`

## Regla de trabajo

En cada bloque:
1. Ejecutar comandos.
2. Entender salida.
3. Corregir fallos de forma guiada.
4. Verificar el resultado antes de seguir.
