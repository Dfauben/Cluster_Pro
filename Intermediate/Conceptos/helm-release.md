# Release de Helm

## Que es

Una release es una instancia instalada de un chart en un cluster/namespace.

## Operaciones clave

- `install`: crea release
- `upgrade`: aplica cambios
- `history`: historial de revisiones
- `rollback`: vuelve a una revision anterior
- `uninstall`: elimina release

## Comandos base

```bash
helm list -n <namespace>
helm history <release> -n <namespace>
helm rollback <release> <revision> -n <namespace>
```
