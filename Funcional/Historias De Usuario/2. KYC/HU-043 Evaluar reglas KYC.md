#### HU-043 — Evaluar las reglas KYC y guardar el resultado de cada una
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero evaluar las cuatro reglas duras de KYC y guardar el resultado de cada una (con contraste onboarding vs consultado), para soporte y trazabilidad. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Se evalúan siempre: representante/identidad; Colpatria; Reconocer (contacto); cuenta bancaria vs centrales. Cada regla deja outcome y, si aplica, causal y comparación lado a lado. Fallas de "no cumple" se distinguen de "servicio de centrales caído". |
| **Relaciones** | [HU-038](../../../5.%20Gesti%C3%B3n%20Plataforma%20del%20admin/HU-038%20Consultar%20informaci%C3%B3n%20de%20centrales.md),
[HU-039](..//Funcional/Historias%20De%20Usuario/5.%20Gesti%C3%B3n%20Plataforma%20del%20admin/HU-039%20%20Ver%20coincidencias%20entre%20Fliipa%20y%20Reconocer.md) (consulta y match **manual** en admin); [HU-042](../2.%20KYC/HU-042%20%20Iniciar%20la%20evaluaci%C3%B3n%20KYC%20al%20quedar%20la%20solicitud%20en%20REQUESTED.md).
[HU-044](../2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md).. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **En desarrollo.** Las 4 reglas ya corren en el motor con comparación; se está completando persistir la corrida/expediente por cliente y usarla en el flujo automático. |
| **Comentarios** | La regla de cuenta compara onboarding vs centrales; no es validar el PDF ni Olimpia. El match visual de Reconocer en admin (HU-039) no es esta regla automática. |

