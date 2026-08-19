#### HU-008: Conocer el resultado en máximo 24 horas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero conocer el resultado de mi solicitud en máximo 24 horas, para poder planear mis compras en D1. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe notificación de aprobación o rechazo en alguno de los canales de comunicación dentro de las 24 horas siguientes a completar la validación de identidad, la biometría y la carga de soportes bancarios. |
| **Relaciones** | Casos de uso: [CU-006](../../Casos%20de%20Uso/2.%20KYC/CU-006%20Consultar%20analisis%20de%20KYC%20y%20evaluaci%C3%B3n%20de%20credito.md). Requerimientos:[RF-010](../../Requerimientos/Requerimientos%20Funcionales.md),[RF-011](../../Requerimientos/Requerimientos%20Funcionales.md), [RF-012](../../Requerimientos/Requerimientos%20Funcionales.md). Historias relacionadas: [HU-006](../2.%20KYC/HU-006%20Completar%20la%20validaci%C3%B3n%20biom%C3%A9trica%20(KYC).md), [HU-007](../2.%20KYC/HU-007%20Cargar%20soportes%20bancarios.md).. |
| **Referencias** | [Procesos](../../../Operaciones/Procesos/07%20Modelo%20Cobranza.md); `b2b/services/evaluations/src/third-party/Experian/authentication-experian.ts`, `midecisorpj.ts`, `reconocer.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | v.1.7 |
| **Comentarios** | **Confirmada** en el microservicio `b2b/services/evaluations`, que autentica contra Experian y consulta el score (`midecisorpj`) y la identidad (`reconocer`). El controlador `b2b/fliipa-back/src/controllers/institutions/get-advance-score.ts` actúa como proxy hacia ese microservicio vía `evaluationsClient`. La referencia a **Datacrédito** debe interpretarse con cautela: la evidencia revisada no permite concluir que corresponda a un segundo buró independiente utilizado en paralelo con Experian. No se encontró un job o temporizador que garantice el SLA de 24 horas; ese plazo parece ser un compromiso operativo/de negocio, no una regla codificada. |

