# Onboarding

[← Volver al índice](README.md)

Cubre el recorrido del cliente empresarial desde el primer contacto hasta el primer uso del cupo, junto con la gestión comercial (asesor) que acompaña ese recorrido: contacto multicanal, acompañamiento durante la originación y seguimiento a clientes que no activan su primera compra.

**Historias en este capítulo:** HU-001 a HU-012, HU-018 a HU-021.

### HU-001: Recibir enlace único de solicitud

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir un enlace único de solicitud por WhatsApp, para poder iniciar mi proceso de crédito de forma directa. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe por WhatsApp un enlace único asociado a su proceso de solicitud. Al acceder al enlace, el sistema valida el Documento de Identidad y, si ya existe una solicitud en estado `REQUEST_STARTED`, la reutiliza; si no existe una solicitud iniciada, crea una nueva. El hecho de que el cliente ya esté registrado no impide el ingreso al proceso. |
| **Relaciones** | Casos de uso: CU-001, CU-002. Historias relacionadas: HU-002, HU-003, HU-019. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** al entrar con el enlace, el sistema valida el Documento de Identidad y, si ya existe una solicitud empezada en estado `REQUEST_STARTED`, la reutiliza; si no existe, crea una nueva. Que el cliente ya esté registrado no implica rechazar el ingreso. Para el equipo técnico: `create-checkout` reutiliza checkouts en estado `REQUEST_STARTED`; no existe un rechazo por el simple hecho de que ya exista un cliente asociado al documento. |

### HU-002: Consultar si tengo cupo preaprobado con mi número de documento

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ingresar mi número de documento para consultar si tengo un cupo preaprobado, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente ingresa su tipo y número de documento y el sistema consulta si existe una preaprobación asociada. El sistema informa al cliente si puede continuar con el proceso antes de completar el formulario de solicitud. |
| **Relaciones** | Casos de uso: CU-002. Historias relacionadas: HU-001, HU-003. |
| **Referencias** | [Procesos](../negocio/procesos/02-onboarding-digital.md); `b2b/services/rules-engine/src/rule-models/b2b-base-preapproval.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** el cliente ingresa su Documento de Identidad y el sistema determina si cuenta con una preaprobación y puede continuar con el proceso, antes de completar todo el formulario. Esta historia es distinta de HU-003: HU-002 valida la existencia de una preaprobación y determina si el cliente puede continuar; HU-003 corresponde a la visualización del valor del cupo preaprobado. |

### HU-003: Ver cupo preaprobado antes de completar el formulario

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero consultar mi cupo preaprobado antes de completar el formulario, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Una vez identificada la preaprobación del cliente, el sistema muestra el valor del cupo preaprobado o sugerido antes de exigirle completar todos los pasos del onboarding. El valor mostrado corresponde al cupo disponible para el proceso de solicitud según la información de preaprobación cargada y procesada por la plataforma. |
| **Relaciones** | Casos de uso: CU-002. Requerimiento: RF-005. Historias relacionadas: HU-002, HU-004. |
| **Referencias** | [Procesos](../negocio/procesos/02-onboarding-digital.md); `b2b/services/rules-engine/src/rule-models/b2b-base-preapproval.ts`, `b2b/services/rules-engine/src/utils/get-suggested-credit.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** la preaprobación y el cupo sugerido están operativos en el motor de riesgo. La plataforma permite cargar los clientes preaprobados mediante archivo, consultar/procesar la información de preaprobación y obtener el cupo sugerido utilizado en el flujo. Por tanto, esta funcionalidad no corresponde únicamente a un diseño documental, sino que cuenta con soporte operativo en el motor de riesgo. |
#### HU-004: Confirmar identidad

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero confirmar mi identidad mediante un código de verificación enviado por WhatsApp y por correo electrónico, para validar mi identidad de forma segura. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe el código OTP tanto por WhatsApp como por correo electrónico, lo ingresa en la plataforma y el sistema valida el código antes de permitirle continuar. Si la validación falla, el sistema muestra un mensaje genérico y no revela información sensible. |
| **Relaciones** | Casos de uso: CU-003. Requerimiento: RF-006. Historias relacionadas: HU-003, HU-005. |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-otp.ts`, `otp/validate-otp.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | la validación se realiza por los dos canales definidos (WhatsApp y correo electrónico), y no por "el canal autorizado"/"el canal definido" en singular como quedaba redactado hasta la v1.5. Pendiente confirmar con negocio si ambos canales son obligatorios o si basta con validar por uno de los dos. **Confirmado y ampliado (hallazgos técnicos vigentes)**: en `validate-otp.ts` existe un código comodín hardcodeado (`"490831"`, truncado según la longitud del código ingresado) que valida cualquier OTP — esto es el hallazgo de seguridad RNF-001. En `send-otp.ts` el canal `sms` no envía ningún mensaje real: solo registra una advertencia en consola (`console.warn("SMS channel not implemented yet")`) y responde `success: true` de forma simulada — esto confirma RNF-007. Ambos hallazgos son críticos y deben priorizarse antes de producción. |

