# Historias Usuario

| Documento | Historias Usuario |
|:---:|:---:|
| **Proyecto** | Fliipa |
| **Versión** | 1.6 |
| **Estado** | En revisión |
| **Responsable** | Producto y negocio |
| **Última actualización** | 2026-08-13 |

---

## Control de versiones

| Versión | Fecha | Autor | Descripción |
|:---:|:---:|:---:|:---:|
| 0.1 | 2026-07-06 | Maria Fernanda Herazo | Borrador vacío (pendiente de completar). |
| 1.0 | 2026-07-10 | María Fernanda Herazo | Primera versión completa: 28 historias de usuario por actor, en línea con Actores y Casos de Uso. |
| 1.1 | 2026-07-10 | María Fernanda Herazo | Se organizan las historias en tablas por actor, con prioridad y casos de uso relacionados. |
| 1.2 | 2026-07-10 | María Fernanda Herazo | Se convierte cada historia en una ficha individual (formato adaptado de plantilla de actor). |
| 1.3 | 2026-07-22 | Maria Fernanda Herazo | Se contrasta cada historia contra el código fuente real del repositorio `fliipa-main` (carpetas `b2b/fliipa-back`, `b2b/fliipa-checkout`, `b2b/fliipa-redemption`, `b2b/services/*`, `fliipa-ui`). Se corrigen rutas de archivo inexactas, se actualizan comentarios que afirmaban "no encontrado en el código" cuando sí existe evidencia, y se marca como **hallazgo crítico** que el backend administrativo (`backends/admin`) referenciado en HU-024 a HU-028 no existe en el repositorio analizado. Ver sección "Conclusión de la revisión" al final. |
| 1.4 | 2026-07-30 | Maria Fernanda Herazo | Se corrige el hallazgo crítico de la v1.3: el repositorio de referencia correcto es `credits-platform-main`, no `fliipa-main`. Al validar contra `credits-platform-main`, HU-024 a HU-028 sí tienen respaldo real en `backends/admin`/`apps/admin`. Se corrigen las cinco fichas con rutas verificadas y se actualiza la sección de hallazgos. |
| 1.5 | 2026-08-13 | María Fernanda Herazo | Revisión funcional y técnica integral: se elimina la referencia a "tendero", se unifica el repositorio de referencia en `credits-platform-main`, se corrige el SLA a 24 horas, se precisa la validación por OTP, se ajusta HU-008 para no afirmar la existencia del QR sin respaldo suficiente y se matiza la referencia a Datacrédito. Se reorganiza la sección final de hallazgos y conclusiones. |
| **1.6** | **2026-08-13** | María Fernanda Herazo  | Revisión funcional integral a partir de retroalimentación de negocio (24 observaciones). Cambios principales: (1) se agrega HU-002 "consultar cupo preaprobado por documento" y se **renumeran todas las historias subsecuentes**, quedando el documento en 36 historias (HU-001 a HU-036); (2) se precisa que la validación de identidad ocurre por WhatsApp **y** por correo electrónico, no por "el canal autorizado" de forma genérica; (3) se agrega historia de reintento/corrección de OTP; (4)-(6) y (8) se separan biometría y carga de soportes bancarios en dos historias atómicas y se elimina en todo el documento la restricción del flujo de KYC (y de la plataforma en general) a "desde el celular"; (7) se reescribe la historia de firma de contrato para reflejar firma digital con un proveedor externo, ya sin flujo de OTP; (9) se agrega historia dedicada a clientes con estado rechazado, en blacklist o sin crédito aprobado/activo; (10) se separan prepago por PSE y débito automático en dos historias atómicas, reformulando el débito automático como una historia de sistema ("Como Fliipa..."); (11) se separan los flujos de atención por IA y de escalamiento a agente humano; (12) se corrige error tipográfico ("Soporto" → "soporte"); (13) se corrige un criterio de aceptación que en realidad era una precondición, y se revisan todos los demás criterios de aceptación del documento; (15) se corrige título y criterios de aceptación de la historia de seguimiento a clientes sin primera compra; (17) se renombra la historia de score/Experian/histórico D1 a "Análisis de KYC + evaluación de crédito"; (22) se confirma la separación entre atención por IA y gestión humana; (23) se agrega historia de registro general de todo contacto con el cliente; (24) se complementa la historia de administración de blacklist con el registro del motivo de ingreso y se agrega historia de consulta del listado de blacklist. |

---

## Objetivo

