# HU-008: Conocer el resultado en máximo 24 horas

| Campo | Detalle |
|:---:|:---|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero conocer el resultado de mi solicitud en un plazo máximo de 24 horas, para poder planear mis compras en D1. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente debe recibir una notificación informándole si su solicitud fue **aprobada o rechazada** en un plazo máximo de 24 horas después de completar las etapas requeridas del proceso. La notificación del resultado debe enviarse mediante los canales de comunicación definidos para el cliente, incluyendo **correo electrónico**. En caso de rechazo, la notificación no debe exponer información técnica ni información sensible del proceso de evaluación. |
| **Relaciones** | Casos de uso: CU-006. Requerimientos: RF-010, RF-011, RF-012. Historias relacionadas: HU-006, HU-007. |
| **Referencias** | Procesos; `b2b/services/evaluations/src/third-party/Experian/authentication-experian.ts`, `midecisorpj.ts`, `reconocer.ts`; `b2b/fliipa-back/src/controllers/institutions/get-advance-score.ts`. |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | v.1.8 |
| **Comentarios** | **Corrección funcional:** se especifica que el cliente debe recibir una notificación con el resultado de su solicitud, indicando si fue **aprobada o rechazada**, y que el **correo electrónico** es uno de los canales definidos para comunicar dicho resultado. **Consideración técnica:** la evidencia revisada confirma consultas contra Experian mediante el microservicio `b2b/services/evaluations` y el uso de `get-advance-score.ts` como proxy. No se encontró un job o temporizador que garantice técnicamente el SLA de 24 horas; por lo tanto, este plazo se mantiene como compromiso operativo/de negocio y no como una regla actualmente codificada. La referencia a Datacrédito debe mantenerse con cautela, ya que la evidencia revisada no permite concluir que corresponda a un segundo buró independiente utilizado en paralelo con Experian. |