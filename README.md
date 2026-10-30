# NimbusERP — Módulo de Gestión de Inventario y Stock

**Caso:** NimbusTech Soluciones S.A.
**Asignatura:** Organización Empresarial — Tecnicatura Universitaria en Programación a Distancia (UTN)
**Trabajo:** TPI — Entrega N.º 4: Procesos, Trabajo Colaborativo y Control Integrador

## Descripción del sistema

NimbusERP es el producto de NimbusTech Soluciones S.A. para PyMEs. Este repositorio aloja la documentación técnica del **módulo de Gestión de Inventario y Stock**, que:

- registra los movimientos de stock (INGRESO, EGRESO, AJUSTE y DEVOLUCION) por producto y por depósito;
- valida cada movimiento con reglas de integridad antes de aceptarlo;
- calcula el stock resultante y conserva el historial completo;
- genera alertas de reposición y órdenes de compra sugeridas al proveedor cuando el stock llega al mínimo.

El modelo de datos (entidades PRODUCTO, MOVIMIENTO_STOCK, PROVEEDOR y DEPOSITO) se definió en la Entrega N.º 3; el proceso que automatiza el módulo se modela en BPMN en esta entrega.

## Integrantes

| Integrante | GitHub |
|---|---|
| J. Javier Soria | [@ImAgInArIaS](https://github.com/ImAgInArIaS) |

## Contenido del repositorio

| Ruta | Contenido |
|---|---|
| `docs/bpmn/` | Diagrama BPMN del proceso *Reposición de stock* (PNG y SVG) |
| `docs/modelo-datos.md` | Entidad USUARIO y esquema de vínculos con cardinalidades |
| `docs/historias-de-usuario.md` | Las tres Historias de Usuario con criterios de aceptación |
| `docs/indicadores-control.md` | Indicadores de control, estándares de desempeño y consultas de auditoría |
| `backlog/` | Archivo de importación de las tareas del tablero |
| `setup_github.sh` | Script con los comandos usados para crear ramas, commits y Pull Requests |

## Proceso modelado (BPMN)

![Proceso de reposición de stock](docs/bpmn/reposicion-stock.png)

Pools: **Cliente PyME** (con los lanes *Encargado de depósito*, *NimbusERP (sistema)* y *Responsable de compras*) y **Proveedor externo**. Compuertas de excepción: movimiento válido, stock bajo el mínimo y proveedor activo.

## Flujo de trabajo (Git)

- La rama `main` solo recibe cambios mediante Pull Request con revisión de un par.
- Una rama por tema: `docs/bpmn-reposicion`, `docs/historias-usuario`, `docs/indicadores-control`.
- Mensajes de commit con el formato `tipo(ámbito): descripción en imperativo` (por ejemplo `docs(bpmn): agregar diagrama del proceso de reposición de stock`).

## Declaración de Uso de IA

Se utilizó un asistente de IA generativa (Claude, de Anthropic) como apoyo en esta entrega.

**Para qué se usó:**

1. Estructurar el documento sobre la plantilla de la cátedra.
2. Generar con código (Python y Matplotlib) el diagrama BPMN a partir del proceso definido sobre el diccionario de datos de la Entrega N.º 3.
3. Redactar borradores de las Historias de Usuario, de los indicadores de control y de este README.
4. Preparar el script de comandos Git del repositorio.

**Prompts utilizados y justificación crítica:**

| Prompt (resumen) | Por qué se usó |
|---|---|
| Se compartió el enunciado de la Entrega N.º 4 y la plantilla de la cátedra, pidiendo un resumen de requisitos. | Verificar que ninguna consigna ni el formato de entrega quedara sin cubrir. |
| Se compartió la Entrega N.º 3 y se pidió completar la Entrega N.º 4 en continuidad con ella. | Obligar al asistente a reutilizar las entidades, campos y criterios de integridad ya definidos, en lugar de inventar un modelo nuevo, para que el BPMN, las historias y los indicadores sean coherentes con las entregas previas. |

**Límites:** el asistente no tuvo acceso a la cuenta de GitHub ni al tablero; la creación del repositorio, las ramas, el Pull Request, la revisión de pares y el tablero las realiza el autor directamente.

**Correcciones humanas sobre lo generado por la IA:**

> COMPLETAR ANTES DE ENTREGAR: describir 2 o 3 correcciones propias reales y el motivo de cada una (por ejemplo, un ajuste a una regla de validación, un cambio en un estándar de los indicadores o una corrección de un paso del BPMN).

Los errores o "alucinaciones" del asistente son responsabilidad del autor, conforme a la pauta de la cátedra.
