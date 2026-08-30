# Fase 0 — Fundamentos

Qué se practica: fundamentos de qué puede y qué no puede hacer un LLM, para diseñar arquitecturas realistas. Sin código; entregables puramente analíticos (Markdown).

## Cursos Skilljar de referencia

- `Claude 101`
- `AI Capabilities and Limitations`
- `AI Fluency: Framework & Foundations`

## Entregables

Los documentos viven en [`../docs/`](../docs/) (fuente de verdad de enunciados y material de cada fase):

| Entregable | Archivo | Estado |
|---|---|---|
| Proyecto implementado (referencia) — guía de decisión "qué puede / no puede hacer Claude" y su implicación para arquitectura | [`../docs/fase0-que-puede-y-no-puede-hacer-claude.md`](../docs/fase0-que-puede-y-no-puede-hacer-claude.md) | ✅ Hecho |
| Proyecto sin implementar (mío) — **ADR-001**: adoptar un asistente de IA para apoyar la elaboración de diseños técnicos, con evaluación de por qué el módulo es candidato a IA generativa | [`../docs/fase0-adr-asistente-ia-diseno-tecnico.md`](../docs/fase0-adr-asistente-ia-diseno-tecnico.md) | ✅ Hecho |

Nota: el programa proponía elegir entre "validación de documentos / atención al cliente / generación de informes". Se sustituyó por un módulo real propio (proceso análisis funcional → diseño técnico), manteniendo el objetivo del ejercicio: un ADR analítico que razona si el módulo es candidato a IA generativa y con qué diseño.

## Cómo revisarlo

No hay build ni tests. Abrir los dos `.md` de `docs/` en un visor Markdown con soporte Mermaid (GitHub los renderiza) para ver los diagramas del ADR.

## Estado de la fase

**Cerrada** una vez vistos los 3 cursos de Skilljar y con los dos entregables anteriores en `docs/`.