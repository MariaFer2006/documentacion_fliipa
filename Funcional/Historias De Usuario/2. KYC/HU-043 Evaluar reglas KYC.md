#### HU-043 — Evaluar las reglas KYC y guardar el resultado de cada una
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero evaluar las cuatro reglas duras de KYC y guardar el resultado de cada una (con contraste onboarding vs consultado), para soporte y trazabilidad. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Se evalúan siempre: representante/identidad; Colpatria; Reconocer (contacto); cuenta bancaria vs centrales. Cada regla deja outcome y, si aplica, causal y comparación lado a lado. Fallas de "no cumple" se distinguen de "servicio de centrales caído". |
| **Relaciones** | HU-038 / HU-039 (consulta y match **manual** en admin); HU-042; HU-044. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **En desarrollo.** Las 4 reglas ya corren en el motor con comparación; se está completando persistir la corrida/expediente por cliente y usarla en el flujo automático. |
| **Comentarios** | La regla de cuenta compara onboarding vs centrales; no es validar el PDF ni Olimpia. El match visual de Reconocer en admin (HU-039) no es esta regla automática. |
