# Taller avanzado de Genie Code: Spec-Driven Development en un ETL de comisiones

Material del taller para el equipo de ingeniería de datos de Postobón, nivel L200-L300. Muestra cómo aplicar Spec-Driven Development (SDD) y un ciclo de vida agéntico **dentro de Genie Code**, con los errores reales de la migración de un ETL de comisiones desde SAP Data Services como punto de partida.

Lo armé para que ustedes lo sigan en su workspace de desarrollo, con o sin facilitador. Todo el laboratorio corre con **datos sintéticos** y con un ATL reducido construido para el taller: no contiene datos ni código reales de la empresa.

## Por dónde empezar

1. Revisen los [prerrequisitos](prerrequisitos.md): un catálogo por participante, el entitlement Workspace access y acceso a este repositorio desde un Git folder.
2. Sigan la [guía del laboratorio](lab_guide.md) desde el Lab 0. Está escrita para seguirse sin facilitador.

## Contenido

| Archivo | Qué es |
|---|---|
| [`agenda.md`](agenda.md) | Bloques del taller de 210 minutos |
| [`slides_outline.md`](slides_outline.md) | Guion de diapositivas, con fuentes públicas |
| [`lab_guide.md`](lab_guide.md) | Labs 0 a 4 y el 5 opcional, con prompts, resultado esperado y troubleshooting |
| [`resultados_experimento.md`](resultados_experimento.md) | Experimento v1 contra v2 con el Genie Code task de Jobs |
| [`openspec_speckit_assessment.md`](openspec_speckit_assessment.md) | Si OpenSpec o Spec Kit sirven tal cual dentro de Genie Code |
| [`prerrequisitos.md`](prerrequisitos.md) | Lo que debe estar listo en el workspace antes del taller |
| [`lab/`](lab/) | Todo lo que se instala y se ejecuta en el workspace |

## Qué hay en `lab/`

| Carpeta | Qué contiene |
|---|---|
| [`mapa_controles.md`](lab/mapa_controles.md) | Los 11 errores del caso (E1 a E11), con su control, dónde vive y si es blando o determinista |
| `constitucion_v2/` | Instrucciones v2 de Genie Code y el `AGENTS.md` que viaja con el código |
| `skills_v2/` | Las 4 skills v2: `postobon-spec-desde-atl`, `postobon-etl-crear`, `postobon-etl-verificacion` y `postobon-atl-comparacion`, con sus scripts y plantillas |
| `plantillas/` | `spec.md`, `plan.md` y `verification_report.md` |
| `controles/` | `atl_inventario.py`, `conf_linter.py`, `aceptacion.py`, el notebook `verificacion_aceptacion` y un `databricks.yml` mínimo, con sus pruebas |
| `entorno/` | Setup del catálogo sintético, utilidades del framework con las mismas firmas, el ATL del taller, las ETL de referencia y los escenarios con errores sembrados |
| `experimento/` | Prompts, notebooks de reset y evaluación, y el protocolo del job del experimento v1 contra v2 |

## Cómo protege el taller su entorno

- **Guard de catálogo.** El setup y las utilidades se niegan a trabajar sobre un catálogo que no empiece por `cx_postobon_sdd`. El laboratorio no puede escribir en `dllo_glux`, `prbs_glux` ni `prod_glux`.
- **Configuración personal.** Las skills y las instrucciones v2 se instalan en la carpeta del usuario, con respaldo de las instrucciones anteriores. Las skills de workspace del equipo no se modifican.
- **Datos sintéticos.** Las tablas, el ATL y los archivos esperados se generan con una semilla fija: son inventados y reproducibles.

## Qué está probado

Instalé y corrí el laboratorio en un workspace de Azure Databricks con serverless el 9 de noviembre de 2026:

- Las 3 ETL de referencia pasan el linter y la aceptación, 4 de 4 escenarios.
- El camino del participante, desde una copia de `lab/` en el workspace: setup, controles y la ETL del Lab 4, cuyos 5 errores aparecen como se diseñaron.
- Las pruebas locales de los controles y del entorno pasan.
- El bundle del Lab 5, desplegado y corrido desde zsh: pasa con la ETL correcta, falla en `aceptacion` con otra fecha de corte y falla en `etl` con un `%` suelto en un `.conf`.
- El 10 de noviembre, el setup con `instalar_v2 = si` desde una copia de `lab/`: instaló la constitución y las 4 skills v2 en mi usuario, y esa fue la v2 del experimento.

Lo que todavía no probé:

- Clonar este repositorio como Git folder. La prueba del participante usó una copia de `lab/` subida al workspace.

La comparación de v1 contra v2 está en [`resultados_experimento.md`](resultados_experimento.md). En el entorno sintético, v2 no mejoró el resultado: las dos variantes resolvieron casi lo mismo al primer intento, y v2 dejó más evidencia escrita por scripts y tardó más.

## Fuentes

Las afirmaciones de producto del material citan la documentación pública de Azure Databricks. Las principales: [Genie Code](https://learn.microsoft.com/en-us/azure/databricks/genie-code/), [instructions](https://learn.microsoft.com/en-us/azure/databricks/genie-code/instructions), [skills](https://learn.microsoft.com/en-us/azure/databricks/genie-code/skills), [Navigate Genie Code](https://learn.microsoft.com/en-us/azure/databricks/genie-code/navigate-genie-code) y [Genie Code task para jobs](https://learn.microsoft.com/en-us/azure/databricks/jobs/tasks/genie-code).
