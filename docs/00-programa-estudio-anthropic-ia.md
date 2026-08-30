# Programa de estudio: De arquitecto Java a desarrollador/arquitecto de soluciones con IA (Claude)

> Basado en la revisión completa de **anthropic.skilljar.com** (agosto 2026): 20 cursos publicados, catálogo, prerrequisitos y currículo de cada uno.
> Objetivo: darte una vía dual **Python + Java**, con un proyecto **implementado** (que ves y estudias) y un proyecto **sin implementar** (que haces tú) por cada bloque de aprendizaje, pensando en dos salidas profesionales posibles: (A) arquitecto de soluciones que integra IA en sistemas Java, o (B) desarrollador de producto/IA a tiempo completo (agentes, MCP, RAG).

---

## 1. Mapa completo del catálogo Skilljar y clasificación

Revisé los 20 cursos publicados en `anthropic.skilljar.com`. Los clasifico en 3 grupos:

### Grupo A — Track técnico (los que vamos a seguir en este programa)
| # | Curso | Lenguaje del curso | Nivel | Por qué importa para ti |
|---|-------|--------------------|-------|--------------------------|
| 1 | **Claude 101** | N/A (uso de producto) | Básico | Contexto rápido, 30 min, para entender el producto antes de programar |
| 2 | **AI Capabilities and Limitations** | N/A | Básico | Fundamentos de qué puede/no puede hacer un LLM — clave para diseñar arquitecturas realistas |
| 3 | **Claude Platform 101** | **TypeScript** (SDK `@anthropic-ai/sdk`) | Medio | Visión completa de la plataforma: agent loop, tool use, thinking, skills, MCP, managed agents |
| 4 | **Building with the Claude API** | **Python** | Medio-Alto | El curso más completo: prompting, evals, tool use, RAG, MCP, agentes, caching — 8h+ |
| 5 | **Introduction to Model Context Protocol** | **Python** (SDK oficial) | Medio | Construir servidores y clientes MCP desde cero |
| 6 | **Model Context Protocol: Advanced Topics** | **Python** (async) | Alto | Sampling, notifications, transports (stdio/HTTP), producción |
| 7 | **Claude Code 101** | N/A (herramienta CLI) | Básico | Flujo diario de trabajo con Claude Code |
| 8 | **Claude Code in Action** | N/A (herramienta CLI) | Medio-Alto | Sesiones largas, hooks, CLAUDE.md, CI/CD, plugins, verificación |
| 9 | **Introduction to agent skills** | Markdown/YAML | Medio | Crear "Skills" reutilizables para Claude Code |
| 10 | **Introduction to subagents** | Markdown/YAML | Medio | Delegar tareas a subagentes especializados |
| 11 | **Introduction to Claude Cowork** | N/A (producto) | Básico | Flujo de trabajo agente-humano sobre archivos reales |
| 12 | **Claude with Amazon Bedrock** | Python/TS | Medio | Si tu empresa usa AWS |
| 13 | **Claude on Google Cloud (Vertex AI)** | Python/TS | Medio | Si tu empresa usa GCP |

### Grupo B — Track "AI Fluency" (no técnico, opcional)
`AI Fluency: Framework & Foundations`, `AI Fluency for educators/students/nonprofits/small businesses/builders/creative work`, `Teaching AI Fluency`. Son cursos de criterio y gobernanza de uso de IA (no programación). **Recomendación**: solo el de "Framework & Foundations" (2h) al principio, como cultura general; el resto no aporta a tu objetivo de programación.

### Grupo C — No aplican a tu objetivo actual
Cursos específicos de audiencia no-developer (nonprofits, pK-12, creative work). Los excluyo del programa.

**Nota importante sobre Java**: Ninguno de los cursos de Skilljar usa Java — usan TypeScript o Python. Pero Anthropic mantiene un **SDK oficial en Java** (`com.anthropic:anthropic-java`, en GitHub `anthropics/anthropic-sdk-java`). Por eso el programa está diseñado así: **tú ves la lección en el lenguaje original (Python/TS), yo te implemento el proyecto de referencia en ese mismo lenguaje, y tu proyecto "sin implementar" lo construyes en Java** usando el SDK oficial — así consolidas el concepto Y mantienes/potencias tu perfil de arquitecto Java. En algunos bloques avanzados (RAG, agentes) el ejercicio en Java será de arquitectura/diseño (interfaces, patrones) más que de SDK 1:1, porque el SDK Java es más limitado que el de Python en utilidades de alto nivel.

