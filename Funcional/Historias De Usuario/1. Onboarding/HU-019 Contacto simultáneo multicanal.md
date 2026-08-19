#### HU-019: Contacto multicanal

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero contactar a los clientes preaprobados mediante correo, WhatsApp y llamada, de acuerdo con la estrategia de contacto definida, para maximizar la tasa de respuesta. |
| **Prioridad** | Alta |
| **Precondiciones** | El asesor cuenta con la base de clientes preaprobados y con las plantillas de contacto por los tres canales. |
| **Criterios de aceptación** | El cliente recibe los contactos definidos a través de los canales establecidos (correo, WhatsApp y llamada), de acuerdo con la estrategia de contacto, y el equipo comercial puede registrar y consultar la tasa de respuesta por canal. |
| **Relaciones** | Casos de uso: CU-001. Requerimiento: RF-001. Historia relacionada: HU-001. |
| **Referencias** |  `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | v1.7 |
| **Comentarios** | **Corrección v1.7:** se elimina el término “simultáneamente”, ya que los contactos por los diferentes canales no se realizan en el mismo instante de tiempo. La historia se ajusta para describir una estrategia de contacto multicanal sin asumir simultaneidad ni un orden específico entre los canales. |
