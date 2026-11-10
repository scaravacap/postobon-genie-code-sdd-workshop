# Prerrequisitos del taller

Para que cada participante haga el laboratorio en su workspace de desarrollo, necesito que ustedes tengan listos estos seis puntos antes del taller. Toda la práctica corre con datos sintéticos que imitan las tablas de comisiones y con un ATL reducido que construí para el taller: no se usan datos reales ni el ATL real.

## 1. Un catálogo por participante

Les propongo `cx_postobon_sdd_<usuario>_glux`, por ejemplo `cx_postobon_sdd_aperez_glux`, con permisos completos para su dueño.

El sufijo `_glux` es a propósito. Sus `.conf` dicen `catalogo = {{Environment}}_glux`, así que con el entorno `cx_postobon_sdd_aperez` apuntan a ese catálogo sin cambiar una línea, igual que `dllo` apunta a `dllo_glux`.

El notebook de setup crea dentro los schemas `oro`, `plata`, `stg`, `conf` y `taller`, con datos sintéticos. Las utilidades del taller se niegan a escribir en un catálogo que no empiece por `cx_postobon_sdd`, de modo que el laboratorio no puede tocar `dllo_glux`.

Un ejemplo para el administrador:

```sql
CREATE CATALOG IF NOT EXISTS cx_postobon_sdd_aperez_glux
  COMMENT 'Taller SDD Genie Code. Solo datos sinteticos';
GRANT ALL PRIVILEGES ON CATALOG cx_postobon_sdd_aperez_glux TO `<correo_participante>`;
```

Si su metastore exige ubicación administrada, agreguen el `MANAGED LOCATION` que usen normalmente.

Si prefieren no crear un catálogo por persona, me sirve uno solo, `cx_postobon_sdd_workshop_glux`, y trabajamos en parejas por turnos: el setup de una persona deja el catálogo en el estado inicial, así que dos personas a la vez sobre el mismo catálogo se pisan.

## 2. Entitlement "Workspace access" para cada participante

Las skills y las instrucciones personales de Genie Code son archivos en la carpeta de cada usuario (`/Users/<correo>/.assistant/skills/` y `/Users/<correo>/.assistant_instructions.md`). Para crearlos hace falta el entitlement **Workspace access**, que es el que da lectura y escritura sobre objetos del workspace ([entitlements](https://learn.microsoft.com/en-us/azure/databricks/security/auth/entitlements)).

Para probarlo, cada persona abre **Genie Code > Settings > User instructions > Add instructions file** ([instructions](https://learn.microsoft.com/en-us/azure/databricks/genie-code/instructions)). Si falla, revisen en este orden:

1. Que el usuario tenga el entitlement **Workspace access**.
2. Que los archivos de workspace estén habilitados en el workspace.
3. Que el usuario tenga CAN MANAGE sobre su carpeta `/Users/<correo>`.

Si sigue fallando, envíenme el texto exacto del error y lo resolvemos antes del taller.

## 3. Acceso a GitHub desde Git folders

El material vive en este repositorio público. En el workspace se clona con **Workspace > Create > Git folder**. Si su red bloquea github.com, avísenme y les llevo el paquete para importarlo con **Import**.

## 4. Compute

Serverless habilitado para notebooks y jobs. Los scripts de las skills, el setup y las ETL del taller corren ahí.

## 5. Sus skills `postobon-*` de workspace no se tocan

Durante el laboratorio cada participante instala la versión v2 en su carpeta personal y apaga, solo para sí, las de workspace desde la configuración de Genie Code. No hay que borrar ni editar nada del equipo. Al final, la [guía](lab_guide.md) explica cómo volver a como estaban.

## 6. Laptop con acceso al workspace de desarrollo

Cada persona con su laptop y su sesión abierta en el workspace.

## Lista para comprobar antes del taller

- [ ] El catálogo `cx_postobon_sdd_<usuario>_glux` existe y el participante puede crear schemas en él.
- [ ] **Add instructions file** funciona en Genie Code.
- [ ] El Git folder del repositorio clona.
- [ ] Un notebook corre en serverless.
