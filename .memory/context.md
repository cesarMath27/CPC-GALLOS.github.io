# Contexto del proyecto

## Propósito y arquitectura

CPC-GALLOS es el Club de Programación Competitiva de la Universidad Autónoma de Aguascalientes. Este repositorio publica su blog y recursos para estudiantes. El sitio es estático, está escrito principalmente en español y se genera con Jekyll y el tema Chirpy para GitHub Pages.

| Ruta | Contenido |
| --- | --- |
| `_posts/` | Artículos publicados: recursos, concursos, entrenamiento, oportunidades y vida del club. |
| `_drafts/` | Borradores aún no publicados. |
| `_tabs/` | Páginas principales del menú; `about.md` describe al club. |
| `_data/` | Datos del sitio, autores y textos de interfaz. Valida `author` contra `_data/authors.yml`. |
| `_includes/`, `_layouts/` | Componentes y plantillas de Jekyll/Chirpy. Son zonas sensibles del tema. |
| `assets/img/posts/` | Imágenes de artículos y recursos visuales asociados. |
| `assets/js/posts/` | JavaScript de funciones interactivas de algunos artículos. |
| `.github/workflows/` | Automatización de compilación y publicación en GitHub Pages. |

La API de datos se mantiene en el repositorio separado `CPC-GALLOS/api`; sus endpoints públicos siguen el patrón `https://cpc-gallos.github.io/api/<dataset>/data.json` y el índice está en `https://cpc-gallos.github.io/api/index.json`.

## Entorno de desarrollo

- Requisitos documentados: Ruby 3.3+, Bundler y herramientas de compilación nativas.
- Instalar dependencias: `bundle install`.
- Servir localmente: `bundle exec jekyll serve` (por defecto en `http://127.0.0.1:4000`).
- Compilar: `bundle exec jekyll build`.
- Validar HTML y enlaces: `bundle exec htmlproofer _site ...`; el README y `.agents/AGENTS.md` contienen el comando recomendado.
- Antes de integrar cambios de contenido, validar la compilación y los enlaces según las instrucciones del proyecto.

## Convenciones de contenido

- Lee `.cursor/rules/` y `AGENTS.md` antes de editar. El texto editorial del blog debe estar en español; el código puede estar en inglés o C++.
- Los artículos nuevos van en `_posts/` con nombre `YYYY-MM-DD-Titulo_Con_Guiones_Bajos.md` y front matter completo: `title`, `description`, `date`, `categories`, `author`, `tags`, `pin`, `mermaid` e `image`.
- Usa un `author` existente en `_data/authors.yml`; mantén las etiquetas en minúsculas y las categorías como lista.
- Usa `https://` en enlaces externos. Las imágenes de artículos van en `assets/img/posts/`; nunca agregues imágenes en `assets/img/favicons/`.
- Para editar menús o páginas principales, trabaja en `_tabs/`.
- `_config.yml`, `.github/workflows/`, `_layouts/` e `_includes/` requieren revisión humana explícita antes de modificarse, según `AGENTS.md`.

## Contexto para asistentes

- El skill de Graphify del proyecto está en `.codex/skills/graphify/`; el grafo legible por máquina, el reporte y la visualización están en `graphify-out/`. Para explorar el contenido usa `graphify query "<pregunta>"`, `graphify path "<concepto A>" "<concepto B>"` o `graphify explain "<concepto>"`. Después de modificar código, actualiza con `graphify update .`.
- GitNexus aporta relaciones estructurales del repositorio mediante MCP y el índice local `.gitnexus/`. Comprueba su vigencia con `node .gitnexus/run.cjs status`; el índice no sustituye la lectura de artículos para cambios editoriales.
- Conserva los cambios existentes del usuario. Revisa `git status --short` y agrega al commit solo archivos que pertenezcan a la tarea actual.
