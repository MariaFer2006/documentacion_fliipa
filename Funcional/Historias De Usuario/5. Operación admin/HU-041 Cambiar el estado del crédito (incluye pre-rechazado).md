#### HU-041 — Cambiar el estado del crédito (incluye pre-rechazado)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador / analista de riesgo |
| **Historia** | Como administrador, quiero cambiar el estado de la línea de crédito del cliente (incluido pre-rejected), para gestionar casos en evaluación o decisión manual. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Desde la ficha, con permiso, se puede cambiar el estado. Existe el estado **pre-rejected**. El rechazo definitivo de una solicitud solo procede a partir del estado **pre-rejected** (flujo: prerechazar → rechazar); no se permite rechazar directamente desde otros estados. Al pasar el crédito a pre-rechazado, el equipo recibe una alerta operativa. Los casos excepcionales que requieran un cambio de estado fuera de este flujo se gestionan mediante intervención directa en la base de datos, y no como una acción soportada desde el panel administrativo. |
| **Relaciones** | [HU-008](../2.%20KYC/HU-008%20Conocer%20el%20resultado%20en%20m%C3%A1ximo%2024%20horas.md) (resultado de la solicitud); [HU-044](../2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md)(decisión **automática** del KYC — distinta de esta). |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.8 |
| **Estado en plataforma** | **Hecho** (cambio **manual**). |
| **Comentarios** | **Corrección v1.8 (Check-in de Producto, 20 ago 2026):** se clarifican los estados de transición conforme al consenso del equipo: el rechazo solo procede desde el estado pre-rejected (no desde cualquier estado), y las excepciones puntuales se manejan vía base de datos, fuera de la aplicación. Se elimina la redacción previa sobre reentrada inconsistente del flujo, por considerarse innecesaria. El automático post-KYC es HU-044. |


