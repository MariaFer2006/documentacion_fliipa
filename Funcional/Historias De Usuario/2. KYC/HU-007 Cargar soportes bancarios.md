#### HU-007: Cargar soportes bancarios

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero cargar mi certificación bancaria y mis extractos de los últimos 3 meses, para respaldar mi solicitud de crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | 1. El cliente carga **dos archivos PDF**: uno correspondiente a la certificación bancaria y otro correspondiente a los extractos bancarios de los últimos 3 meses.<br>2. El sistema recibe los archivos y permite al cliente continuar con el flujo sin esperar a que finalice su almacenamiento.<br>3. Los archivos son enviados y almacenados en el repositorio correspondiente **en segundo plano**.<br>4. La consulta o apertura de los archivos desde el panel administrativo corresponde a la **HU-037** y no hace parte de esta historia. |
| **Relaciones** | Casos de uso: CU-005. Historia relacionada: HU-006. |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/upload-document.ts` |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | v1.7 |
| **Comentarios** | Esta historia contempla exclusivamente la **carga de los soportes bancarios**. En el flujo actual, después de indicar la cuenta bancaria, el cliente debe cargar dos archivos PDF: la certificación bancaria y los extractos de los últimos 3 meses. El sistema recibe los archivos y permite continuar con el flujo sin esperar a que finalice su almacenamiento, ya que este proceso se ejecuta en segundo plano. No se afirma que exista una confirmación visual de recepción, dado que este comportamiento no está contemplado en el flujo actual. La visualización o apertura de los soportes desde el panel administrativo corresponde a la **HU-037**. Se mantiene la definición de carga desde el dispositivo disponible y no se restringe el flujo al uso de un celular. |