#### HU-008: Conocer el resultado en máximo 24 horas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero conocer el resultado de mi solicitud en máximo 24 horas, para poder planear mis compras en D1. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe notificación de aprobación o rechazo dentro de las 24 horas siguientes a completar la validación de identidad, la biometría y la carga de soportes bancarios. |
| **Relaciones** | Casos de uso: CU-006. Requerimientos: RF-010, RF-011, RF-012. Historias relacionadas: HU-006, HU-007. |
| **Referencias** | [Procesos](../../../Operaciones/Procesos/07%20Modelo%20Cobranza.md); `b2b/services/evaluations/src/third-party/Experian/authentication-experian.ts`, `midecisorpj.ts`, `reconocer.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | v.1.7 |
| **Comentarios** | **Confirmada** en el microservicio `b2b/services/evaluations`, que autentica contra Experian y consulta el score (`midecisorpj`) y la identidad (`reconocer`). El controlador `b2b/fliipa-back/src/controllers/institutions/get-advance-score.ts` actúa como proxy hacia ese microservicio vía `evaluationsClient`. La referencia a **Datacrédito** debe interpretarse con cautela: la evidencia revisada no permite concluir que corresponda a un segundo buró independiente utilizado en paralelo con Experian. No se encontró un job o temporizador que garantice el SLA de 24 horas; ese plazo parece ser un compromiso operativo/de negocio, no una regla codificada. |
