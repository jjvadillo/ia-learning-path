# CLAUDE.md

Contexto persistente para Claude Code en este repositorio. Léelo siempre al empezar una sesión aquí.

## Qué es este repositorio

`ia-learning-path` es mi repo de práctica para un programa de estudio basado en los cursos de `anthropic.skilljar.com`. El objetivo es aprender a construir con la API de Claude, MCP y Claude Code, manteniendo en paralelo un track equivalente en **Java** (soy arquitecto de soluciones Java explorando una transición hacia desarrollo/arquitectura de IA).

Cada fase del programa tiene:
- un **proyecto implementado** (referencia ya resuelta, para estudiar, normalmente en Python o TypeScript según el curso original),
- un **proyecto sin implementar** (lo construyo yo, normalmente en Java, a veces en el mismo lenguaje del curso si el bloque es puramente conceptual).

## Dónde está la documentación del programa

**`docs/`** contiene el programa completo y el material de cada fase en Markdown:

- `docs/00-programa-estudio-anthropic-ia.md` — programa completo, las 6 fases + proyecto final, con qué ver en Skilljar y qué construir en cada bloque.
- `docs/fase0-*.md`, `docs/fase1-*.md`, `docs/fase2-*.md`, etc. — un archivo (o varios) por fase/sub-fase, generados a medida que avanzo.

**Antes de ayudarme con cualquier tarea de una fase, lee primero el archivo de esa fase en `docs/` (y `docs/00-programa-estudio-anthropic-ia.md` si necesitas el contexto global).** No asumas el contenido de memoria: los enunciados y criterios de aceptación exactos están en esos archivos.

Cuando te diga "estamos en la Fase X" o "haz el proyecto sin implementar de la fase X", busca primero el `.md` correspondiente en `docs/` antes de proponer código.

## Estructura del repositorio

```
ia-learning-path/
├── CLAUDE.md                     # este archivo
├── docs/                         # programa + un .md por fase (fuente de verdad de los enunciados)
├── 00-fundamentos/                # Fase 0 — sin código, análisis/ADRs
├── 01-claude-platform-101-ts/     # Fase 1 — TypeScript
├── 02-claude-api-python/          # Fase 2 — Python, subcarpeta por sub-bloque
│   ├── 01-accessing-api/
│   ├── 02-prompt-evaluation/
│   ├── 03-prompt-engineering/
│   ├── 04-tool-use/
│   ├── 05-rag-agentic-search/
│   ├── 06-features-thinking-caching/
│   ├── 07-mcp/
│   └── 08-agents-workflows/
├── 03-mcp-intro-python/           # Fase 3
├── 04-mcp-advanced-python/        # Fase 3
├── 05-claude-code-workflow/       # Fase 4 — CLAUDE.md, hooks, skills, subagentes de práctica
├── 06-java-track/                 # TODOS mis proyectos "sin implementar" en Java
│   ├── pom.xml
│   └── src/main/java/...
└── 07-proyecto-final-arquitectura/
```

## Convenciones generales

- Cada carpeta de fase/sub-bloque tiene su propio `README.md` con: qué se está practicando, cómo ejecutar el proyecto, y qué falta por hacer.
- No mezclar código de "implementado" (referencia) con "sin implementar" (mi solución) en la misma carpeta salvo que la fase lo indique explícitamente.
- Commits en español, formato Conventional Commits (`feat:`, `fix:`, `docs:`, `test:`, `chore:`), en minúsculas, imperativo. Ej: `feat(fase2-tool-use): agente con tool getStockPrice en Java`.
- No hacer commit de API keys ni archivos `.env`. Usar variables de entorno (`ANTHROPIC_API_KEY`) y mantener `.env.example` sin valores reales.

## Track Python (proyectos implementados y algunos ejercicios conceptuales)

- Python 3.11+, entorno virtual por carpeta (`python -m venv .venv`).
- Dependencias en `requirements.txt` por sub-carpeta, no un único requirements global.
- Cliente oficial: `anthropic` (SDK Python).
- Tests con `pytest`. Comando: `pytest -v` desde la carpeta del proyecto.
- Formateo: `black .` antes de cada commit.

## Track Java (mis proyectos "sin implementar", carpeta `06-java-track/` y equivalentes dentro de cada fase)

- Java 21, Maven (`pom.xml` en la raíz del track).
- Framework por defecto para servicios: **Spring Boot 3.x** cuando el ejercicio lo pida (endpoints REST, RAG service, MCP server).
- Cliente oficial: SDK Java de Anthropic (`com.anthropic:anthropic-java`) — usarlo siempre en vez de llamar a la API REST a mano, salvo que el ejercicio pida explícitamente entender el detalle HTTP.
- Estructura de paquete: `com.miempresa.ialearning.<fase>.<modulo>`.
- Tests con JUnit 5, siguiendo el patrón AAA (Arrange-Act-Assert). Comando: `mvn test` desde `06-java-track/`.
- Estilo: separar siempre "tool schema / integración con Claude" de "lógica de negocio" en clases/paquetes distintos — es un requisito explícito del programa (ver Fase 2.4 en `docs/`), no solo una preferencia de estilo.
- Antes de dar por terminado un ejercicio Java: `mvn test` debe pasar en verde y no debe haber warnings de compilación.

## Cómo quiero que trabajes en este repo

1. Si te pido resolver el "proyecto sin implementar" de una fase, primero localiza y lee el `.md` de esa fase en `docs/`, luego propón un plan corto (2-4 líneas) antes de escribir código, salvo que te diga que vayas directo.
2. No copies el proyecto "implementado" de referencia tal cual al track Java — tradúcelo a las convenciones Java/Spring de este repo, no es un port literal línea a línea.
3. Si un requisito del `.md` de la fase es ambiguo, dilo explícitamente en vez de asumir silenciosamente.
4. Al terminar un ejercicio, actualiza el `README.md` de esa carpeta con un resumen de qué se implementó y cómo ejecutarlo/testearlo.
5. No toques carpetas de fases distintas a la que estoy trabajando salvo que te lo pida.