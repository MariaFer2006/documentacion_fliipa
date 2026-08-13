# Alcance del Producto

| Documento | Alcance del Producto |
|------------|----------------------|
| **Proyecto** | Fliipa |
| **Versión** | 1.2 |
| **Estado** | En revisión |
| **Responsable** | Equipo de Producto |
| **Última actualización** | 2026-07-14 |

---

# Control de versiones

| Versión | Fecha | Autor | Descripción |
|---------|-------|--------|-------------|
| 1.0 | 2026-07-07 | María Fernanda Herazo | Creación inicial del documento. |
| 1.1 | 2026-07-08 | María Fernanda Herazo | Corrección del nombre del producto, detalle del proceso de validación biométrica e hipervínculos|
| 1.2 | 2026-07-14 | (autor) | Corrección tras el Weekly Sync de Producto (10 jul 2026): se reemplazan las 11 secciones narrativas de "Alcance del MVP" por una tabla resumen; se confirma el proveedor de biometría (Olimpia); se agrega marcador de enlace pendiente al Modelo Comercial B2B. |

---

# Propósito

Definir el alcance funcional y de negocio del producto durante su primera fase de implementación, estableciendo los procesos, funcionalidades e integraciones que hacen parte del Producto Mínimo Viable (MVP), así como las capacidades que serán desarrolladas en fases posteriores.

Este documento sirve como referencia para la toma de decisiones de producto, arquitectura, desarrollo y priorización del roadmap.

---

# Objetivo

Delimitar el alcance del MVP para validar el modelo de crédito empresarial basado en datos transaccionales, permitiendo ofrecer una solución financiera escalable, sostenible y alineada con los objetivos estratégicos del negocio.

---

# Contexto

Fliipa es una plataforma de crédito rotativo B2B orientada a micro y pequeñas empresas, especialmente tenderos y comerciantes, diseñada para facilitar el acceso al crédito formal mediante el análisis de información transaccional y comportamiento comercial.

Durante el MVP, el crédito estará disponible para ser utilizado en tiendas D1, permitiendo validar el modelo de negocio, la aceptación del mercado y el desempeño del modelo de riesgo antes de su expansión a nuevos comercios y productos financieros.

La primera etapa busca establecer las bases para una plataforma financiera digital sustentada en datos transaccionales, automatización de procesos y generación de información crediticia.

---

# Alcance del MVP

La primera versión del producto comprende los siguientes procesos de negocio. El detalle operativo de cada uno (con diagramas Mermaid) está en [Procesos del negocio](../negocio/procesos/README.md); esta tabla es un resumen para efectos de alcance.

> 📎 **Modelo comercial:** el detalle completo de la captación comercial (canales, guiones y hoja de ruta del piloto) está desarrollado en la presentación *Modelo Comercial B2B*. **Enlace pendiente** — falta agregar aquí la URL de la presentación para no duplicar su contenido en texto.

| # | Proceso | Incluye |
|---|---------|---------|
| 1 | Captación comercial | Contacto inicial con clientes preaprobados; campañas comerciales; comunicación por WhatsApp; contacto telefónico; gestión del interés del cliente; seguimiento comercial. |
| 2 | Onboarding digital | Acceso mediante enlace único; validación del NIT; registro del representante legal; validación mediante OTP; aceptación de términos y condiciones; registro de ubicación; configuración del PIN de seguridad; vinculación de cuenta bancaria; cargue de certificación y extractos bancarios. |
| 3 | Validación de identidad | Validación biométrica con Olimpia para verificación de identidad (KYC); validación automática del resultado; gestión de casos en revisión; rechazo automático cuando corresponda. |
| 4 | Evaluación del riesgo | Consulta de Experian; consulta del histórico transaccional de D1; evaluación automática de reglas de negocio (definidas por Colpatria); cálculo del cupo aprobado; validación de capacidad de endeudamiento. |
| 5 | Originación del crédito | Aprobación del crédito; comunicación del cupo aprobado; generación del contrato; firma digital; generación del pagaré; activación del cupo. |
| 6 | Administración del crédito | Administración del cupo rotativo; consulta del estado del crédito, plan de pagos y saldo disponible; liberación automática del cupo al cancelar el crédito. |
| 7 | Uso del crédito | Generación del bono D1; compra en tiendas D1; bloqueo temporal del cupo durante la compra; evaluación para renovación del cupo. |
| 8 | Gestión de pagos | Débito automático mediante Druo; pago por PSE; prepago; actualización automática del saldo; liquidación del crédito. |
| 9 | Cobranza | Reintentos automáticos de débito; recordatorios de pago; bloqueo del cupo; acuerdos de pago; reestructuración de obligaciones; reporte a centrales de riesgo; cobro jurídico; castigo de cartera. |
| 10 | Servicio al cliente | Atención mediante asistente virtual basado en IA; escalamiento a agentes humanos; atención por WhatsApp y telefónica; gestión de PQRS; medición de satisfacción mediante NPS y CSAT. |
| 11 | Portal administrativo | Gestión de clientes y solicitudes; seguimiento del onboarding; consulta del análisis de riesgo; administración de la originación; seguimiento del ciclo de vida del crédito; gestión de cobranza y de campañas comerciales; consulta de indicadores operativos. |


