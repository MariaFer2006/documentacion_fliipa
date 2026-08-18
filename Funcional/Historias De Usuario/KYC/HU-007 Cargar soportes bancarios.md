#### HU-007: Cargar soportes bancarios

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero cargar mi certificación bancaria y los extractos de los últimos meses, para respaldar mi solicitud de crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente carga **dos archivos PDF**: la certificación bancaria y los extractos de los últimos meses. El sistema confirma la recepción de cada soporte y permite continuar con el flujo sin esperar a que finalice el almacenamiento de los archivos. |
| **Relaciones** | Casos de uso: CU-005. Historia relacionada: HU-006 y HU-037. |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/upload-document.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-004 original (v1.5).** En el flujo actual, después de indicar la cuenta bancaria, el cliente carga **dos archivos PDF**: la certificación bancaria y los extractos de los últimos meses. El sistema **acepta la carga de inmediato**, permite al cliente continuar y realiza el envío de los archivos al almacenamiento **en segundo plano**. La consulta y apertura de estos soportes desde el panel administrativo corresponde a **HU-037** y no forma parte de esta historia. Se elimina la restricción a “desde el celular”, ya que el cargue puede realizarse desde el dispositivo disponible para el cliente. |
