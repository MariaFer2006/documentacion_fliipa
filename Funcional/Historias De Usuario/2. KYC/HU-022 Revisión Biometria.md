#### HU-022: Resolver manualmente casos de biometría en revisión

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero revisar manualmente los casos de biometría marcados "en revisión", para decidir si el cliente puede continuar el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista visualiza los casos "en revisión" y registra la decisión (continuar o rechazar). |
| **Relaciones** | Casos de uso: [CU-005](../../Casos de Uso/2. KYC/CU-005 Revisar manualmente casos de biometria en revision.md). Historias relacionadas: [HU-006](../1. Onboarding/HU-006%20Completar%20la%20validaci%C3%B3n%20biom%C3%A9trica%20%28KYC%29.md), [HU-046](../2. KYC/HU-046 Manejo de rechazo en biometr�a.md). |
| **Referencias** | [Procesos](../../../Operaciones/Procesos/07 Modelo Cobranza.md); |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | No se encontró en el código ningún estado de "en revisión" para biometría, ni una cola o pantalla de revisión manual (se buscó "en_revision", "manual_review", "under_review" en todo el repositorio, sin coincidencias). Esta historia no tiene respaldo verificable en el código fuente entregado; se recomienda confirmar si el flujo de biometría vive en un sistema externo (proveedor de biometría) no incluido en este repositorio. |