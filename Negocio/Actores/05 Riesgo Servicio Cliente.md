# 5. Actores de riesgo y servicio al cliente

[← Volver a Actores](README.md)

| Actor | Rol | Fuente |
|---|---|---|
| Analista de riesgo | Resuelve manualmente los casos de biometría que quedan "en revisión" durante el KYC (Journey Colpatria B2B, pág. 3). La evaluación de score/cupo vía Experian ya es 100% automática ("se elimina el estudio manual del analista" en ese paso, pág. 4); el rol manual queda acotado a los casos de biometría en revisión, no a la decisión de crédito en general. | Journeys Colpatria B2B |
| Asistente virtual (IA) | *(largo plazo)* Atiende el primer nivel de servicio al cliente (WhatsApp, correo, llamada), clasifica el caso e intenta resolverlo en el primer contacto. | Journeys Colpatria B2B |
| Agente humano de servicio al cliente | Recibe el caso con contexto cuando la IA no lo resuelve; valida identidad y aprueba manualmente los casos críticos (suplantación, uso indebido del cupo, desconocimiento de compra), y decide el enrutamiento final: resolución autónoma, escalación a un área (riesgo, cobranza, TI) o Legal/PQR. | Journeys Colpatria B2B, pág. 9 |
| Áreas internas de escalamiento (riesgo, cobranza, TI) | Reciben los casos estándar de servicio al cliente que el agente humano escala y los analizan según su especialidad. | Journeys Colpatria B2B, pág. 9 |
| Área Legal/PQR | Recibe los casos legales o de PQR (tutela, derecho de petición) enrutados por el agente, con SLA de respuesta inmediata. | Journeys Colpatria B2B, pág. 9 |

Ver el detalle completo del flujo de enrutamiento en [Procesos → 11. Servicio al cliente](../procesos/11-servicio-cliente.md).

## Fuentes consultadas

- `Journeys Fran finales.pdf` (Journeys Colpatria B2B, junio 2026), páginas 3, 4 y 9