---

## 2. Cómo vamos a trabajar cada lección (mecánica del programa)

Cada **bloque de aprendizaje** (agrupando 1-3 lecciones afines del curso original) sigue siempre esta estructura de 4 pasos:

1. **Tú ves el vídeo/lectura original en Skilljar** (yo no tengo acceso a reproducir el vídeo por ti; te indico exactamente qué lección ver).
2. **Yo te entrego el "proyecto implementado"**: código funcional, comentado, con README explicando el porqué de cada decisión — en el lenguaje del curso (Python o TS).
3. **Tú resuelves el "proyecto sin implementar"**: un enunciado con requisitos, sin código, normalmente en **Java** (o en Python cuando el bloque es puramente conceptual/prompting, ya que ahí Java no aporta).
4. **Cierre**: me pegas tu solución (o la subes) y te hago code review de arquitecto — comparando con buenas prácticas de Anthropic + patrones Java (SOLID, hexagonal, DDD si aplica).

### Qué herramienta usar para cada paso

| Paso | Herramienta recomendada | Por qué |
|------|--------------------------|---------|
| Ver el curso Skilljar | Navegador normal | Es contenido en vídeo, no se puede automatizar |
| Generar el proyecto **implementado** (yo te lo doy) | **Este chat (Claude.ai) con Code Execution/Artifacts**, o pídemelo y yo lo preparo aquí como archivos descargables | Proyectos pequeños/medios (1 curso = 1 script o mini-app), no necesitas un IDE agente para recibir algo ya hecho |
| Construir tú el proyecto **sin implementar** en Python (bloques 1-6) | **Claude Code** (terminal, VS Code o app de escritorio) | Es donde vas a *programar de verdad*, iterar, depurar, correr tests — exactamente el flujo real de un desarrollador. Ideal para practicar cómo se trabaja con un agente de código día a día (justo lo que enseña el curso "Claude Code in Action") |
| Construir tú el proyecto **sin implementar** en Java (arquitectura/servicios) | **Claude Code** también (mismo motivo) | Java + Maven/Gradle + tests → Claude Code es el entorno natural, no Cowork |
| Proyectos que combinan varios ficheros de negocio, documentos, hojas de cálculo o requieren investigar/comparar antes de construir (p. ej. el proyecto final de arquitectura, o preparar el "prompt eval dataset") | **Claude Cowork** | Cowork brilla en tareas multi-paso con muchos archivos/herramientas (investigación + redacción + generación de datasets), no tanto en escribir y depurar código línea a línea |
| Maquetas visuales de un dashboard/UI para el proyecto de agente (si en algún punto quieres un frontend bonito para demostrar tu agente) | **Claude Design** | Solo si en el módulo de "Managed Agents" o "RAG" decides construir una interfaz de demo; no es necesario para el grueso del programa |
| Dudas conceptuales, revisión de tu código, diseño de arquitectura, generación de los enunciados "sin implementar" | **Este chat (Claude.ai)** | Aquí seguimos el hilo pedagógico completo |

**Regla práctica**: si vas a *escribir y ejecutar código iterando*, usa **Claude Code**. Si vas a *investigar, comparar, redactar o coordinar varios documentos*, usa **Cowork**. Si necesitas *una vista/mock visual*, usa **Claude Design**. El resto (explicaciones, planificación, code review) lo hacemos aquí.

---

## 3. Estructura de tu repositorio de proyectos

```
ia-learning-path/
├── 00-fundamentos/              # Claude 101, AI Capabilities & Limitations, AI Fluency
├── 01-claude-platform-101-ts/   # proyectos en TypeScript
├── 02-claude-api-python/        # curso grande, un subcarpeta por sección
│   ├── 01-accessing-api/
│   ├── 02-prompt-evaluation/
│   ├── 03-prompt-engineering/
│   ├── 04-tool-use/
│   ├── 05-rag-agentic-search/
│   ├── 06-features-thinking-caching/
│   ├── 07-mcp/
│   └── 08-agents-workflows/
├── 03-mcp-intro-python/
├── 04-mcp-advanced-python/
├── 05-claude-code-workflow/      # ejercicios de CLAUDE.md, hooks, skills, subagents
├── 06-java-track/                # TODOS tus proyectos "sin implementar" en Java
│   ├── pom.xml (o build.gradle)
│   └── src/main/java/...
└── 07-proyecto-final-arquitectura/
```

