#### HU-016: Atención inicial por asistente virtual con IA
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que un asistente virtual con inteligencia artificial atienda mi primer contacto por WhatsApp, para obtener respuesta inmediata a mis dudas más comunes. |
| **Prioridad** | Bajo |
| **Criterios de aceptación** | El asistente virtual con IA recibe y responde el primer contacto del cliente por WhatsApp, dentro de las dudas frecuentes definidas en su alcance. |
| **Relaciones** | Casos de uso: [CU-014](../../Casos de Uso/5. Servicio al Cliente/CU-014 Atender al cliente por IA y escalar a agente humano.md). Requerimiento: [RF-028](../../Requerimientos/Requerimientos Funcionales.md). Historia relacionada: [HU-017](../6. Servicio al Cliente/HU-017 Escalar a agente humano cuando la IA no resuelve el caso.md). |
| **Referencias** | [Atención al cliente](../../../Operaciones/Procesos/06 Servicio Cliente.md); `b2b/services/communications/src/controllers/whatsapp/whatsapp.controller.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Historia separada de la HU-011 original (v1.5)**, que combinaba el flujo de atención por IA con el flujo de escalamiento a un agente humano; deben documentarse por separado para no interferir con los procesos ya definidos de servicio al cliente y de la operación. No se encontró en el código revisado ningún módulo de asistente conversacional de IA ni lógica de escalamiento; los controladores del microservicio `communications` están limitados a envío de OTP, firma y contrato por WhatsApp/correo. Probablemente vive en una herramienta externa no incluida en este repositorio. |
