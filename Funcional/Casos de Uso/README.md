# Casos de Uso — Fliipa

| Documento | Casos de Uso |
|:---:|:---:|
| **Proyecto** | Fliipa |
| **Versión** | 1.0 |
| **Estado** | En revisión |
| **Responsable** | Producto y negocio |
| **Basado en** | Historias de Usuario — Fliipa, v1.7 (`Funcional/Historias De Usuario`) |

---

## Objetivo

Describir, a nivel de interacción funcional entre actores y sistema, los flujos que soportan las historias de usuario de Fliipa: actores involucrados, precondiciones, flujo principal, flujos alternativos/excepciones, postcondiciones y reglas de negocio. Este documento agrupa las historias de usuario (HU-XXX) en casos de uso (CU-XXX) de mayor granularidad, siguiendo la misma organización por capítulo/vertical de servicio que el documento de Historias de Usuario.

## Alcance y metodología

- Se conservó la carpeta y el capítulo de cada HU de origen (Onboarding, KYC, Crédito, Cobranza, Servicio al Cliente, Gestión Plataforma del admin).
- Cuando una HU ya referenciaba un número de caso de uso (campo "Relaciones" de la ficha HU), se usó ese mismo número (CU-001 a CU-018).
- Cuando una o más HU no tenían un CU asignado en el documento fuente (HU-007, HU-008, HU-018, HU-027, HU-030, HU-040, HU-041, HU-042, HU-043, HU-044), se creó un caso de uso nuevo con el siguiente consecutivo disponible (CU-019 a CU-025), indicándolo explícitamente en una nota dentro de la ficha.
- El "Estado en plataforma" y los hallazgos técnicos de cada CU se heredan directamente de los comentarios de las HU de origen; no se reinterpretaron ni se dieron por hechos adicionales.

## Índice de capítulos

Cada carpeta incluye, además de las fichas CU-XXX:
- Un archivo `Diagrama de Casos de Uso.md` con el diagrama **consolidado del capítulo** (todos los casos de uso y actores del capítulo en un solo diagrama), en formato `.svg`.
- Dentro de **cada ficha CU-XXX individual**, un diagrama propio (`diagrama_CU-XXX.svg`) que muestra únicamente ese caso de uso con sus actores, embebido justo debajo del título de la ficha.

**Cobertura verificada (2026-08-19):** las 24 fichas CU-XXX de este catálogo cubren, en conjunto, las 43 historias de usuario que existen físicamente en el repositorio `documentacion_fliipa` (HU-001 a HU-044, sin HU-021, que no tiene ficha en el repositorio de origen — ver hallazgo del propio README de Historias de Usuario). No falta ninguna historia por cubrir.

> **Hallazgo pendiente de confirmar con negocio:** las fichas HU-007 y HU-008 del repositorio de origen (v1.7) declaran pertenecer a CU-005 y CU-006 respectivamente, pero esos números ya están usados en este catálogo para flujos de un actor distinto (Analista de riesgo). Ver la nota dentro de CU-005, CU-006 y CU-019 para el detalle.

| Capítulo | Carpeta | Casos de uso que contiene |
|:---|:---|:---|
| Onboarding | `1. Onboarding/` | CU-001, CU-002, CU-003 |
| KYC | `2. KYC/` | CU-004, CU-005, CU-006, CU-007, CU-019, CU-020 |
| Crédito | `3. Credito/` | CU-009, CU-010 |
| Cobranza | `4. Cobranza/` | CU-011, CU-012, CU-013, CU-021 |
| Servicio al Cliente | `5. Servicio al Cliente/` | CU-014, CU-022, CU-023 |
| Gestión Plataforma del admin | `6. Gestión Plataforma del admin/` | CU-015, CU-016, CU-017, CU-018, CU-024, CU-025 |

## Tabla de correspondencia Historias de Usuario → Casos de Uso

| Caso de uso | Título | Historias de usuario cubiertas |
|:---:|:---|:---|
| CU-001 | Iniciar contacto y solicitud de crédito | HU-001, HU-019, HU-020 |
| CU-002 | Consultar y ver cupo preaprobado | HU-001, HU-002, HU-003 |
| CU-003 | Confirmar identidad mediante OTP | HU-004, HU-005 |
| CU-004 | Completar validación biométrica | HU-006 |
| CU-005 | Revisar manualmente casos de biometría en revisión | HU-022 |
| CU-006 | Consultar análisis de KYC y evaluación de crédito | HU-023, HU-038, HU-039 |
| CU-007 | Firmar contrato mediante firma digital | HU-009 |
| CU-009 | Consultar cupo, plan de pagos y disponibilidad de crédito | HU-010, HU-011 |
| CU-010 | Usar el cupo en tienda D1 | HU-012 |
| CU-011 | Pagar y gestionar cuotas del crédito | HU-013, HU-014 |
| CU-012 | Gestionar y registrar cartera y cobranza | HU-024, HU-025, HU-026 |
| CU-013 | Recibir alivios ante dificultades de pago | HU-015 |
| CU-014 | Atender al cliente por IA y escalar a agente humano | HU-016, HU-017, HU-028, HU-029 |
| CU-015 | Buscar cliente, ver historial auditado y ajustar cupo o fecha de corte | HU-031, HU-032 |
| CU-016 | Simular plan de pago con distintas tasas | HU-033 |
| CU-017 | Administrar y consultar clientes en blacklist | HU-034, HU-035 |
| CU-018 | Monitorear salud del sistema en tiempo real | HU-036 |
| CU-019 *(nuevo)* | Cargar soportes bancarios y conocer el resultado | HU-007, HU-008, HU-037 |
| CU-020 *(nuevo)* | Motor KYC automático post-solicitud | HU-042, HU-043, HU-044 |
| CU-021 *(nuevo)* | Escalar casos a cobro jurídico | HU-027 |
| CU-022 *(nuevo)* | Recuperar PIN o desbloquear la cuenta | HU-018 |
| CU-023 *(nuevo)* | Registrar cada contacto con el cliente | HU-030 |
| CU-024 *(nuevo)* | Ver y reconectar la cuenta Druo del cliente | HU-040 |
| CU-025 *(nuevo)* | Cambiar el estado del crédito manualmente (incluye pre-rechazado) | HU-041 |

## Hallazgos pendientes

1. **HU-007 y HU-008 están vacías** en el repositorio de Historias de Usuario (sin ficha de contenido, solo el encabezado del archivo). El caso de uso CU-019 se construyó a partir de las referencias cruzadas que otras historias (HU-006, HU-011, HU-030, HU-037) hacen sobre ellas; se recomienda completar esas dos fichas en el documento fuente para cerrar la trazabilidad.
2. Varios casos de uso heredan de sus HU de origen funcionalidad **no implementada o solo parcialmente implementada** en el código revisado (biometría, revisión manual de biometría, PSE, débito automático de punta a punta, alivios/buckets de mora, tablero del Comité de Cartera, escalamiento jurídico automático, IA conversacional, blacklist consultable en admin). Esto se señala explícitamente en el campo "Estado en plataforma" de cada ficha, siguiendo la misma evidencia documentada en las Historias de Usuario.
3. Los casos de uso CU-019 a CU-025 son de numeración nueva, propuesta en este ejercicio de documentación; se recomienda validarlos con negocio antes de considerarlos definitivos.

## Fuentes consultadas

- Repositorio `MariaFer2006/documentacion_fliipa`, carpeta `Funcional/Historias De Usuario` (44 fichas HU-001 a HU-044 y su README).
