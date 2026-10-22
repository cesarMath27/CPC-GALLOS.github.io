# Guía para contribuir

¡Gracias por ayudar a mejorar el blog del Club de Programación Competitiva GALLOS! Aceptamos contribuciones de miembros del club y de la comunidad.

## Antes de empezar

- Lee el [README](README.md) para conocer el proyecto, preparar el entorno local y revisar las convenciones de publicación.
- Si vas a trabajar con un asistente de IA, consulta el [flujo de trabajo con asistentes de IA](docs/ai-workflow.md), que reúne el contexto del repositorio, herramientas como GitNexus y ejemplos de prompts.
- Revisa `git status --short` y conserva cualquier cambio local que ya tengas.

## Proponer un cambio

1. Define el cambio y mantén el alcance enfocado. Para una mejora grande, conversa primero con los mantenedores mediante un issue.
2. Crea una rama con un nombre descriptivo y realiza cambios pequeños que sean fáciles de revisar.
3. Sigue las convenciones del README y las instrucciones locales del repositorio, en particular `AGENTS.md` y `.cursor/rules/`.
4. Compila el sitio y revisa los enlaces cuando el cambio afecte contenido o código del sitio:

   ```bash
   bundle exec jekyll build
   bundle exec htmlproofer _site --disable-external --ignore-urls "/^http:\/\/127.0.0.1/,/^http:\/\/0.0.0.0/,/^http:\/\/localhost/"
   ```

   Si no puedes ejecutar una validación, indícalo en la descripción del Pull Request.

5. Revisa `git diff` y `git status --short`. Agrega al commit solo los archivos relacionados con tu contribución.
6. Abre un Pull Request que explique qué cambió, por qué y qué validaciones ejecutaste. Incluye capturas si el cambio modifica el aspecto visual del sitio.

## Commits

Usa mensajes breves y descriptivos. Se recomienda el formato convencional, por ejemplo:

```text
docs: aclarar instrucciones para colaboradores
fix: corregir enlace de una pestaña
feat: agregar guía de grafos
```

Los mantenedores revisarán el Pull Request y podrán solicitar ajustes antes de integrarlo.