Describir las necesidades de cada actor de Fliipa en lenguaje de negocio, como base para la priorización y el desarrollo de las funcionalidades del sistema.

## Alcance

Cubre historias de usuario para el cliente empresarial, el asesor comercial, el analista de riesgo, el analista de cartera, el agente de servicio al cliente y el administrador del producto, en línea con los actores descritos en [Actores](../negocio/Actores/README.md) y los casos de uso en [Casos De Uso](casos-de-uso.md). Usa la numeración `HU-XXX` definida en [Convenciones](../CONVENCIONES.md).

## Contenido

Cada historia se documenta como una ficha individual: identificador, descripción, criterios de aceptación, relaciones con otros elementos del desarrollo, referencias de origen, control de autor/fecha/versión y comentarios adicionales. Los campos "Referencias" y "Comentarios" fueron verificados directamente contra el código fuente en la revisión v1.3-1.5; las historias nuevas o reformuladas de la v1.6 provienen de retroalimentación de negocio y se marcan explícitamente como pendientes de verificación en código donde corresponda.

> **Nota de renumeración (v1.6):** a partir de esta versión el documento tiene 36 historias (antes 28). La tabla de correspondencia entre la numeración v1.5 y v1.6 se incluye en la "Conclusión de la revisión", al final del documento.

### Cliente empresarial

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
| **Comentarios**  | **Confirmado en código:** `create-checkout.ts` valida el Documento de Identidad y su tipo, rechaza la creación cuando ya existe un cliente asociado al Documento de Identidad y reutiliza checkouts existentes en estado `REQUEST_STARTED`. |

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
| **Comentarios** | la validación se realiza por los dos canales definidos (WhatsApp y correo electrónico), y no por "el canal autorizado"/"el canal definido" en singular como quedaba redactado hasta la v1.5. Pendiente confirmar con negocio si ambos canales son obligatorios o si basta con validar por uno de los dos. **Confirmado y ampliado (hallazgos técnicos vigentes)**: en `validate-otp.ts` existe un código comodín hardcodeado (`"490831"`, truncado según la longitud del código ingresado) que valida cualquier OTP — esto es el hallazgo de seguridad RNF-001. En `send-otp.ts` el canal `sms` no envía ningún mensaje real: solo registra una advertencia en consola (`console.warn("SMS channel not implemented yet")`) y responde `success: true` de forma simulada — esto confirma RNF-007. Ambos hallazgos son críticos y deben priorizarse antes de producción. |

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
| **Relaciones** | Casos de uso: CU-004. Historias relacionadas: HU-007, HU-022. |
| **Referencias** | [Procesos](../negocio/procesos/03-validacion-kyc.md); no se encontró en el repositorio lógica de biometría ni integración con un proveedor externo (se buscó "biometr*" y "Olimpia" en todo `b2b/`, sin resultados). |
| **Autor / Fecha / Versión** | María Fernanda Herazo|
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
| **Autor / Fecha / Versión** | María Fernanda Herazo  |
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
| **Relaciones** | Casos de uso: CU-009. Historias relacionadas: HU-010, HU-034. |
| **Referencias** | Pendiente de verificar en código; relacionado con la restricción de estados descrita en HU-010 (`fliipa-redemption/actions/auth.ts`). |
| **Autor / Fecha / Versión** | María Fernanda Herazo  |
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

