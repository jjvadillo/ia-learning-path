# Qué puede y no puede hacer Claude — guía de decisión para arquitectura

> Proyecto implementado — Fase 0. Referencia para decidir cuándo un módulo de software es candidato a IA generativa y cuándo debe seguir siendo lógica determinista.

## 1. Capacidades reales (lo que Claude hace bien)

| Capacidad | Qué significa en términos de arquitectura |
|---|---|
| Comprensión y generación de lenguaje natural | Ideal para interfaces conversacionales, resumen, clasificación de texto libre, generación de documentación |
| Razonamiento en contexto (no memoriza tu dominio) | Todo lo que Claude "sabe" de tu negocio debe dársele en el prompt, en una tool, o vía RAG/MCP en cada llamada — no hay estado propio entre peticiones |
| Uso de herramientas (tool use) | Puede decidir *cuándo* llamar a un servicio tuyo, pero la ejecución y la verdad de los datos siguen siendo responsabilidad de tu sistema |
| Seguir instrucciones estructuradas (system prompts, XML, JSON schema) | Se puede integrar como componente de un pipeline con contratos de entrada/salida bien definidos |
| Multimodalidad (imágenes, PDFs) | Útil para extracción de datos de documentos no estructurados (facturas, contratos) |
| Extended thinking para problemas ambiguos | Mejora decisiones en casos con múltiples interpretaciones válidas, no en cálculos que requieren exactitud garantizada |

## 2. Limitaciones reales (lo que NO debes pedirle)

| Limitación | Implicación de diseño |
|---|---|
| No hay garantía de determinismo | Nunca uses el modelo como única fuente de verdad para reglas de negocio críticas (cálculo de impuestos, validación legal, importes) |
| Ventana de contexto finita | Sistemas con mucho histórico/documentación necesitan RAG o resumido progresivo, no "meterlo todo en el prompt" |
| Puede alucinar datos | Toda salida que afecte a una decisión de negocio debe ser verificable (citations, validación contra la fuente real) |
| Coste y latencia por token | No es gratis escalar; hay que diseñar con caching, elección de modelo (Haiku/Sonnet/Opus) y límites de uso |
| No ejecuta código de forma nativa fuera del sandbox que tú le des | La "acción sobre el mundo real" siempre pasa por tools que tú controlas y auditas |
| Conocimiento de mundo con fecha de corte | Para hechos recientes necesita herramientas de búsqueda o datos que tú le proporciones |

## 3. Tabla de decisión rápida

| Si el módulo requiere... | Entonces... |
|---|---|
| Cálculo exacto y auditable (nóminas, impuestos, saldos) | **No** uses IA generativa como motor; puede ayudar a *explicar* el resultado, no a calcularlo |
| Interpretar texto libre / lenguaje natural de usuarios | **Sí**, buen candidato (soporte, clasificación, extracción) |
| Tomar una decisión de negocio de alto impacto sin supervisión humana | **No** de forma autónoma; sí como asistente con humano en el loop |
| Consultar/combinar información dispersa en documentos | **Sí**, vía RAG, con citations obligatorias |
| Ejecutar acciones sobre sistemas de producción (borrar, pagar, desplegar) | **Sí**, pero solo detrás de una tool con permisos explícitos y logging — nunca acceso directo |
| Generar código, tests, documentación | **Sí**, con revisión humana antes de merge |

## 4. Cómo usar esto como arquitecto

1. Identifica el módulo candidato.
2. Clasifícalo con la tabla del punto 3.
3. Si es candidato: decide el patrón (chat directo, tool use, RAG, agente con MCP) — lo iremos viendo en las siguientes fases.
4. Si no es candidato puro pero tiene una parte "blanda" (ej. cálculo determinista + explicación en lenguaje natural del resultado): separa las dos responsabilidades en dos componentes distintos.
