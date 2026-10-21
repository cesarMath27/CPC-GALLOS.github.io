# Stack Tecnológico y Flujos Agénticos (AGENTS.md)

Este documento describe la arquitectura tecnológica del blog de CPC-GALLOS y establece los flujos de trabajo recomendados para asistentes de IA (Agentes) que interactúan con este repositorio.

## 🛠️ Stack Tecnológico Completo

El proyecto es un sitio estático generado con Jekyll, diseñado para ser rápido, seguro y fácil de mantener en GitHub Pages.

**Core Stack:**
- **Framework Generador:** [Jekyll](https://jekyllrb.com/) (Ruby)
- **Tema Base:** [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)
- **Lenguaje Principal:** Markdown (Kramdown) para contenido, HTML/Liquid para plantillas.
- **Estilos:** SCSS (Sass) procesado por Jekyll.
- **Gestor de Paquetes:** Bundler (Gemas de Ruby).
- **Hosting y CI/CD:** GitHub Pages y GitHub Actions.

**Herramientas de Desarrollo y Validación:**
- **Pruebas de HTML y Enlaces:** `html-proofer`
- **Entornos Aislados:** Dev Containers (Docker) / Nix.
- **Asistencia IA:** Cursor IDE con reglas locales en `.cursor/rules/`.

---

## 🤖 Flujo Agéntico (Agentic Workflow)

Para mantener la consistencia y calidad del código, los agentes de IA (como Cursor) deben seguir el siguiente ciclo de vida al ejecutar tareas en este repositorio:

### 1. Inicialización y Contexto
Antes de proponer cualquier código o artículo, el Agente debe:
- Leer obligatoriamente el directorio `.cursor/rules/` para asimilar las convenciones de nomenclatura, front matter y restricciones de edición.
- Analizar el `README.md` para entender el propósito del proyecto (Club de Programación Competitiva).
- Revisar `_data/authors.yml` si la tarea implica la creación de un nuevo post, para asegurar que el `author_id` sea válido.

### 2. Ejecución de la Tarea (Roles)
Dependiendo del prompt del usuario, el Agente asume uno de los siguientes roles:

*   **Agente Redactor (Creación de Posts):**
    *   Genera archivos en `_posts/` usando el formato `YYYY-MM-DD-titulo.md`.
    *   Inyecta el Front Matter YAML estricto.
    *   Redacta el contenido principal en español, manteniendo código en inglés/C++.
    *   Asigna imágenes exclusivamente en `assets/img/posts/`.

*   **Agente Estructural (Menús y Páginas):**
    *   Modifica archivos en `_tabs/` para agregar o editar secciones principales del sitio.
    *   Evita estrictamente modificar `_config.yml`, `_layouts/` o `.github/workflows/` a menos que haya una confirmación explícita de "Revisión Humana".

### 3. Validación y Pruebas
Una vez completada la edición de archivos, el Agente debe recomendar o preparar la validación local:
- Sugerir al usuario correr `bundle exec jekyll build` para verificar que la compilación de Jekyll sea exitosa.
- Recomendar la ejecución de `bundle exec htmlproofer _site ...` para evitar enlaces rotos (links HTTP vs HTTPS).

### 4. Preparación para Integración (PR)
El Agente ayuda al usuario a aislar los cambios:
- Se asegura de que los cambios estén listos para un entorno de *Fork* y *Pull Request*.
- Genera mensajes de commit semánticos (ej. `docs: agregar nuevo post sobre grafos bipartitos` o `chore: actualizar configuración de agentes`).