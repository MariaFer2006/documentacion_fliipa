#### HU-016: Atención inicial por asistente virtual con IA
| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que un asistente virtual con inteligencia artificial atienda mi primer contacto por WhatsApp, para obtener respuesta inmediata a mis dudas más comunes. |
| **Prioridad** | Bajo |
| **Criterios de aceptación** | El asistente virtual con IA recibe y responde el primer contacto del cliente por WhatsApp, dentro de las dudas frecuentes definidas en su alcance. |
| **Relaciones** | Casos de uso: [CU-014](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md). Requerimiento: [RF-028](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-017](../6.%20Servicio%20al%20Cliente/HU-017%20Escalar%20a%20agente%20humano%20cuando%20la%20IA%20no%20resuelve%20el%20caso.md). |
| **Referencias** | [Atención al cliente](../../../Operaciones/Procesos/06%20Servicio%20Cliente.md); `b2b/services/communications/src/controllers/whatsapp/whatsapp.controller.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Historia separada de la HU-011 original (v1.5)**, que combinaba el flujo de atención por IA con el flujo de escalamiento a un agente humano; deben documentarse por separado para no interferir con los procesos ya definidos de servicio al cliente y de la operación. No se encontró en el código revisado ningún módulo de asistente conversacional de IA ni lógica de escalamiento; los controladores del microservicio `communications` están limitados a envío de OTP, firma y contrato por WhatsApp/correo. Probablemente vive en una herramienta externa no incluida en este repositorio. |