### HU-005: Reintentar o corregir el envío del OTP

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero poder reintentar el envío del código OTP cuando no me llega, o corregir mi número de teléfono o correo si los ingresé mal, para poder completar la validación de identidad. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede solicitar nuevamente el envío del código OTP cuando no lo recibe, respetando el tiempo de espera definido entre envíos. Si el cliente ingresó incorrectamente su número de teléfono o correo electrónico, puede regresar al paso anterior, corregir el dato y solicitar un nuevo código sin reiniciar toda la solicitud. El nuevo código se envía al dato de contacto corregido. |
| **Relaciones** | Casos de uso: CU-003. Historia relacionada: HU-004. |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-otp.ts`, `otp/validate-otp.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** el cliente puede solicitar nuevamente el código OTP y existe un tiempo de espera entre envíos. Si el número de teléfono o correo fue ingresado incorrectamente, el cliente puede regresar al paso anterior, corregir el dato y solicitar un nuevo código sin reiniciar la solicitud desde cero. |


#### HU-006: Completar la validación biométrica (KYC)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero completar la validación biométrica con el proveedor externo, para verificar mi identidad de forma segura sin tener que ir a una oficina. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente completa el proceso de biometría con el proveedor externo definido, desde el dispositivo que tenga disponible, y el sistema registra el resultado (aprobado, rechazado o en revisión) asociado a su solicitud. |
| **Relaciones** | Casos de uso: CU-004. Historias relacionadas: HU-007, HU-022. |
| **Referencias** | [Procesos](../negocio/procesos/03-validacion-kyc.md); no se encontró en el repositorio lógica de biometría ni integración con un proveedor externo (se buscó "biometr*" y "Olimpia" en todo `b2b/`, sin resultados). |
| **Autor / Fecha / Versión** | María Fernanda Herazo|
| **Comentarios** | **Historia separada de la HU-004 original (v1.5)**, que combinaba biometría y carga de soportes bancarios en un solo paso; al ser dos procesos distintos y no relacionados, deben documentarse como historias atómicas. Se elimina la restricción a "desde el celular": el cliente debe poder completar este paso desde el dispositivo que tenga disponible (celular, computador u otro), ya que la plataforma no debe limitarse a un flujo exclusivamente móvil. Se mantiene pendiente de confirmar si la biometría vive en un microservicio no incluido en este repositorio. |


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


