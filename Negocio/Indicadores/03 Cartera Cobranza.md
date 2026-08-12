# 3. Indicadores de cartera y cobranza

[← Volver a Indicadores](README.md)

**Horizonte:** Evolución

## Qué se mide en cada bucket

```mermaid
flowchart LR
    PA["Pago anticipado"] --> B1["Bucket 1 · 1-30 días"]
    B1 --> B2["Bucket 2 · 31-60 días"]
    B2 --> B3["Bucket 3 · 61-90 días"]
    B3 --> B4["Bucket 4 · 91-120 días"]
    B4 --> B5["Bucket 5 · 120+ días"]
    B5 --> J["Castigo de cartera"]
```

En cada bucket se hace seguimiento a: % de cartera en ese bucket (monto y volumen), tasa de recuperación, cumplimiento de acuerdos de pago y % de casos escalados al siguiente bucket.

## Indicadores

- Distribución de la cartera por bucket de mora (pago anticipado, bucket 1 a 5), en porcentaje y en monto.
- Tasa de mora y cartera en riesgo (PAR).
- Tasa de recuperación por bucket y por tipo de alivio otorgado (abono parcial, congelamiento de intereses, condonación).
- % de clientes reportados negativamente a centrales de riesgo.
- % de casos escalados a proceso jurídico y tasa de recuperación en esa etapa.
- % de castigo de cartera.
- Cumplimiento de compromisos y acuerdos de pago (promesas cumplidas vs. incumplidas).
- Casos priorizados por el Comité de Cartera y motivo de priorización (días de mora, cuotas vencidas, monto adeudado).

## Fuentes consultadas

- Modelo y Proceso de Cobranza B2B — *Modelo Cobranza/Modelo_de_Cobranza_B2B_.pptx* y *Modelo Cobranza/Modelo y gestion de cobranza.docx*
- Reglas Negocio (`negocio/reglas-negocio/02-mora-buckets.md`)
- Procesos — [09. Gestión de cobranza por bucket de mora](../procesos/09-cobranza.md)