#### HU-014: Débito automático de créditos vencidos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Sistema (Fliipa) |
| **Historia** | Como Fliipa, quiero debitar automáticamente los créditos que hayan superado su fecha de pago y aún presenten saldo pendiente por pagar, para asegurar el recaudo de la cartera vencida sin depender de una acción del cliente. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Un crédito es candidato a débito automático cuando: (1) superó la fecha de pago definida, (2) presenta saldo pendiente por pagar, (3) tiene una cuenta bancaria conectada y vigente en Druo, y (4) no está en un proceso de alivio o negociación activo que lo excluya. El sistema ejecuta el débito automáticamente vía Druo cuando se cumplen estas condiciones, y registra el resultado del intento (exitoso o fallido) mediante el webhook de eventos. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. Historia relacionada: HU-013. |
| **Referencias** | `b2b/fliipa-back/src/services/druo/debit-bank-account.druo.ts`, `connect-bank-account.druo.ts`; `b2b/services/webhooks/src/controllers/webhooks/druo-events.webhook.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia separada de la HU-009 original (v1.5)**. El débito automático vía Druo sí está implementado (conexión de cuenta, débito, webhook de eventos). Se corrige el enfoque de la historia: el cliente no realiza ninguna acción (de hecho, está incumplido), por lo que no debe redactarse como "Como cliente" ni "Como cliente empresarial", sino como una historia de sistema ("Como Fliipa..."); los criterios de aceptación corresponden a las condiciones que hacen a un crédito candidato al débito automático, no a una acción del usuario. |

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

### Analista de riesgo

#### HU-022: Resolver manualmente casos de biometría en revisión

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero revisar manualmente los casos de biometría marcados "en revisión", para decidir si el cliente puede continuar el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista visualiza los casos "en revisión" y registra la decisión (continuar o rechazar). |
| **Relaciones** | Casos de uso: CU-005. Historia relacionada: HU-006. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/07-kyc-evaluacion-riesgo.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | No se encontró en el código ningún estado de "en revisión" para biometría, ni una cola o pantalla de revisión manual (se buscó "en_revision", "manual_review", "under_review" en todo el repositorio, sin coincidencias). Esta historia no tiene respaldo verificable en el código fuente entregado; se recomienda confirmar si el flujo de biometría vive en un sistema externo (proveedor de biometría) no incluido en este repositorio. |

#### HU-023: Análisis de KYC + evaluación de crédito

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero ver en un solo lugar el resultado de Experian, el histórico transaccional de D1 y el score calculado, para validar o ajustar la decisión automática. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta, para un cliente dado, el resultado de Experian, el histórico D1 y el score consolidado antes de aprobar o rechazar. |
| **Relaciones** | Casos de uso: CU-006. Requerimiento: RF-010. |
| **Referencias** | `b2b/fliipa-back/src/controllers/companies/lookup-company.ts`, `institutions/get-advance-score.ts`; `b2b/services/evaluations/src/third-party/Experian/*` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: se renombra el título de la historia (antes "Ver score, Experian e histórico D1 en un solo lugar") a "Análisis de KYC + evaluación de crédito", que refleja mejor el alcance funcional. La integración con Experian sí existe en el código (microservicio `evaluations`); lo que sigue sin encontrarse es una pantalla o endpoint que consolide en un solo lugar Experian + histórico D1 + score para el analista; cada dato se consulta por endpoints separados. Recomendamos aclarar si esa consolidación visual es responsabilidad del portal administrativo (ver hallazgo crítico en la conclusión). |

### Analista de cartera / Comité de Cartera

#### HU-024: Ver cartera segmentada por bucket de mora

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero ver la cartera segmentada por bucket de mora, para priorizar mi gestión de cobro diaria. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta la cartera agrupada en pago anticipado y buckets 1 a 5, con los datos necesarios para priorizar su gestión. |
| **Relaciones** | Casos de uso: CU-012. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/02-mora-buckets.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo|
| **Comentarios** | El motor de reglas (`rules-engine`) que sí existe está enfocado en preaprobación, no en cobranza. Esta historia no está respaldada por el código fuente entregado; se recomienda validar si vive en un sistema externo de cobranza. Se mantiene la nota sobre la discrepancia de plazos de escalamiento documentada en RNF-017. |

#### HU-025: Registrar cada interacción de cobranza

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero registrar cada interacción de cobranza (canal, tipo de contacto, resultado, compromiso de pago), para mantener trazabilidad completa del caso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista registra canal, tipo de contacto, resultado y monto comprometido de cada interacción, quedando disponible en el resumen de atención del cliente. |
| **Relaciones** | Casos de uso: CU-012. Requerimientos: RF-025, RF-026. Historia relacionada: HU-030. |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/collection-notes.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo  |
| **Comentarios** | **Confirmado**: el módulo está completamente implementado — creación, edición, eliminación y listado de notas de cobranza, más un resumen de atención (`getCollectionNotesAttentionSummary`). Ver HU-030 (nueva en v1.6) para el registro de contacto general, más allá de cobranza. |

#### HU-026: Tablero semanal de priorización del Comité de Cartera

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Comité de Cartera |
| **Historia** | Como miembro del Comité de Cartera, quiero un tablero semanal con los casos priorizados (días de mora, monto, historial), para decidir alivios o escalamiento jurídico. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El comité visualiza semanalmente los casos priorizados según días de mora, flujo de caja, cuota vencida, historial y monto adeudado. |
| **Relaciones** | Casos de uso: CU-012, CU-013. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/04-gestion-escalamiento.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo  |
| **Comentarios** | Confirmado: no se encontró ningún tablero de priorización automatizado en el código revisado. Depende de la misma ausencia de lógica de mora/buckets señalada en HU-024. |

#### HU-027: Recibir casos de escalamiento jurídico automáticamente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista jurídico / abogado |
| **Historia** | Como analista jurídico, quiero recibir automáticamente los casos que llegan al bucket de escalamiento legal, para iniciar el proceso de cobro jurídico sin depender de un traspaso manual. |
| **Prioridad** | Media |
| **Criterios de aceptación** | Los casos que alcanzan el bucket de escalamiento jurídico se enrutan automáticamente al analista jurídico. |
| **Relaciones** | — |
| **Referencias** | [Actores](../negocio/Actores/03-actores-comerciales-cobranza.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin respaldo en código (consistente con la ausencia general de lógica de buckets de mora, ver HU-024). Depende de resolver primero la discrepancia de plazos de escalamiento (RNF-017). |

### Agente de servicio al cliente

#### HU-028: Recibir el caso escalado con contexto completo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero recibir el caso escalado por la IA con el contexto completo de la conversación, para no pedirle al cliente que repita su problema. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando la IA escala un caso, el agente humano ve el historial completo de la conversación antes de responder. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-028. Historia relacionada: HU-017. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Se confirma la separación entre el flujo de atención por IA (HU-016) y el de escalamiento/gestión humana (esta historia y HU-017): son procesos distintos y deben documentarse por separado. Confirmado (ver HU-016/HU-017): no existe módulo de IA conversacional ni de escalamiento en el código de `communications` ni en ningún otro servicio revisado. |

#### HU-029: Validar identidad en casos críticos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero validar la identidad del cliente antes de aprobar un caso crítico (suplantación, uso indebido del cupo), para evitar fraude. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Los casos críticos requieren validación de identidad y aprobación manual explícita del agente antes de cerrarse. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-029. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin código de respaldo encontrado; es consistente con la ausencia general de un módulo de servicio al cliente/IA en el repositorio. |

#### HU-030: Registrar cada contacto con el cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero registrar cada contacto que se tiene con el cliente, sin importar el canal o el motivo, para mantener trazabilidad completa de toda la atención brindada, no solo de la gestión de cobranza. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cada contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano) queda registrado con canal, motivo, resultado y fecha, disponible en el historial general de atención del cliente, independientemente de si el contacto está o no relacionado con cobranza. |
| **Relaciones** | Historias relacionadas: HU-006, HU-007, HU-016, HU-017, HU-025, HU-028, HU-029. |
| **Referencias** | Pendiente de verificar en código; ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no un registro general de contacto que cubra todos los flujos. |
| **Autor / Fecha / Versión** | María Fernanda Herazo  |
| **Comentarios** | **Historia agregada en la v1.6**: aunque ya existe el registro de notas de gestión de cobranza (HU-025), también se debe guardar un registro de todo contacto con el cliente en general (KYC, biometría, atención por IA, atención humana, etc.), no solo el de cobranza. |

### Administrador del producto (portal administrativo)

#### HU-031: Buscar cliente y ver historial auditado

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero buscar un cliente por documento y ver su historial completo de operaciones auditadas, para resolver dudas o disputas rápidamente. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador busca por documento y consulta hasta 500 registros de auditoría del cliente (línea de crédito, desembolsos, pagos). |
| **Relaciones** | Casos de uso: CU-015. Requerimientos: RF-030, RF-031. |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`getClientAuditedOperations`) — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada. El controlador `getClientAuditedOperations` en `backends/admin` sí existe y expone el historial auditado por cliente. |

#### HU-032: Ajustar cupo o fecha de corte

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero ajustar el cupo o la fecha de corte de una línea de crédito, para corregir casos excepcionales autorizados por negocio. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador puede ajustar dentro de los rangos válidos, quedando la acción registrada en auditoría. |
| **Relaciones** | Casos de uso: CU-015. Requerimiento: RF-018. |
| **Referencias** | `backends/admin/src/controllers/credit-lines.controller.ts` — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada. Se confirma también el hallazgo de RF-018: el admin acepta `cutoffDay` en rango 0–31, mientras que redemption exige 1–31 — discrepancia real entre ambos módulos. |

#### HU-033: Simular plan de pago con distintas tasas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero simular el plan de pago de un cliente en mora con distintas tasas, para preparar acuerdos de pago o alivios. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador ingresa tasa corriente, tasa de mora y umbral de días, y obtiene el plan de pago diario descargable en CSV. |
| **Relaciones** | Casos de uso: CU-016. Requerimiento: RF-024. |
| **Referencias** | `backends/admin/src/controllers/calculator.controller.ts` (`getCalculatorStatus`, recibe `currentInterestRate`, `overdueInterestRate`, `thresholdDays`); descarga CSV en `apps/admin/src/lib/generate-csv-file.ts` y `apps/admin/src/app/disbursements/consult/CalculatorDownloaderButton.tsx` — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo  |
| **Comentarios** | Implementada, exactamente con los campos descritos en la historia (tasa corriente, tasa de mora, umbral de días) y con descarga CSV real. |

#### HU-034: Administrar la lista negra (blacklist)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero agregar o retirar clientes de la lista negra, para bloquear casos de fraude confirmado. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El administrador agrega o retira clientes de la blacklist, validando que el cliente exista y registrando el motivo por el cual el cliente ingresa a la lista negra. |
| **Relaciones** | Casos de uso: CU-017. Requerimiento: RF-027. Historia relacionada: HU-011, HU-035. |
| **Referencias** | `backends/b2b/src/controllers/blacklist/add-client-to-blacklist.ts`, `backends/b2b/src/controllers/blacklist/remove-client-client-from-blacklist.ts` |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.6**: se agrega al criterio de aceptación el registro del motivo de ingreso a la blacklist, que hacía falta. Pendiente de verificar en código si el modelo actual de blacklist tiene un campo de motivo o si debe agregarse. A diferencia de HU-031/032/033/036, esta historia sí tenía respaldo real desde la v1.3, pero en `backends/b2b` — no en un backend administrativo separado. Se confirma el hallazgo original: no hay enforcement de la blacklist sobre checkout, evaluación de riesgo o desembolso en ningún archivo del repositorio (`blacklists` solo aparece como relación de lectura en `get-client-by-id.service.ts`, sin ninguna validación bloqueante). Este es un riesgo de negocio real y verificado. |

#### HU-035: Consultar clientes en blacklist

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero consultar la tabla de clientes en la lista negra (blacklist), para saber a quién no debo ofrecerle ningún producto o beneficio. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El administrador consulta, desde el panel administrativo, el listado completo de clientes en blacklist, incluyendo el motivo de ingreso registrado en HU-034. |
| **Relaciones** | Casos de uso: CU-017. Historia relacionada: HU-034. |
| **Referencias** | Pendiente de verificar en código si existe un endpoint o pantalla de listado de blacklist (más allá de agregar/retirar clientes de forma individual). |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Historia agregada en la v1.6**: no se encontró en el código revisado ninguna pantalla o endpoint dedicado a consultar el listado completo de blacklist; solo se identificaron los controladores para agregar y retirar clientes individualmente. |

#### HU-036: Monitorear salud del sistema en tiempo real

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador con rol de sistema (SYS_ADMIN) |
| **Historia** | Como administrador con rol de sistema, quiero ver el estado del core bancario y de la base de datos en tiempo real, para detectar incidentes antes de que afecten a los clientes. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador de sistema consulta latencia y disponibilidad del core bancario y de Cloud SQL desde el panel. |
| **Relaciones** | Casos de uso: CU-018. Requerimiento: RF-033. |
| **Referencias** | `backends/admin/src/controllers/system-core-health.controller.ts`, `system-cloud-sql.controller.ts` — confirmados en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Implementada, con un hallazgo adicional (ver RF-033): el monitoreo de terceros solo cubre GitHub, npm y GCP; no cubre Experian, Druo, el proveedor de biometría, Zenvia/Sendgrid ni el core bancario, a pesar de que la historia y el alcance del producto los describen como críticos para el negocio. |

## Conclusión de la revisión

La revisión funcional de la versión v1.6 incorporó 24 observaciones de negocio identificadas sobre la v1.5, tomando como referencia el documento fuente de retroalimentación. Los principales cambios fueron:

Incorporación de una historia previa a la consulta de cupo, lo que implicó la renumeración de las historias posteriores.
Separación de historias no atómicas en historias independientes, particularmente en los flujos de biometría y soportes bancarios, prepago y débito automático, y atención mediante IA y atención humana.
Corrección de criterios de aceptación que correspondían a precondiciones, pasos del proceso o mecanismos operativos, en lugar de condiciones verificables para determinar el cumplimiento de la historia.
Eliminación de restricciones no justificadas que limitaban el flujo exclusivamente al uso del celular.
Incorporación de historias faltantes, entre ellas el reintento de OTP, la gestión de clientes sin oferta de crédito, el registro general de contactos, la consulta de blacklist y el registro del motivo de ingreso a blacklist.

Se mantienen vigentes los hallazgos técnicos identificados en versiones anteriores, entre ellos el uso de un OTP comodín, el canal SMS simulado, la ausencia en el repositorio de módulos correspondientes a biometría, alivios, mora por buckets e IA conversacional, así como la falta de enforcement de la blacklist. Estos aspectos deberán ser revisados y priorizados conjuntamente por negocio y el equipo técnico antes de llevar las historias a desarrollo.

### Tabla de correspondencia de numeración (v1.5 → v1.6)

| v1.5 | v1.6 | Cambio |
|:---:|:---:|:---|
| HU-001 | HU-001 | Sin cambios de contenido. |
| — | **HU-002** | Nueva: consultar cupo preaprobado por documento. |
| HU-002 | HU-003 | Renumerada. |
| HU-003 | HU-004 | Actualizada: validación por WhatsApp y correo. |
| — | **HU-005** | Nueva: reintento/corrección de OTP. |
| HU-004 | HU-006 + HU-007 | Dividida en biometría y soportes bancarios. |
| HU-005 | HU-008 | Renumerada. |
| HU-006 | HU-009 | Reescrita: firma digital con proveedor externo. |
| HU-007 | HU-010 | Renumerada. |
| — | **HU-011** | Nueva: mensaje de no disponibilidad de crédito. |
| HU-008 | HU-012 | Renumerada. |
| HU-009 | HU-013 + HU-014 | Dividida en prepago (PSE) y débito automático (Fliipa). |
| HU-010 | HU-015 | Renumerada. |
| HU-011 | HU-016 + HU-017 | Dividida en atención IA y escalamiento a humano. |
| HU-012 | HU-018 | Corrección tipográfica. |
| HU-013 | HU-019 | Corrección de criterio de aceptación (precondición → resultado). |
| HU-014 | HU-020 | Renumerada. |
| HU-015 | HU-021 | Corrección de título y criterios de aceptación. |
| HU-016 | HU-022 | Renumerada. |
| HU-017 | HU-023 | Renombrada: "Análisis de KYC + evaluación de crédito". |
| HU-018 | HU-024 | Renumerada. |
| HU-019 | HU-025 | Renumerada. |
| HU-020 | HU-026 | Renumerada. |
| HU-021 | HU-027 | Renumerada. |
| HU-022 | HU-028 | Renumerada. |
| HU-023 | HU-029 | Renumerada. |
| — | **HU-030** | Nueva: registro general de contacto con el cliente. |
| HU-024 | HU-031 | Renumerada. |
| HU-025 | HU-032 | Renumerada. |
| HU-026 | HU-033 | Renumerada. |
| HU-027 | HU-034 | Actualizada: registro de motivo de ingreso a blacklist. |
| — | **HU-035** | Nueva: consultar clientes en blacklist. |
| HU-028 | HU-036 | Renumerada. |

## Fuentes consultadas

- [Actores](../negocio/Actores/README.md)
- [Procesos](../negocio/procesos/README.md)
- [Reglas Negocio](../negocio/reglas-negocio/README.md)
- [Casos De Uso](casos-de-uso.md)
- [Requerimientos Funcionales](requerimientos-funcionales.md)
- [Requerimientos No Funcionales](requerimientos-no-funcionales.md)
- Inventario funcional del código fuente `credits-platform-main` (base de la v1.0-1.2).
- La revisión de esta versión toma como referencia el repositorio `credits-platform-main`; los snapshots anteriores de `fliipa-main` se conservan únicamente como antecedente de las versiones previas.
- Revisión directa del código fuente del repositorio `credits-platform-main.zip` (incluyendo `backends/admin`, `backends/b2b`, `apps/admin`, `apps/checkout`, `apps/redemption`, `services/core/*`, `services/product/*`, `gateways/core-hub`), realizada como parte de la corrección v1.4. Este es el repositorio de código de referencia vigente.
- Documento de retroalimentación funcional de negocio sobre la versión 1.5 (24 observaciones numeradas), base de los cambios incorporados en esta versión 1.6.