#### HU-008: Conocer el resultado en máximo 24 horas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero conocer el resultado de mi solicitud en máximo 24 horas, para poder planear mis compras en D1. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe notificación de aprobación o rechazo dentro de las 24 horas siguientes a completar la validación de identidad, la biometría y la carga de soportes bancarios. |
| **Relaciones** | Casos de uso: CU-006. Requerimientos: RF-010, RF-011, RF-012. Historias relacionadas: HU-006, HU-007. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/01-cupo-credito.md); `b2b/services/evaluations/src/third-party/Experian/authentication-experian.ts`, `midecisorpj.ts`, `reconocer.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmada** en el microservicio `b2b/services/evaluations`, que autentica contra Experian y consulta el score (`midecisorpj`) y la identidad (`reconocer`). El controlador `b2b/fliipa-back/src/controllers/institutions/get-advance-score.ts` actúa como proxy hacia ese microservicio vía `evaluationsClient`. La referencia a **Datacrédito** debe interpretarse con cautela: la evidencia revisada no permite concluir que corresponda a un segundo buró independiente utilizado en paralelo con Experian. No se encontró un job o temporizador que garantice el SLA de 24 horas; ese plazo parece ser un compromiso operativo/de negocio, no una regla codificada. |

#### HU-009: Firmar contrato mediante firma digital con proveedor externo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero firmar mi contrato mediante firma digital con un proveedor externo, para activar mi cupo sin papeleo físico. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente revisa el contrato y lo firma a través del mecanismo de firma digital del proveedor externo definido para este flujo. El sistema genera el PDF firmado y lo envía por correo al cliente. |
| **Relaciones** | Casos de uso: CU-007. Requerimientos: RF-013, RF-014 (pendiente confirmar vigencia dado el cambio de mecanismo). |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/sign-contract.ts`, `send-contract/send-contract.controller.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: esta historia (antes HU-006, v1.5) ya no debe describir una firma por código OTP; según retroalimentación de negocio, ese flujo ya no ocurre y la firma se realiza mediante un proveedor externo de firma digital. Se retira la referencia a `send-signature-otp.ts`. Se recomienda que el equipo técnico confirme el proveedor de firma digital vigente y evalúe si `send-signature-otp.ts` debe retirarse del código para evitar mantener lógica obsoleta. |

#### HU-010: Consultar cupo, plan de pagos y movimientos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero consultar mi cupo disponible, mi plan de pagos y mis movimientos, para saber cuánto puedo usar y cuánto debo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente accede al portal de usuarios y visualiza cupo disponible, plan de pagos y movimientos, solo si su línea de crédito está en estado Aprobado o Activa. |
| **Relaciones** | Casos de uso: CU-009. Requerimientos: RF-016, RF-017. Historia relacionada: HU-011. |
| **Referencias** | `b2b/fliipa-back/src/controllers/credit-line/get-credit-status.ts`, `credit-line/get-disbursements.ts`; `b2b/fliipa-redemption/actions/auth.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Los endpoints de estado de crédito y desembolsos existen y delegan en un cliente del core bancario (`coreApiClient`). La restricción exacta a estados `approved`/`active` no se verificó línea por línea; se recomienda confirmarla en la capa de autenticación de `fliipa-redemption/actions/auth.ts`. |


### HU-011: Ver mensaje de no disponibilidad de crédito

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ver un mensaje claro cuando no tengo ninguna opción de crédito disponible, para entender mi situación cuando no puedo continuar con el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando el cliente no puede continuar porque su solicitud fue rechazada, no existe una oferta disponible o no existe un crédito con el que pueda continuar, el portal muestra un mensaje claro indicando que actualmente no hay opciones de crédito disponibles, en lugar de mostrar un error o una pantalla vacía. |
| **Relaciones** | Casos de uso: CU-009. Historias relacionadas: HU-010, HU-034. |
| **Referencias** | Relacionado con la lógica de ingreso y consulta del estado del crédito en `fliipa-redemption`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en plataforma:** existe un mensaje claro para los casos en los que el cliente no puede continuar, principalmente cuando el estado del crédito no permite avanzar o no existe un match/oferta disponible. **Corrección v1.6:** estar incluido en una lista negra (blacklist) no debe documentarse como condición que dispara este mensaje en el ingreso actual, ya que no corresponde al comportamiento observado en el flujo vigente. |