Te sugiero repositorio único en Git desde el día 1: así Claude Code puede usar `CLAUDE.md` para "recordar" tus convenciones (paquetes Java, estilo, versión de Spring Boot, etc.) en cada sesión.

---

## 4. Programa de estudio detallado

### Fase 0 — Fundamentos (≈2-3h) — *Grupo A #1, #2, y B (Framework & Foundations)*

**Ver en Skilljar**: `Claude 101` → `AI Capabilities and Limitations` → `AI Fluency: Framework & Foundations`.

- **Proyecto implementado (te lo doy)**: un documento comparativo de 1 página — "Qué puede y no puede hacer Claude hoy, y qué implica para arquitectura de software" (mapa mental / tabla de decisión: cuándo usar IA generativa vs reglas de negocio deterministas).
- **Proyecto sin implementar (tú)**: escribe (en Markdown) un **ADR (Architecture Decision Record)** — a tu estilo de arquitecto — evaluando si un módulo real de tu empresa (elige uno: validación de documentos, atención al cliente, generación de informes) es candidato a IA generativa, y por qué. No hay código; es puramente analítico. Herramienta: este chat o Cowork si quieres investigar casos similares en la industria.

---

### Fase 1 — Claude Platform 101 (TypeScript) (≈3-4h) — *Grupo A #3*

**Ver en Skilljar**, en orden: *What is the Claude Platform → Your first API call → Choosing the right model → The agent loop explained → What is tool use? → What is thinking? → Built-in tools → Skills → MCP → Context management → Managed agents → Building with Claude Code*.

- **Proyecto implementado (te lo doy, en TypeScript/Node)**: un **agent loop manual** (sin SDK helpers) que llama a Claude, le da una tool de "consultar inventario simulado", procesa `tool_use`, le devuelve `tool_result`, y decide cuándo parar. Incluye comparación con la misma lógica usando el `Tool Runner` del SDK.
- **Proyecto sin implementar (tú, en Java)**: reimplementa el mismo agent loop usando el **SDK oficial `anthropic-java`**. Requisitos: (1) una tool `getStockPrice(ticker)` simulada, (2) manejo explícito de los bloques de mensaje (`text`, `tool_use`), (3) límite de 5 turnos máximo, (4) logs estructurados de cada decisión del agente. Esto es exactamente el tipo de "wrapper de agente" que un arquitecto Java construiría para exponer un servicio interno.

---

### Fase 2 — Building with the Claude API (Python) — el curso troncal (≈8-10h repartidas en varias sesiones) — *Grupo A #4*

Este es el curso más largo; lo trocearemos en 6 sub-bloques, cada uno con su propio par de proyectos.

#### 2.1 Acceso a la API, prompting básico y streaming
**Ver**: *Accessing the API → Getting an API key → Making a request → Multi-turn conversations → System prompts → Temperature → Response streaming → Structured data*.

- **Implementado (Python)**: chatbot de consola con historial multi-turno, system prompt configurable por archivo YAML, streaming de respuesta token a token, y salida estructurada (JSON Schema) para extraer "intención + entidades" de cada mensaje.
- **Sin implementar (Java)**: construye un servicio REST en **Spring Boot** con un endpoint `POST /chat` que mantenga sesión (in-memory o Redis), reenvíe a Claude con streaming (Server-Sent Events hacia el cliente), y valide la salida estructurada contra un DTO Java. Esto es un microservicio real de "chat backend".

#### 2.2 Evaluación de prompts (prompt evals)
**Ver**: *Prompt evaluation → typical eval workflow → generating test datasets → running the eval → model-based grading → code-based grading*.

- **Implementado (Python)**: pipeline de evals que genera 20 casos de prueba sintéticos, corre el prompt contra cada uno, y califica con dos métodos (grading por código para respuestas exactas, grading por modelo para respuestas abiertas), sacando un informe con % de acierto.
- **Sin implementar (Java, o Cowork para el dataset)**: diseña (en Java, con JUnit 5 + un cliente HTTP a Claude) una suite de "regression tests de prompts" que se pueda correr en tu pipeline de CI — es decir, tests automatizados que fallen si un cambio de prompt degrada la calidad. Usa Cowork si prefieres primero investigar/generar el dataset de 20-30 casos de negocio reales antes de picar el código.

