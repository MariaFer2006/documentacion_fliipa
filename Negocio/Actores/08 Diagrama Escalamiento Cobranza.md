# 8. Diagrama: escalamiento de cobranza por bucket

[← Volver a Actores](README.md)

```mermaid
flowchart LR
    PA["Pago anticipado<br/>Asesor comercial / Hunter"] --> B1["Bucket 1 · 1-30 días<br/>Analista de cartera"]
    B1 --> B2["Bucket 2 · 31-60 días<br/>Analista de cartera + Comité de Cartera"]
    B2 --> B3["Bucket 3 · 61-90 días<br/>Preaviso jurídico (Analista de cartera)"]
    B3 --> B4["Bucket 4 · 91-120 días<br/>Analista jurídico / Abogado"]
    B4 --> B5["Bucket 5 · 120+ días<br/>Comité Legal (demanda)"]
```

> Ver la nota de consistencia sobre los plazos de escalamiento jurídico frente al journey Colpatria en [04-comite-cartera.md](04-comite-cartera.md) y en [Procesos → 9. Gestión de cobranza](../procesos/09-cobranza.md).

## Fuentes consultadas

- Modelo y Proceso de Cobranza B2B