#### HU-012: Usar el cupo en tienda D1

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero generar un código de compra para usar mi cupo en la tienda D1, para pagar mi mercancía sin dinero en efectivo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente obtiene un código de compra y el punto de venta D1 lo valida para aplicar el cupo a la compra. |
| **Relaciones** | Casos de uso: CU-010. Requerimientos: RF-019, RF-020. |
| **Referencias** | `b2b/fliipa-back/src/controllers/qr/get-or-create-qr.ts`, `qr/validate-qr.ts`, `clients/get-client-coupon.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.5:** la historia se limita al código de compra/cupón, que sí cuenta con referencia funcional en el repositorio. |

#### HU-013: Prepagar la cuota por PSE

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero prepagar mi cuota antes de la fecha de corte mediante PSE, para no incurrir en mora y mantener un buen comportamiento de crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede realizar el pago de su cuota en cualquier momento antes de la fecha de corte mediante PSE, y el sistema refleja el pago en su plan de pagos y en su cupo disponible. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. Historia relacionada: HU-014. |
| **Referencias** | [Procesos](../negocio/procesos/08-cobro-pago.md); no se encontró implementación de pago por PSE en ningún archivo del repositorio (se buscó "PSE" en todo el proyecto sin coincidencias). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-009 original (v1.5)**, que combinaba prepago y débito automático en un solo paso; aunque ambos son pagos y ambos usan Druo, son procesos distintos que pertenecen a flujos diferentes. Se mantiene pendiente de confirmar con el equipo técnico si el prepago por PSE vive en un microservicio no incluido en este repositorio. |

### HU-014: Débito automático de créditos vencidos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero gestionar el débito automático de créditos que hayan superado su fecha de pago y mantengan un saldo pendiente, para facilitar el recaudo de la cartera vencida sin depender de una acción manual del cliente. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El sistema debe identificar los créditos vencidos que podrían ser candidatos a débito automático de acuerdo con las reglas de cartera definidas. La cuenta bancaria del cliente debe estar previamente conectada y vigente mediante Druo. Cuando el débito automático de cartera vencida esté habilitado como producto, el sistema deberá ejecutar el débito conforme a las reglas definidas y registrar el resultado del intento. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. Historia relacionada: HU-013. |
| **Referencias** | `b2b/fliipa-back/src/services/druo/debit-bank-account.druo.ts`, `connect-bank-account.druo.ts`; `b2b/fliipa-back/src/controllers/webhooks/druo-events.webhook.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6:** actualmente está implementada la conexión de la cuenta bancaria mediante Druo y existen mecanismos para recibir avisos/eventos relacionados con dicha conexión. Sin embargo, el **débito automático de una cuota vencida de punta a punta todavía no está implementado como funcionalidad de producto**. Por tanto, esta historia no debe marcarse como implementada. La existencia de `debit-bank-account.druo.ts` no es suficiente para afirmar que el flujo completo de cobro automático de cartera vencida está operativo. |

#### HU-015: Recibir alivios ante dificultades de pago

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir alivios (abono parcial, congelamiento de intereses) cuando tengo dificultades temporales de pago, para no perder mi cupo ni mi historial. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede acceder al abono parcial, congelamiento de intereses o condonación, según las condiciones y topes definidos por bucket de mora. |
| **Relaciones** | Casos de uso: CU-013. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/03-alivios-negociacion.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | No se encontró ningún módulo de alivios, condonación ni "bucket de mora" en el código revisado (se buscó "bucket", "mora", "condona*", "alivio*" en todo el repositorio; sin coincidencias relevantes — únicamente coincidencias de "bucket" de almacenamiento GCP, sin relación con cartera). Esta funcionalidad parece no estar implementada en el código fuente entregado, o vive en un sistema externo/manual. Se recomienda confirmar con negocio. |