#### 2.3 Prompt engineering
**Ver**: *Prompt engineering → being clear and direct → being specific → XML tags → providing examples*.

- **Implementado**: biblioteca de "prompt templates" reutilizables en Python (con Jinja2), documentando antes/después de cada técnica sobre un mismo caso de negocio (clasificación de tickets de soporte).
- **Sin implementar**: no requiere Java — es transversal. Tarea: reescribe 5 prompts que uses hoy en tu trabajo (o inventa 5 típicos de un backend Java: generación de commit messages, resumen de logs de excepción, explicación de un stack trace, generación de tests, revisión de PR) aplicando las 4 técnicas. Entrega en Markdown.

#### 2.4 Tool use (uso de herramientas)
**Ver**: *Introducing tool use → tool functions → tool schemas → handling message blocks → sending tool results → multi-turn with tools → multiple tools → fine-grained tool calling → text edit tool → web search tool*.

- **Implementado (Python)**: agente con 3 tools (calculadora, búsqueda en una "base de conocimiento" local, y el `text_editor` tool para modificar un archivo), con manejo completo del ciclo multi-turno.
- **Sin implementar (Java)**: diseña un agente Java que exponga como "tools" **3 servicios reales de tu dominio** (ej. `consultarPedido`, `calcularDescuento`, `generarFactura`) usando interfaces Java limpias detrás de cada tool, de forma que mañana puedas sustituir la implementación simulada por tus servicios de producción sin tocar la capa de integración con Claude. Este es el ejercicio más importante del programa para tu objetivo de arquitecto: separar "tool schema" de "lógica de negocio".

#### 2.5 RAG y búsqueda agéntica
**Ver**: *Introducing RAG → text chunking → embeddings → full RAG flow → implementing RAG → BM25 → multi-index RAG pipeline*.

- **Implementado (Python)**: pipeline RAG completo sobre un set de PDFs (chunking, embeddings, búsqueda vectorial + BM25 híbrido, generación de respuesta con citas).
- **Sin implementar (Java)**: arquitectura + implementación parcial en Java de un **RAG service**: define las interfaces (`DocumentChunker`, `EmbeddingClient`, `VectorStore`, `Retriever`), implementa el chunking y la orquestación en Java, y usa un vector store real u open-source con binding Java (p. ej. pgvector desde JDBC, o pinecone-client). El objetivo no es reinventar embeddings sino demostrar que sabes **diseñar la arquitectura de un sistema RAG productivo** en tu stack.

#### 2.6 Features avanzadas: thinking, imágenes, PDFs, citations, prompt caching
**Ver**: *Extended thinking → image support → PDF support → citations → prompt caching (reglas y en acción) → code execution y Files API*.

- **Implementado (Python)**: demo que procesa un PDF de factura, extrae datos con citations, usa extended thinking para casos ambiguos, y aplica prompt caching sobre el system prompt + documentos base para reducir coste/latencia.
- **Sin implementar (Java)**: implementa el **cliente Java** equivalente para el caso "procesar PDF + prompt caching", midiendo y logueando el ahorro de tokens en cache-hit vs cache-miss (esto es justo el tipo de métrica que un arquitecto reporta a negocio para justificar coste de IA).

---

### Fase 3 — Model Context Protocol: Intro + Avanzado (Python) (≈4-5h) — *Grupo A #5 y #6*

**Ver Intro to MCP**: *Introducing MCP → MCP clients → Project setup → Defining tools with MCP → Server inspector → Implementing a client → Defining resources → Accessing resources → Defining prompts*.
**Ver MCP Advanced**: *Sampling → Notifications (log/progress) → Roots → JSON message types → STDIO transport → StreamableHTTP transport (in depth) → State y HTTP*.

- **Implementado (Python)**: servidor MCP completo (tools + resources + prompts) para gestión documental, probado con el MCP Inspector, más un cliente que lo consume; en la parte avanzada, se añade sampling, notificaciones de progreso y transporte StreamableHTTP con estado.
- **Sin implementar (Java)**: construye un **servidor MCP en Java** (existe SDK oficial `mcp-java-sdk` de Spring AI / Anthropic) que exponga como tools 2-3 operaciones de un sistema típico empresarial (ej. consulta de tickets Jira simulada, consulta de estado de despliegue). Este proyecto es doblemente valioso: te prepara para el futuro cercano donde tu empresa probablemente querrá exponer *sus propios sistemas Java* a agentes de IA vía MCP — literalmente tu rol de arquitecto en 2026-2027.

