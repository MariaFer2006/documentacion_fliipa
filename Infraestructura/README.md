# Infraestructura

| Documento | Infraestructura |
|-----------|------------------|
| **Proyecto** | Fliipa |
| **Estado** | Borrador para validación |
| **Responsable** | Tecnología / Infraestructura |

---

## Objetivo

Documentar la infraestructura técnica de Fliipa: proveedor cloud y entornos, pipeline de despliegue, configuración y manejo de secretos, jobs batch y migraciones de base de datos, dominio y balanceo de carga, y operación diaria (rollback y pendientes).

## Alcance

Cubre exclusivamente los aspectos técnicos de infraestructura y operación de la plataforma. No incluye reglas de negocio (ver [Negocio](../Negocio/)) ni especificaciones funcionales (ver [Funcional](../Funcional/)).

## Documentos

| # | Documento | Contenido |
|---|-----------|-----------|
| 1 | [Arquitectura y Entornos](01%20Arquitectura%20y%20Entornos.md) | Proveedor GCP, proyectos y entornos (PROD / STG). |
| 2 | [Pipeline de Despliegue](02%20Pipeline%20de%20Despliegue.md) | Flujo de CI/CD. |
| 3 | [Configuración y Secretos](03%20Configuracion%20y%20Secretos.md) | Variables de entorno y manejo de secretos. |
| 4 | [Jobs y Migraciones](04%20Jobs%20y%20Migraciones.md) | Jobs batch y migraciones de base de datos. |
| 5 | [Dominio y Load Balancer](05%20Dominio%20y%20Load%20Balancer.md) | Configuración de dominio y balanceo de carga. |
| 6 | [Operación y Pendientes](06%20Operacion%20y%20Pendientes.md) | Operación diaria, rollback y pendientes. |

## Documentos relacionados

- [Negocio](../Negocio/)
- [Funcional](../Funcional/)
- [Producto](../Producto/alcance.md)
