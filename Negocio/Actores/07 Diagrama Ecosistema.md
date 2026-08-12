# 7. Diagrama: ecosistema de actores

[← Volver a Actores](README.md)

```mermaid
graph TD
    subgraph Estrategico["Nivel estratégico"]
        GSD["Grupo Santo Domingo"]
        SUMZ["Sumz"]
    end

    subgraph Comercial["Canal y captación comercial (digital)"]
        D1["D1"]
        ASESOR["Asesor de servicio al cliente<br/>(canales digitales)"]
    end

    CLIENTE["Cliente empresarial"]
    FLIIPA["Fliipa"]

    subgraph RiesgoKYC["Riesgo y cumplimiento"]
        RIESGO["Analista de riesgo"]
        EXPERIAN["Experian"]
        OLIMPIA["Olimpia"]
    end

    subgraph Cobranza["Cobranza y jurídico"]
        CARTERA["Analista de cartera"]
        LIDER["Líder de Cartera"]
        COMCARTERA["Comité de Cartera"]
        JURIDICO["Analista jurídico / Representante Jurídico"]
        COMLEGAL["Comité Legal"]
    end

    subgraph SAC["Servicio al cliente"]
        IA["Asistente virtual IA"]
        AGENTE["Agente humano SAC"]
        LEGALPQR["Área Legal / PQR"]
    end

    subgraph Fondeo["Fondeo y pagos"]
        COLPATRIA["Colpatria"]
        DRUO["Druo"]
    end

    subgraph Notif["Notificaciones"]
        ZENVIA["Zenvia"]
        SENDGRID["Sendgrid"]
    end

    GSD --> SUMZ --> FLIIPA
    D1 --> CLIENTE
    ASESOR --> CLIENTE
    CLIENTE --> RIESGO
    RIESGO --> EXPERIAN
    RIESGO --> OLIMPIA
    RIESGO --> FLIIPA
    FLIIPA --> CARTERA
    CARTERA --> LIDER --> COMCARTERA
    COMCARTERA --> JURIDICO --> COMLEGAL
    CLIENTE --> IA --> AGENTE --> LEGALPQR
    COLPATRIA --> CLIENTE
    DRUO --> CLIENTE
    ZENVIA --> CLIENTE
    SENDGRID --> CLIENTE
```

> **Nota (Check-in de Producto, 15 jul 2026):** se renombró el nodo "Administrador del producto" a **Fliipa**, se eliminó el nodo "Hunter / Visitador" (perfil no existente en el modelo 100% digital) y se renombró "Asesor comercial" a **"Asesor de servicio al cliente (canales digitales)"**, consistente con los ajustes de rol acordados en esa reunión.

## Fuentes consultadas

- Elaboración propia a partir de Modelo Comercial B2B, Modelo y Proceso de Cobranza B2B, Investigación B2B y Journeys Colpatria B2B.
- Notas de la reunión "Producto: Check-in" (15 jul 2026) y su transcripción asociada.
