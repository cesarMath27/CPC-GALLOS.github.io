# 🤖 Guía de Configuración: Servidores MCP en Cursor

¡Hola, colaborador de CPC-GALLOS! 👋 

Este proyecto utiliza **Model Context Protocol (MCP)** para potenciar las capacidades de inteligencia artificial dentro del editor **Cursor**. Estos servidores le permiten a la IA interactuar directamente con tu entorno local, recordar el contexto entre sesiones, consumir APIs estáticas y leer Pull Requests o Issues directamente desde GitHub.

A continuación, te explicamos cómo activar esta superpotencia en tu máquina local.

## 📋 Prerrequisitos

Para que los servidores funcionen, tu computadora necesita tener lo siguiente instalado:

1. **Cursor IDE:** Asegúrate de estar usando el editor Cursor.
2. **Node.js y npm:** Los servidores MCP de esta configuración se ejecutan mediante el comando `npx`. Si no tienes Node.js, [descárgalo e instálalo aquí](https://nodejs.org/).

## 🚀 Pasos de Instalación

El archivo `.cursor/mcp.json` ya contiene la configuración base. Solo necesitas realizar un par de ajustes locales.

### Paso 1: Generar tu Token de GitHub
Para que el servidor de GitHub pueda leer los repositorios, PRs e Issues del club, necesitas un Token de Acceso Personal (PAT):
1. Ve a GitHub: `Settings` > `Developer settings` > `Personal access tokens` > `Tokens (classic)`.
2. Haz clic en **Generate new token (classic)**.
3. Dale un nombre (ej. "Cursor MCP Local") y otórgale permisos sobre **`repo`** (Full control of private repositories).
4. Genera el token y **CÓPIALO** (empieza con `ghp_...`). No podrás verlo de nuevo.

### Paso 2: Configurar el Token Localmente ⚠️ (IMPORTANTE)
Abre el archivo `.cursor/mcp.json` y reemplaza la cadena `"<TU_TOKEN_AQUI>"` por tu token real.

**🛑 ¡ALTO AHÍ! REGLA DE SEGURIDAD 🛑**
**NUNCA** debes hacer commit de tu token real. Para evitar subirlo accidentalmente a tu Fork o al repositorio principal, ejecuta el siguiente comando en tu terminal para decirle a Git que ignore tus cambios locales en este archivo:

```bash
git update-index --assume-unchanged .cursor/mcp.json
```
*(Si alguna vez necesitas volver a trackear el archivo para hacer un cambio oficial en la estructura, usa `--no-assume-unchanged`).*

### Paso 3: Reiniciar Cursor
Una vez guardado el archivo `mcp.json` con tu token:
1. Abre la configuración de Cursor (Ctrl + Shift + J / Cmd + Shift + J o ve a `Settings` > `Features` > `MCP`).
2. Cursor debería detectar automáticamente los servidores configurados en el archivo `.cursor/mcp.json`.
3. Si los servidores aparecen en estado de error, presiona el botón de recarga (refresh) o reinicia por completo el editor Cursor. Deberían aparecer todos con un indicador verde.

---

## 🛠️ ¿Qué servidores estamos usando?

*   **GitHub (`server-github`)**: Permite a Cursor leer y buscar dentro de los repositorios de GitHub, leer issues, comentarios y pull requests. Ideal para entender qué tarea estás resolviendo.
*   **Filesystem (`server-filesystem`)**: Le da a la IA la capacidad de leer, buscar y editar archivos de manera estructurada y segura dentro de la carpeta de este proyecto.
*   **Fetch (`server-fetch`)**: Permite a Cursor consumir endpoints y APIs externas para traer información actualizada (por ejemplo, buscar datos de algún juez en línea o documentaciones técnicas).
*   **Memory (`server-memory`)**: Habilita un grafo de conocimiento local persistente. Cursor "recordará" reglas específicas, preferencias y decisiones técnicas que hayas tomado en el pasado, mejorando la coherencia entre tus diferentes sesiones de programación.

¡Eso es todo! Ahora tu asistente de IA está completamente equipado para ayudarte a desarrollar y escribir posts en el blog de CPC-GALLOS.