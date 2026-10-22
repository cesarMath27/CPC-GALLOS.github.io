# Flujo de trabajo con asistentes de IA

Esta guía reúne las convenciones del repositorio para que una persona o un asistente de IA pueda proponer cambios pequeños, coherentes con el blog y fáciles de revisar.

## Flujo recomendado

1. **Entender la tarea.** Aclara el resultado esperado, los archivos que pueden cambiar y cómo se reconocerá que quedó listo. Si faltan datos de contenido, identifica los supuestos antes de redactar.
2. **Leer el contexto del repositorio.** Revisa `AGENTS.md`, `.cursor/rules/`, `README.md` y, cuando exista, `.agents/AGENTS.md`. Si vas a crear un post, consulta también `_data/authors.yml`.
3. **Cuidar el estado de Git.** Ejecuta `git status --short` y revisa los cambios existentes antes de editar. No sobrescribas ni incluyas cambios ajenos a la tarea.
4. **Explorar antes de cambiar.** Para entender código y relaciones, consulta Graphify (`graphify query`, `graphify path` o `graphify explain`) y GitNexus cuando estén disponibles. Usa los archivos fuente como referencia final.
5. **Hacer un cambio acotado.** Edita solo lo necesario y sigue las convenciones de la sección correspondiente. Si la tarea exige cambiar una zona protegida, detente y solicita revisión humana explícita.
6. **Revisar el resultado.** Inspecciona el diff y `git status --short`; explica qué cambió, qué validaste y cualquier limitación. Después de cambios de código, actualiza el índice con `graphify update .` si Graphify está configurado.

## Dónde va cada cambio

- **Artículos publicados:** `_posts/`, con nombre `YYYY-MM-DD-titulo.md`.
- **Borradores:** `_drafts/`.
- **Pestañas o secciones principales:** `_tabs/`.
- **Imágenes de artículos:** `assets/img/posts/`. No agregues imágenes de favicon.
- **Autores:** `_data/authors.yml`. El `author` del post debe corresponder a un `author_id` definido allí.
- **Documentación del proyecto:** `docs/`, salvo que las instrucciones de despliegue indiquen otra cosa.

El sitio es un blog de programación competitiva construido con Jekyll y el tema Chirpy. El contenido editorial se redacta principalmente en español; conserva en inglés los nombres propios, APIs y el código cuando corresponda. Usa enlaces externos con `https://`.

## Reglas para crear un post

Usa el front matter que esperan las reglas del blog. Comprueba los campos y ejemplos actuales en `.cursor/rules/` antes de crear el archivo; normalmente incluyen título, descripción, fecha, categorías, autor, etiquetas y opciones de visualización. Mantén las etiquetas en minúsculas y verifica el identificador del autor. Guarda las imágenes únicamente en `assets/img/posts/` y enlázalas con una ruta válida del repositorio.

No inventes datos, resultados de concursos, citas ni fuentes. Si falta información que afecta la exactitud del artículo, deja el dato señalado para revisión en vez de presentarlo como un hecho.

## Cambios de código y áreas sensibles

Para cambios de código, identifica primero los módulos relacionados y sus dependencias. Haz el cambio mínimo que resuelva el objetivo y conserva las convenciones existentes de formato, nombres y manejo de errores.

`_config.yml`, `.github/workflows/`, `_layouts/` y `_includes/` requieren revisión humana explícita antes de modificarse. No cambies estas rutas como parte incidental de otra tarea. En particular, confirma el efecto de cualquier cambio de configuración sobre el build y la publicación del sitio.

## Validación local

Cuando el entorno tenga Ruby y Bundler instalados, estos comandos ayudan a validar el sitio:

```powershell
bundle install
bundle exec jekyll build
bundle exec htmlproofer _site --disable-external --ignore-urls "/^http:\/\/127.0.0.1/,/^http:\/\/0.0.0.0/,/^http:\/\/localhost/"
```

Usa `bundle install` cuando necesites instalar dependencias; para una revisión normal suele bastar con compilar y ejecutar las comprobaciones pertinentes. Si no se ejecutaron comandos, indícalo claramente en el resumen. Para cambios que no afectan el sitio, explica por qué la compilación no era necesaria.

## Cierre y preparación del commit

Antes de terminar, revisa `git diff --check`, `git diff` y `git status --short`. Confirma que el diff solo incluya los archivos esperados y conserva cualquier cambio previo de la persona usuaria. Resume el resultado, la validación realizada y cualquier revisión pendiente. Sugiere un mensaje de commit semántico, por ejemplo:

```text
docs: agregar guía de flujo de trabajo con IA
```

La persona que mantiene el repositorio decide cuándo crear el commit y qué archivos agregar.

## Ejemplos de prompts útiles

Puedes copiar estos ejemplos y reemplazar el texto entre corchetes:

### Crear un artículo

> Redacta un borrador para `_posts/` sobre **[tema]**, dirigido a **[audiencia]**. Sigue `AGENTS.md` y las reglas de `.cursor/rules/`; confirma el `author_id` en `_data/authors.yml`. Usa el front matter y el nombre de archivo requeridos. Basa las afirmaciones en estas fuentes: **[enlaces o material]**. No inventes datos ni agregues imágenes. Al final, resume los archivos creados y las validaciones que conviene ejecutar.

### Entender una parte del repositorio

> Explícame cómo funciona **[componente o flujo]** en este repositorio. Consulta Graphify o GitNexus si están disponibles y luego verifica la explicación en los archivos fuente. Incluye las rutas relevantes, el recorrido principal y cualquier supuesto; no modifiques archivos.

### Cambiar una pestaña

> Actualiza la pestaña **[nombre]** para que **[resultado esperado]**. Revisa primero las reglas y el archivo existente, limita los cambios a `_tabs/` y conserva el estilo del sitio. Si para completarlo hay que cambiar una ruta protegida, detente y explica por qué. Al terminar, muestra el resumen del diff y el comando de validación recomendado.

### Corregir un error

> Investiga el error **[síntoma o mensaje]**. Traza sus dependencias con Graphify o GitNexus si están disponibles, identifica la causa en el código y aplica el cambio mínimo. Conserva mis cambios actuales. Después revisa el diff, indica qué validación ejecutaste y si queda algún riesgo.

### Revisar un diff

> Revisa los cambios de **[rama, commit o archivos]** buscando errores funcionales, regresiones, enlaces rotos y convenciones incumplidas. Prioriza hallazgos concretos e incluye la ruta y línea correspondiente. No edites archivos; si no encuentras problemas, menciona también qué aspectos no pudiste validar.

### Actualizar la documentación

> Actualiza `docs/ai-workflow.md` para reflejar **[cambio de proceso]**. Verifica las convenciones actuales en `AGENTS.md` y `.cursor/rules/`, conserva los ejemplos útiles y añade o corrige un prompt de ejemplo al final si ayuda. No modifiques `_config.yml` ni otras rutas protegidas sin revisión humana explícita.
