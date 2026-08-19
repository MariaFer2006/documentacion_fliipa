#### HU-039 — Ver coincidencias entre Fliipa y Reconocer
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo / administrador |
| **Historia** | Como analista de riesgo, quiero ver si el correo, celulares y direcciones del cliente (y del representante legal, si aplica) coinciden con lo reportado en Reconocer, para validar contacto de forma visual y rápida. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Sobre el resultado de Reconocer (HU-038): si **coincide**, se indica y se **resalta** la fila que hace match, mostrando contra qué registro coincidió (cliente o representante). Si el dato de Fliipa **no aparece** en centrales, se indica. Si en Fliipa no hay dato para comparar, se muestra "sin dato en registro". Si la sección no trae información de centrales, se muestra sin datos. La información se organiza en acordeones (correos, celulares, direcciones, etc.). |
| **Relaciones** | Depende de [HU-038](../5.%20Gesti%C3%B3n%20Plataforma%20del%20admin/HU-038%20Consultar%20informaci%C3%B3n%20de%20centrales.md). Distinta de la regla automática de contacto en [HU-043](../2.%20KYC/HU-043%20Evaluar%20reglas%20KYC.md). |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Estado en plataforma** | **Hecho.** |
| **Comentarios** | Asistencia visual al analista; no es la decisión automática del motor KYC. |