#### HU-016: Atención inicial por asistente virtual con IA

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que un asistente virtual con inteligencia artificial atienda mi primer contacto por WhatsApp, para obtener respuesta inmediata a mis dudas más comunes. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El asistente virtual con IA recibe y responde el primer contacto del cliente por WhatsApp, dentro de las dudas frecuentes definidas en su alcance. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-028. Historia relacionada: HU-017. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md); `b2b/services/communications/src/controllers/whatsapp/whatsapp.controller.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-011 original (v1.5)**, que combinaba el flujo de atención por IA con el flujo de escalamiento a un agente humano; deben documentarse por separado para no interferir con los procesos ya definidos de servicio al cliente y de la operación. No se encontró en el código revisado ningún módulo de asistente conversacional de IA ni lógica de escalamiento; los controladores del microservicio `communications` están limitados a envío de OTP, firma y contrato por WhatsApp/correo. Probablemente vive en una herramienta externa no incluida en este repositorio. |

#### HU-017: Escalar a agente humano cuando la IA no resuelve el caso

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que mi caso se escale a un agente humano cuando el asistente virtual no logre resolverlo, para no depender únicamente de canales automatizados. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando el asistente virtual no resuelve el caso del cliente, el sistema escala el caso a un agente humano junto con el contexto completo de la conversación. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-029. Historias relacionadas: HU-016, HU-028. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-011 original (v1.5)**. No se encontró lógica de escalamiento en el código revisado; corresponde al mismo hallazgo documentado en HU-016 y en HU-028 (antes HU-022). |

#### HU-018: Recuperar PIN o desbloquear la cuenta

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recuperar mi PIN si lo olvido o mi cuenta se bloquea, para no perder el acceso a mi cupo. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El cliente debe comunicarse con soporte para recibir ayuda y generar un nuevo PIN. |
| **Relaciones** | Requerimiento: RNF-014 (bloqueo de acceso). |
| **Referencias** | `b2b/fliipa-back/src/db/models/Client.ts` (`loginAttempts`, `lockedAt`); `b2b/fliipa-redemption/components/pages/login/ResetPin.tsx` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: se corrige error tipográfico ("Soporto" → "soporte") en el criterio de aceptación. **Confirmado y ampliado**: además del modelo con `loginAttempts`/`lockedAt`, existe un componente de UI dedicado (`ResetPin.tsx`) dentro del flujo de login de `fliipa-redemption`. |

### Asesor comercial

#### HU-019: Contacto simultáneo multicanal

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero contactar simultáneamente por correo, WhatsApp y llamada a los clientes preaprobados, para maximizar la tasa de respuesta. |
| **Prioridad** | Alta |
| **Precondiciones** | El asesor cuenta con la base de clientes preaprobados y con las plantillas de contacto por los tres canales. |
| **Criterios de aceptación** | El cliente recibe contacto por todos los canales definidos (correo, WhatsApp y llamada) y el equipo comercial puede registrar y consultar la tasa de respuesta por canal. |
| **Relaciones** | Casos de uso: CU-001. Requerimiento: RF-001. Historia relacionada: HU-001. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/services/rules-engine/src/db/repositories/get-clients.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: el criterio de aceptación original ("El asesor cuenta con la base de clientes preaprobados y las plantillas de contacto por los tres canales") era en realidad una precondición (algo que se necesita para que la historia se cumpla), no un criterio de aceptación (cómo se sabe que la historia se cumple correctamente). Se traslada al nuevo campo "Precondiciones" y se reemplaza el criterio de aceptación por uno centrado en el resultado. Se revisaron los criterios de aceptación de todas las demás historias del documento y no se identificaron otros casos de precondiciones redactadas como criterios de aceptación. Existe una base de clientes preaprobados en `rules-engine` (`get-clients.ts`, `get-evaluation-clients.handler.ts`), pero no se encontró una herramienta de contacto multicanal orquestada para el asesor (llamadas, plantillas) en el código; probablemente es un proceso manual o de una herramienta externa (CRM). |

#### HU-020: Acompañar la originación del cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero acompañar al cliente durante la originación (dudas, preguntas o inquietudes), para reducir el abandono del proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El asesor realiza seguimiento remoto al cliente durante el proceso de onboarding, atiende sus dudas e inquietudes y brinda orientación cuando sea necesario. El seguimiento se realiza mediante los canales definidos para la gestión comercial, sin requerir visitas presenciales. |
| **Relaciones** | Casos de uso: CU-001. |
| **Referencias** | [Actores](../negocio/Actores/03-actores-comerciales-cobranza.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin cambios: es un proceso operativo/humano, no se esperaba ni se encontró respaldo directo en código. |

#### HU-021: Identificar clients sin uso del cupo tras la activación

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero identificar y gestionar a los clientes que no han realizado su primera compra después de la activación de su cupo, para conocer las causas de no uso y facilitar el inicio de su crédito. |
| **Prioridad** | Media |
| **Criterios de aceptación** | Se contacta al cliente que no ha realizado su primera compra. Se registra en la gestión el motivo por el cual no ha utilizado su cupo aprobado hasta el momento. Se solucionan las inquietudes o problemas identificados que impidan al cliente realizar su primera compra y comenzar a utilizar su crédito. |
| **Relaciones** | — |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6:** se ajusta la historia para enfocarla en los clientes que **no han realizado su primera compra**, evitando interpretarla como un seguimiento de una compra ya realizada. Los criterios de aceptación se centran en los resultados de la gestión: contacto con el cliente, registro del motivo de no uso y solución de las inquietudes o problemas que impidan iniciar el uso del crédito. La identificación de clientes sin uso del cupo a los 7 días corresponde al mecanismo operativo para activar esta gestión y no constituye por sí misma un criterio de aceptación. |


 