# Integraciones incluidas

El MVP contempla integración con los siguientes sistemas externos. Para información detallada sobre cada integración, incluyendo especificaciones técnicas, costos, riesgos y SLAs, consulte la documentación en la carpeta de Integraciones.

| Sistema | Propósito | Documentación |
|----------|-----------|---------------|
| D1 | Información transaccional y utilización del bono. | [Ver integración](../tecnico/Integraciones/D1.md) |
| Experian | Consulta de riesgo crediticio. | [Ver integración](../tecnico/Integraciones/Experian.md) |
| Druo | Débito automático para el recaudo de pagos. | [Ver integración](../tecnico/Integraciones/Druo.md) |
| Olimpia | Validación biométrica y verificación de identidad (KYC). | Pendiente de documentación técnica |
| Zenvia | Gestión de notificaciones y comunicaciones con clientes mediante WhatsApp y otros canales habilitados. | [Ver integración](../tecnico/Integraciones/Zenvia.md) |
| Google Cloud Platform | Infraestructura y servicios del producto. | [Ver Infraestructura](../tecnico/infraestructura.md) |
| Colpatria (Core Bancario) | Fondeo, fiducia y políticas de originación del crédito. | [Ver integración](../tecnico/Integraciones/CoreBancario.md) |

---

# Fuera del alcance

No forman parte del MVP:

- Aplicación móvil nativa.
- Productos de ahorro.
- Productos de inversión.
- Tarjetas de crédito.
- Seguros.
- Marketplace financiero.
- Programas de fidelización.
- Múltiples perfiles administrativos.
- Gestión completa de oficinas.
- Productos para personas naturales.
- Analítica avanzada basada en inteligencia artificial.
- Consultas en lenguaje natural sobre la base de datos mediante IA.

---

# Restricciones

Durante la primera versión:

- El producto estará dirigido a micro y pequeñas empresas, especialmente tenderos y comerciantes.
- Durante el MVP, el crédito podrá utilizarse únicamente para realizar compras en tiendas D1.
- La solución contará con un portal administrativo para uso interno y aplicaciones desarrolladas bajo una arquitectura de microfrontends.
- El producto estará orientado a validar el modelo de negocio antes de escalar la operación.

# Criterios de priorización

Las funcionalidades serán priorizadas cuando aporten a alguno de los siguientes objetivos.

| Prioridad | Objetivo |
|-----------|----------|
| Alta | Validar el modelo de negocio. |
| Alta | Reducir el fraude. |
| Alta | Disminuir el riesgo crediticio. |
| Alta | Mejorar la experiencia del cliente. |
| Alta | Aumentar el uso del crédito. |
| Alta | Garantizar la sostenibilidad financiera. |
| Media | Automatizar procesos internos relacionados con la originación del crédito. |
| Baja | Funcionalidades de mejora continua. |

---

# Beneficios esperados

La implementación del alcance definido permitirá:

- Facilitar el acceso al crédito empresarial para micro y pequeñas empresas.
- Incrementar la recurrencia de compra en tiendas D1.
- Aumentar el ticket promedio.
- Evaluar el riesgo mediante datos transaccionales propios.
- Disminuir el fraude.
- Construir historial crediticio para pequeños comerciantes.
- Generar información crediticia basada en datos transaccionales que fortalezca la estrategia de datos del Grupo Santo Domingo.
- Validar un modelo financiero escalable para futuras etapas.

---

# Exclusiones

Este documento no describe:

- Arquitectura de software.
- APIs.
- Modelo de datos.
- Casos de uso.
- Historias de usuario.
- Reglas de negocio detalladas.
- Manuales de usuario.
- Casos de prueba.

Cada uno de estos temas se desarrolla en la documentación correspondiente.

---

# Documentos relacionados

- [Producto](README.md)
- [Objetivo](objetivo.md)
- [Visión](vision.md)
- [Roadmap](roadmap.md)
- [Negocio](../negocio/README.md)
- [Funcional](../funcional/README.md)
- [Conocimiento](../conocimiento/README.md)
- [Mapa del Conocimiento](../MAPA_DEL_CONOCIMIENTO.md)
 - [Procesos del negocio](../negocio/procesos/README.md)

---

# Fuentes consultadas

- Notas de la reunión "Producto: Weekly Sync" (10 jul 2026) y su transcripción asociada.
- Actores del negocio (`negocio/Actores/06-proveedores-externos.md`) — confirmación del proveedor de biometría (Olimpia) y del rol de Colpatria en las reglas de originación.