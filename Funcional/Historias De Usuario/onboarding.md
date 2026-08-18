# Onboarding

[← Volver al índice](README.md)

Cubre el recorrido del cliente empresarial desde el primer contacto hasta el primer uso del cupo, junto con la gestión comercial (asesor) que acompaña ese recorrido: contacto multicanal, acompañamiento durante la originación y seguimiento a clientes que no activan su primera compra.

**Historias en este capítulo:** HU-001 a HU-012, HU-018 a HU-021.

---

## Cliente empresarial

#### HU-001: Recibir enlace único de solicitud

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir un enlace único de solicitud por WhatsApp, para poder iniciar mi proceso de crédito de forma directa. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe por WhatsApp un enlace único asociado a su proceso de solicitud. Al acceder al enlace, el sistema crea un nuevo checkout para el cliente o reanuda uno existente en estado `REQUEST_STARTED`, según corresponda. |
| **Relaciones** | Casos de uso: CU-001, CU-002. Historias relacionadas: HU-002, HU-003, HU-019. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en código:** `create-checkout.ts` valida el Documento de Identidad y su tipo, rechaza la creación cuando ya existe un cliente asociado al Documento de Identidad y reutiliza checkouts existentes en estado `REQUEST_STARTED`. |

#### HU-002: Consultar si tengo cupo preaprobado con mi número de documento

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ingresar mi número de documento para consultar si tengo un cupo preaprobado, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente ingresa su tipo y número de documento y el sistema indica si existe o no un cupo preaprobado asociado a ese documento, antes de iniciar el formulario completo de solicitud. |
| **Relaciones** | Casos de uso: CU-002. Historias relacionadas: HU-001, HU-003. |
| **Referencias** | Pendiente de verificar en código; potencialmente relacionado con el mismo modelo de preaprobación usado en HU-003 (`b2b/services/rules-engine/src/rule-models/b2b-base-preapproval.ts`). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia agregada en la v1.6** a partir de retroalimentación de negocio: se incorpora un paso previo en el que el cliente consulta si tiene cupo preaprobado mediante su número de documento, antes de visualizar el detalle del cupo (HU-003) y completar el formulario. Pendiente de confirmar con el equipo técnico si esta consulta utiliza el mismo endpoint de HU-003 o uno independiente. |

