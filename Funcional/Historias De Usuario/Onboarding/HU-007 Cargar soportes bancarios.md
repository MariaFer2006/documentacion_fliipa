

### HU-007: Cargar soportes bancarios

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero cargar mi certificación bancaria y mis extractos de los últimos meses, para respaldar mi solicitud de crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Después de indicar la cuenta bancaria, el cliente puede cargar dos archivos PDF: la certificación bancaria y los extractos de los últimos meses. El sistema acepta la carga y permite al cliente continuar sin esperar a que los archivos terminen de almacenarse. Los archivos son enviados al almacenamiento en segundo plano. |
| **Relaciones** | Casos de uso: CU-005. Historias relacionadas: HU-006, HU-037. |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/upload-document.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en el flujo actual:** después de indicar la cuenta bancaria, el cliente carga dos archivos PDF correspondientes a la certificación bancaria y los extractos de los últimos meses. El sistema responde y permite continuar inmediatamente; el almacenamiento de los archivos se realiza en segundo plano, sin hacer esperar al cliente hasta que finalice la carga al bucket. La visualización o apertura de estos archivos desde el panel administrativo corresponde a **HU-037**, no a esta historia. |