---

### Fase 4 — Flujo de trabajo con Claude Code (≈4-5h) — *Grupo A #7, #8, #9, #10*

**Ver**: `Claude Code 101` → `Claude Code in Action` (*Steering long sessions → CLAUDE.md → Verification skills → Permission modes → Hooks → Routines/headless → GitHub Actions/code review → Verifying unsupervised runs → Plugins*) → `Introduction to agent skills` → `Introduction to subagents`.

- **Implementado (te lo muestro con capturas/config, no es "código" tradicional)**: un repo de ejemplo con `CLAUDE.md` bien escrito, 2 hooks (uno que corre tests antes de permitir un commit, otro que bloquea `rm -rf`), y 1 Skill personalizada (`SKILL.md`) para "generar changelog siguiendo Conventional Commits".
- **Sin implementar (tú, en tu propio repo Java del punto 3)**: (1) escribe tu propio `CLAUDE.md` para el repo `06-java-track` (convenciones, comandos de build/test, estilo), (2) crea un hook que impida terminar una sesión si `mvn test` falla, (3) crea una Skill Java-específica (ej. "generar un test JUnit siguiendo el patrón AAA para cualquier clase que te pase"), (4) crea un subagente especializado en "revisor de código Java" con permisos restringidos (solo lectura). Herramienta: **Claude Code obligatoriamente** — este bloque es sobre la herramienta en sí.

---

### Fase 5 — Introduction to Claude Cowork (≈1-2h) — *Grupo A #11*

**Ver**: el curso completo (es corto, un solo módulo).

- **Implementado**: te muestro un ejemplo de sesión Cowork donde se investiga 3 proveedores de vector DB, se compara en una tabla, y se redacta una recomendación — todo en un mismo hilo con archivos de salida.
- **Sin implementar (tú, en Cowork)**: usa Cowork para investigar y producir un **informe de arquitectura de 2-3 páginas** comparando 3 enfoques para integrar IA en tu sistema Java actual (por ejemplo: SDK directo vs pasar por un gateway/BFF vs usar Spring AI), con pros/contras, coste y riesgos. Esto es preparación directa para el proyecto final.

---

### Fase 6 (opcional, según tu infraestructura) — Bedrock o Vertex AI (≈2-3h) — *Grupo A #12/#13*

Solo si tu empresa usa AWS o GCP. Mismo patrón implementado/sin-implementar pero centrado en autenticación gestionada (IAM/roles) en vez de API key directa — muy relevante si eres tú quien decide la arquitectura de despliegue.

---

## 5. Proyecto final integrador (≈1-2 semanas)

**"Agente de arquitectura empresarial en Java"**: un servicio Spring Boot que:
1. Expone un endpoint de chat (Fase 2.1).
2. Usa tool use para invocar 3 servicios de negocio reales o simulados (Fase 2.4).
3. Tiene un componente RAG sobre tu documentación interna (Fase 2.5).
4. Se expone como servidor **MCP** para que Claude Code/Claude Desktop puedan usarlo directamente (Fase 3).
5. Tiene tests de regresión de prompts en CI (Fase 2.2) y un `CLAUDE.md`/hooks que gobiernan cómo se toca ese repo con IA (Fase 4).
6. Documentado con el informe de arquitectura hecho en Cowork (Fase 5).

Este proyecto es, en la práctica, tu **portfolio de transición**: sirve tanto si te quedas como arquitecto Java que lidera adopción de IA, como si decides moverte a un rol más puramente de IA.

---

## 6. Ritmo sugerido

| Semana | Fase |
|--------|------|
| 1 | Fase 0 + Fase 1 |
| 2-4 | Fase 2 (troceada en las 6 sub-fases, ~1 sub-fase cada 2-3 días) |
| 5 | Fase 3 |
| 6 | Fase 4 |
| 6 | Fase 5 |
| 7-8 | Proyecto final |

---

## 7. Cómo seguimos a partir de aquí

Dime **por qué fase quieres empezar** (recomiendo Fase 0) y en cada sesión te entrego:
- el **proyecto implementado** completo (código + explicación) directamente en el chat o como archivos descargables,
- el **enunciado** del proyecto sin implementar con criterios de aceptación claros,
- y cuando termines tu versión, hacemos code review juntos antes de pasar al siguiente bloque.