#### HU-003: Ver cupo preaprobado antes de completar el formulario

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero consultar mi cupo preaprobado antes de completar el formulario, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El sistema muestra al cliente el valor de su cupo preaprobado, calculado a partir del histórico de consumo en D1, antes de exigirle completar todos los pasos del onboarding. |
| **Relaciones** | Casos de uso: CU-002. Requerimiento: RF-005. Historias relacionadas: HU-002, HU-004. |
| **Referencias** | [Procesos](../negocio/procesos/02-onboarding-digital.md); `b2b/services/rules-engine/src/rule-models/b2b-base-preapproval.ts`, `b2b/services/rules-engine/src/utils/get-suggested-credit.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en código:** el microservicio `rules-engine` implementa un modelo de preaprobación (`b2b-base-preapproval.ts`) y utilidades para obtener el cupo sugerido (`get-suggested-credit.ts`), además de un script de importación de un Excel de preaprobación (`scripts/import-preapproval-excel.ts`). Está pendiente validar con negocio si este es el único modelo vigente o si existe otro origen para el cálculo del cupo. |

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
| **Comentarios** | La validación se realiza por los dos canales definidos (WhatsApp y correo electrónico), y no por "el canal autorizado"/"el canal definido" en singular como quedaba redactado hasta la v1.5. Pendiente confirmar con negocio si ambos canales son obligatorios o si basta con validar por uno de los dos. **Confirmado y ampliado (hallazgos técnicos vigentes)**: en `validate-otp.ts` existe un código comodín hardcodeado (`"490831"`, truncado según la longitud del código ingresado) que valida cualquier OTP — esto es el hallazgo de seguridad RNF-001. En `send-otp.ts` el canal `sms` no envía ningún mensaje real: solo registra una advertencia en consola (`console.warn("SMS channel not implemented yet")`) y responde `success: true` de forma simulada — esto confirma RNF-007. Ambos hallazgos son críticos y deben priorizarse antes de producción. |

#### HU-005: Reintentar o corregir el envío del OTP

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero poder reintentar el envío del código OTP cuando no me llega, o corregir mi número de teléfono o correo si los ingresé mal, para poder completar la validación de identidad. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede solicitar el reenvío del código OTP cuando no lo recibe. El cliente puede corregir el número de teléfono o el correo electrónico ingresado y recibir un nuevo código en el dato corregido, sin tener que reiniciar todo el proceso de solicitud. |
| **Relaciones** | Casos de uso: CU-003. Historia relacionada: HU-004. |
| **Referencias** | Pendiente de verificar en código; no se validó explícitamente en esta revisión si `otp/send-otp.ts` soporta reenvío o corrección del dato de contacto. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia agregada en la v1.6**: no existía ninguna historia que cubriera el reintento de OTP ante no recepción o error de digitación del número/correo. Se recomienda validar en código si existe límite de reintentos y si hay una pantalla para corregir el dato de contacto. |

#### HU-006: Completar la validación biométrica (KYC)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero completar la validación biométrica con el proveedor externo, para verificar mi identidad de forma segura sin tener que ir a una oficina. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente completa el proceso de biometría con el proveedor externo definido, desde el dispositivo que tenga disponible, y el sistema registra el resultado (aprobado, rechazado o en revisión) asociado a su solicitud. |
| **Relaciones** | Casos de uso: CU-004. Historias relacionadas: HU-007, HU-022 (capítulo [KYC](kyc.md)). |
| **Referencias** | [Procesos](../negocio/procesos/03-validacion-kyc.md); no se encontró en el repositorio lógica de biometría ni integración con un proveedor externo (se buscó "biometr*" y "Olimpia" en todo `b2b/`, sin resultados). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-004 original (v1.5)**, que combinaba biometría y carga de soportes bancarios en un solo paso; al ser dos procesos distintos y no relacionados, deben documentarse como historias atómicas. Se elimina la restricción a "desde el celular": el cliente debe poder completar este paso desde el dispositivo que tenga disponible (celular, computador u otro), ya que la plataforma no debe limitarse a un flujo exclusivamente móvil. Se mantiene pendiente de confirmar si la biometría vive en un microservicio no incluido en este repositorio. |

#### HU-007: Cargar soportes bancarios

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero cargar mi certificación bancaria y mis extractos de los últimos 3 meses, para respaldar mi solicitud de crédito. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente carga la certificación bancaria y los extractos de los últimos 3 meses desde el dispositivo que tenga disponible, y el sistema confirma la recepción de cada soporte. |
| **Relaciones** | Casos de uso: CU-005. Historia relacionada: HU-006. |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/upload-document.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-004 original (v1.5)**. El controlador `upload-document.ts` solo acepta los tipos de documento `id_document` y `bank_certificate`; no hay lógica que trate "los extractos de los últimos 3 meses" como un conjunto separado. Se recomienda confirmar con el equipo técnico si esto corresponde a un solo archivo o a varios archivos independientes. Se elimina la restricción a "desde el celular" por la misma razón indicada en HU-006. |

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

#### HU-011: Ver mensaje de no disponibilidad de crédito

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ver un mensaje claro cuando no tengo ninguna opción de crédito disponible, para entender mi situación cuando mi solicitud fue rechazada, estoy en la lista negra (blacklist) o no tengo un crédito aprobado ni activo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando el cliente tiene estado rechazado, está en blacklist o no tiene ningún crédito aprobado ni activo, el portal le muestra un mensaje (*happy message*) indicando que de momento no hay opciones de crédito disponibles, en lugar de mostrar un error o una pantalla vacía. |
| **Relaciones** | Casos de uso: CU-009. Historias relacionadas: HU-010, HU-034 (capítulo [Administración](administracion.md)). |
| **Referencias** | Pendiente de verificar en código; relacionado con la restricción de estados descrita en HU-010 (`fliipa-redemption/actions/auth.ts`). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia agregada en la v1.6**: la HU-010 (antes HU-007) solo cubre al cliente con estado Aprobado o Activo; hacía falta una historia dedicada a los clientes con estado rechazado, en blacklist o sin crédito, para evitarles una experiencia confusa o un error en el portal. |

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

## Asesor comercial

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

#### HU-021: Identificar clientes sin uso del cupo tras la activación

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

---

[← Volver al índice](README.md) · [Siguiente: KYC →](kyc.md)
