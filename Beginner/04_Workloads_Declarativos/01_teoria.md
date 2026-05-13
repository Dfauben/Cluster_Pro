# Beginner 04 - Despliegues declarativos

## Navegacion

- [🏠 Inicio del repositorio](../../README.md)
- [📘 Inicio de Beginner](../README.md)
- [📑 Índice del módulo](README.md)
- [⬅️ Anterior](README.md)
- [➡️ Siguiente](02_lab.md)

Cuando trabajas de forma declarativa, no dices "haz esto ahora" sino "este es el estado que quiero". Kubernetes compara ese fichero con lo que hay en el cluster y ajusta lo necesario para que ambos coincidan.

Un archivo YAML no es un script. Es una descripcion estructurada del recurso que quieres crear. Por eso la indentacion importa y por eso merece la pena escribirlo con calma en `nano` o `vim` antes de aplicarlo.

| Parte del YAML | Qué significa | Qué controlas |
|---|---|---|
| `apiVersion` | version de la API | la familia de recurso |
| `kind` | tipo de objeto | si es `Deployment`, `Service`, etc. |
| `metadata` | identidad del recurso | nombre, labels y namespace |
| `spec` | estado deseado | replicas, imagen, puertos, estrategia |

<br>

La idea importante es que el fichero se convierte en la referencia del recurso. Si cambias el YAML y vuelves a aplicar, Kubernetes no adivina nada: reconcilia el cluster con lo que acabas de declarar.

```text
YAML -> apply -> recurso en el cluster -> reconciliacion
```

Cuando entiendes esto, dejas de pensar solo en comandos sueltos y empiezas a trabajar con una declaracion repetible. Eso te permite versionar cambios, revisarlos y repetirlos sin depender de recordar cada paso manual.

**Errores tipicos**
- editar el recurso "a mano" sin saber que el YAML es la fuente de verdad
- confundir `apply` con un script
- mezclar demasiadas ideas en un mismo fichero
- olvidar que `spec` describe el comportamiento real

**Qué debes retener**
- un YAML describe estado deseado
- `apply` sincroniza ese estado con el cluster
- `metadata` identifica, `spec` define comportamiento
- el fichero es mas estable que una secuencia de comandos sueltos

## ➡️ Siguiente

Continua con [Practica guiada](02_lab.md).
