# 7. Reglas de KYC y evaluación de riesgo

[← Volver a Reglas Negocio](README.md)

- La validación de identidad (KYC) es automática: se apoya en un proveedor externo de biometría (Olimpia), en la consulta a Experian y en el histórico transaccional de D1.
- Si el resultado de la biometría queda "en revisión", un analista de riesgo resuelve el caso manualmente; si es rechazado, el proceso termina y se notifica al cliente.
- La evaluación de riesgo valida automáticamente el score mínimo, la capacidad de endeudamiento y que la tienda habitual declarada coincida con la registrada en el histórico de D1.
- Cualquier validación fallida (cuenta bancaria inválida, score insuficiente, inconsistencia de datos) termina en rechazo automático de la solicitud.
- Colpatria es responsable de definir las políticas y reglas de originación que alimentan este motor de riesgo (ver [Actores — Proveedores externos](../Actores/06-proveedores-externos.md)).

## Fuentes consultadas

- Journeys Colpatria B2B, junio 2026 — *Journeys Fran finales-1.pdf*
- Modelo y Proceso de Cobranza B2B — *Modelo Cobranza/Modelo_de_Cobranza_B2B_.pptx*
