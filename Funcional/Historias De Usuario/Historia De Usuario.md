# Historias Usuario

| Documento | Historias Usuario |
|:---:|:---:|
| **Proyecto** | Fliipa |
| **Versión** | 1.5 |
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
| **1.4** | **2026-07-30** | Maria Fernanda Herazo | Se corrige el hallazgo crítico de la v1.3: el repositorio de referencia correcto es `credits-platform-main`, no `fliipa-main`. Al validar contra `credits-platform-main`, HU-024 a HU-028 sí tienen respaldo real en `backends/admin`/`apps/admin`. Se corrigen las cinco fichas con rutas verificadas y se actualiza la sección de hallazgos. |
| **1.5** | **2026-08-13** | María Fernanda Herazo | Revisión funcional y técnica integral: se elimina la referencia a "tendero" y a , se unifica el repositorio de referencia en `credits-platform-main`, se corrige el SLA a 24 horas, se precisa la validación por OTP, se ajusta HU-008 para no afirmar la existencia del QR sin respaldo suficiente y se matiza la referencia a Datacrédito. Se reorganiza la sección final de hallazgos y conclusiones. |

---

## Objetivo

Describir las necesidades de cada actor de Fliipa en lenguaje de negocio, como base para la priorización y el desarrollo de las funcionalidades del sistema.

## Alcance

Cubre historias de usuario para el cliente empresarial, el asesor comercial, el analista de riesgo, el analista de cartera, el agente de servicio al cliente y el administrador del producto, en línea con los actores descritos en [Actores](../negocio/Actores/README.md) y los casos de uso en [Casos De Uso](casos-de-uso.md). Usa la numeración `HU-XXX` definida en [Convenciones](../CONVENCIONES.md).


## Contenido

Cada historia se documenta como una ficha individual: identificador, descripción, criterios de aceptación, relaciones con otros elementos del desarrollo, referencias de origen, control de autor/fecha/versión y comentarios adicionales. **Los campos "Referencias" y "Comentarios" fueron verificados directamente contra el código fuente en esta revisión (v1.3)**; donde el comentario original era impreciso o la ruta no existía, se corrigió y se documentó la evidencia encontrada.

### Cliente empresarial

#### HU-001: Recibir enlace único de solicitud

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir un enlace único de solicitud por WhatsApp, para poder iniciar mi proceso de crédito sin tener que buscarlo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe el enlace por WhatsApp como parte del contacto simultáneo (correo, WhatsApp, llamada). El enlace crea un checkout nuevo o reanuda uno existente en `REQUEST_STARTED` para su documento. |
| **Relaciones** | Casos de uso: CU-001, CU-002. Historias relacionadas: HU-002, HU-013. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` *(ruta corregida; antes: `backends/b2b/...`)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado en código**: `create-checkout.ts` valida documento/tipo de documento, rechaza si ya existe un cliente con ese documento, y reutiliza checkouts en estado `REQUEST_STARTED`. El comportamiento descrito coincide con la implementación real. |

#### HU-002: Ver cupo preaprobado antes de completar el formulario

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ver mi cupo preaprobado antes de completar todo el formulario, para decidir si vale la pena continuar. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El sistema muestra el cupo preaprobado calculado a partir del histórico de consumo en D1, antes de exigir todos los pasos del onboarding. |
| **Relaciones** | Casos de uso: CU-002. Requerimiento: RF-005. |
| **Referencias** | [Procesos](../negocio/procesos/02-onboarding-digital.md); `b2b/services/rules-engine/src/rule-models/b2b-base-preapproval.ts`, `b2b/services/rules-engine/src/utils/get-suggested-credit.ts` *(referencia agregada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** |  Sí existe en el código: el microservicio `rules-engine` implementa un modelo de preaprobación (`b2b-base-preapproval.ts`) y utilidades de cupo sugerido (`get-suggested-credit.ts`), con un script de importación de un Excel de preaprobación (`scripts/import-preapproval-excel.ts`). Falta validar con negocio si este es el único modelo vigente o si hay otro origen adicional del cálculo. |

#### HU-003: Confirmar identidad

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero confirmar mi identidad mediante un código enviado por un canal autorizado, para validar mi identidad de forma segura. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe un código OTP por el canal definido para el proceso, lo ingresa en la plataforma y el sistema valida el código antes de permitirle continuar. Si la validación falla, el sistema muestra un mensaje genérico y no revela información sensible. |
| **Relaciones** | Casos de uso: CU-003. Requerimiento: RF-006. |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-otp.ts`, `otp/validate-otp.ts` *(ruta corregida; antes: `backends/b2b/...`)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado y ampliado**: en `validate-otp.ts` existe un código comodín hardcodeado (`"490831"`, truncado según la longitud del código ingresado) que valida cualquier OTP — esto es el hallazgo de seguridad RNF-001, verificado directamente en el código. En `send-otp.ts` el canal `sms` no envía ningún mensaje real: solo registra una advertencia en consola (`console.warn("SMS channel not implemented yet")`) y responde `success: true` de forma simulada — esto confirma RNF-007. Ambos hallazgos son críticos y deben priorizarse antes de producción. |

#### HU-004: Completar KYC y cargar soportes desde el celular

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero completar la validación biométrica y cargar mi información desde el celular, para no tener que ir a una oficina. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente completa la biometría con el proveedor externo y carga certificación bancaria y extractos de los últimos 3 meses, todo desde el flujo móvil de onboarding. |
| **Relaciones** | Casos de uso: CU-004, CU-005. |
| **Referencias** | [Procesos](../negocio/procesos/03-validacion-kyc.md); `b2b/fliipa-back/src/controllers/clients/upload-document.ts` *(ruta corregida)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Parcialmente verificable**: `upload-document.ts` solo acepta dos tipos de documento (`id_document`, `bank_certificate`); no hay lógica de "extractos de los últimos 3 meses" como conjunto separado ni llamada a un proveedor de biometría en este controlador ni en ningún otro archivo del repositorio (se buscó explícitamente "biometr*" y "Olimpia" en todo `b2b/`, sin resultados). El criterio de aceptación tal como está redactado **excede lo que el código respalda**; se recomienda ajustar la historia o confirmar que la biometría vive en un microservicio no incluido en este repositorio. |

#### HU-005: Conocer el resultado en máximo 24 horas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero conocer el resultado de mi solicitud en máximo 24 horas, para poder planear mis compras en D1. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente recibe notificación de aprobación o rechazo dentro de las 24 horas siguientes a completar la validación de identidad. |
| **Relaciones** | Casos de uso: CU-006. Requerimientos: RF-010, RF-011, RF-012. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/01-cupo-credito.md); `b2b/services/evaluations/src/third-party/Experian/authentication-experian.ts`, `midecisorpj.ts`, `reconocer.ts` *(referencia corregida y ampliada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmada**en el microservicio `b2b/services/evaluations`, que autentica contra Experian y consulta el score (`midecisorpj`) y la identidad (`reconocer`). El controlador `b2b/fliipa-back/src/controllers/institutions/get-advance-score.ts` actúa como proxy hacia ese microservicio vía `evaluationsClient`. La referencia a **Datacrédito** debe interpretarse con cautela: la evidencia revisada no permite concluir que corresponda a un segundo buró independiente utilizado en paralelo con Experian. Se mantiene como una integración técnica pendiente de precisar con el equipo responsable. No se encontró, en cambio, un job o temporizador que garantice el SLA de 24 horas; ese plazo parece ser un compromiso operativo/de negocio, no una regla codificada. |

#### HU-006: Firmar contrato

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero firmar mi contrato desde cualquier Dispositivo con un código de verificación, para activar mi cupo sin papeleo físico. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente revisa el contrato, recibe un Codigo para realizar la firma, válido por 24 horas, y el sistema genera el PDF firmado y lo envía por correo. |
| **Relaciones** | Casos de uso: CU-007. Requerimientos: RF-013, RF-014. |
| **Referencias** | `b2b/fliipa-back/src/controllers/otp/send-signature-otp.ts`, `clients/sign-contract.ts`, `send-contract/send-contract.controller.ts` *(ruta corregida; se agrega referencia de envío)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Confirmado: existen controladores dedicados para la firma del contrato y envío del contrato. El bloqueo de 24 horas tras agotar intentos (RNF-013) no se verificó a nivel de constante exacta en esta revisión; se recomienda una revisión técnica puntual de `config/constants.ts` para confirmar el valor. |

#### HU-007: Consultar cupo, plan de pagos y movimientos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero consultar mi cupo disponible, mi plan de pagos y mis movimientos, para saber cuánto puedo usar y cuánto debo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente accede al portal de usuarios y visualiza cupo disponible, plan de pagos y movimientos, solo si su línea de crédito está en estado Aprobado o Activa. |
| **Relaciones** | Casos de uso: CU-009. Requerimientos: RF-016, RF-017. |
| **Referencias** | `b2b/fliipa-back/src/controllers/credit-line/get-credit-status.ts`, `credit-line/get-disbursements.ts`; `b2b/fliipa-redemption/actions/auth.ts` *(ruta corregida; antes: `backends/b2b/...`, `apps/redemption/...`)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-10 / 1.0 |
| **Comentarios** | Los endpoints de estado de crédito y desembolsos existen y delegan en un cliente del core bancario (`coreApiClient`). La restricción exacta a estados `approved`/`active` no se verificó línea por línea en esta pasada; se recomienda confirmarla en la capa de autenticación de `fliipa-redemption/actions/auth.ts`. |

#### HU-008: Usar el cupo en tienda D1

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero generar un código de compra para usar mi cupo en la tienda D1, para pagar mi mercancía sin dinero en efectivo. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente obtiene un código de compra y el punto de venta D1 lo valida para aplicar el cupo a la compra. |
| **Relaciones** | Casos de uso: CU-010. Requerimientos: RF-019, RF-020. |
| **Referencias** | `b2b/fliipa-back/src/controllers/qr/get-or-create-qr.ts`, `qr/validate-qr.ts`, `clients/get-client-coupon.ts` *(ruta corregida)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección v1.5:** La historia se limita al código de compra/cupón, que sí cuenta con referencia funcional en el repositorio. |

#### HU-009: Pagar por débito automático o prepago

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero que mi cuota se debite automáticamente o poder prepagar por PSE, para no tener que hacer trámites adicionales de pago. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El sistema debita automáticamente vía Druo en la fecha de corte, o permite prepago voluntario por PSE en cualquier momento antes del corte. |
| **Relaciones** | Casos de uso: CU-011. Requerimiento: RF-022. |
| **Referencias** | [Procesos](../negocio/procesos/08-cobro-pago.md); `b2b/fliipa-back/src/services/druo/debit-bank-account.druo.ts`, `connect-bank-account.druo.ts`; `b2b/services/webhooks/src/controllers/webhooks/druo-events.webhook.ts` *(referencia ampliada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | El débito automático vía Druo **sí está implementado** (conexión de cuenta, débito, webhook de eventos). La ejecución real de **prepago por PSE no se encontró** en ningún archivo del repositorio (se buscó "PSE" en todo el proyecto sin coincidencias reales). Se mantiene como pendiente de confirmar con el equipo técnico. |

#### HU-010: Recibir alivios ante dificultades de pago

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recibir alivios (abono parcial, congelamiento de intereses) cuando tengo dificultades temporales de pago, para no perder mi cupo ni mi historial. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente puede acceder al abono parcial, congelamiento de intereses o condonación, según las condiciones y topes definidos por bucket de mora. |
| **Relaciones** | Casos de uso: CU-013. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/03-alivios-negociacion.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **No se encontró ningún módulo de alivios, condonación ni "bucket de mora" en el código revisado** (se buscó "bucket", "mora", "condona*", "alivio*" en todo el repositorio; sin coincidencias relevantes — únicamente coincidencias de "bucket" de almacenamiento GCP, sin relación con cartera). Esta funcionalidad parece no estar implementada en el código fuente entregado, o vive en un sistema externo/manual. Se recomienda confirmar con negocio. |

#### HU-011: Resolver dudas por WhatsApp con respuesta inmediata

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero resolver mis dudas o reclamos por WhatsApp con respuesta inmediata, para no depender de canales lentos o presenciales. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | *Un asistente virtual* atiende el primer contacto y, si no resuelve el caso, escala a un agente humano con el contexto completo. |
| **Relaciones** | Casos de uso: CU-014. Requerimientos: RF-028, RF-029. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md); `b2b/services/communications/src/controllers/whatsapp/whatsapp.controller.ts` *(referencia agregada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | El microservicio `communications` existe, pero sus controladores están limitados a envío de OTP, firma y contrato por WhatsApp/correo; **no hay ningún módulo de asistente conversacional de IA ni lógica de escalamiento a agente humano en el código revisado**. Se confirma el comentario original: probablemente vive en una herramienta externa (p. ej. un proveedor de chatbot) no incluida en este repositorio. |

#### HU-012: Recuperar PIN o desbloquear la cuenta

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero recuperar mi PIN si lo olvido o mi cuenta se bloquea, para no perder el acceso a mi cupo. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El cliente debe comunicarse con Soporto para recibir ayuda y generar un nuevo Pin. |
| **Relaciones** | Requerimiento: RNF-014 (bloqueo de acceso). |
| **Referencias** | `b2b/fliipa-back/src/db/models/Client.ts` (`loginAttempts`, `lockedAt`); `b2b/fliipa-redemption/components/pages/login/ResetPin.tsx` *(ruta corregida y ampliada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Confirmado y ampliado**: además del modelo con `loginAttempts`/`lockedAt`, existe un componente de UI dedicado (`ResetPin.tsx`) dentro del flujo de login de `fliipa-redemption`, lo que da mayor respaldo a esta historia que en la versión anterior. |

### Asesor comercial

#### HU-013: Contacto simultáneo multicanal

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero contactar simultáneamente por correo, WhatsApp y llamada a los clientes preaprobados, para maximizar la tasa de respuesta. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El asesor cuenta con la base de clientes preaprobados y las plantillas de contacto por los tres canales. |
| **Relaciones** | Casos de uso: CU-001. Requerimiento: RF-001. Historia relacionada: HU-001. |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md); `b2b/services/rules-engine/src/db/repositories/get-clients.ts` *(referencia agregada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Existe una base de clientes preaprobados en `rules-engine` (`get-clients.ts`, `get-evaluation-clients.handler.ts`), pero no se encontró una herramienta de contacto multicanal orquestada para el asesor (llamadas, plantillas) en el código; probablemente es un proceso manual o de una herramienta externa (CRM). |

#### HU-014: Acompañar la originación del cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero acompañar al cliente durante la originación (dudas, Preguntas o inquietudes), para reducir el abandono del proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El asesor realiza seguimiento remoto al cliente durante el proceso de onboarding, atiende sus dudas e inquietudes y brinda orientación cuando sea necesario. El seguimiento se realiza mediante los canales definidos para la gestión comercial, sin requerir visitas presenciales. |
| **Relaciones** | Casos de uso: CU-001. |
| **Referencias** | [Actores](../negocio/Actores/03-actores-comerciales-cobranza.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin cambios: es un proceso operativo/humano, no se esperaba ni se encontró respaldo directo en código. |

#### HU-015: Seguimiento de primera compra

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Asesor comercial |
| **Historia** | Como asesor comercial, quiero identificar a los clientes que no han usado su cupo 7 días después de la activación, para hacer seguimiento de primera compra. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El asesor recibe o consulta la lista de clientes activados sin uso del cupo a los 7 días. |
| **Relaciones** | — |
| **Referencias** | [Procesos](../negocio/procesos/01-captacion-comercial.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-10 / 1.0 |
| **Comentarios** | Confirmado: no se encontró ningún reporte automatizado de este seguimiento en el código revisado. |

### Analista de riesgo

#### HU-016: Resolver manualmente casos de biometría en revisión

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero revisar manualmente los casos de biometría marcados "en revisión", para decidir si el cliente puede continuar el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista visualiza los casos "en revisión" y registra la decisión (continuar o rechazar). |
| **Relaciones** | Casos de uso: CU-005. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/07-kyc-evaluacion-riesgo.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Nuevo hallazgo (v1.3)**: no se encontró en el código ningún estado de "en revisión" para biometría, ni una cola o pantalla de revisión manual (se buscó "en_revision", "manual_review", "under_review" en todo el repositorio, sin coincidencias). Esta historia no tiene respaldo verificable en el código fuente entregado; se recomienda confirmar si el flujo de biometría vive en un sistema externo (proveedor de biometría) no incluido en este repositorio. |

#### HU-017: Ver score, Experian e histórico D1 en un solo lugar

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de riesgo |
| **Historia** | Como analista de riesgo, quiero ver en un solo lugar el resultado de Experian, el histórico transaccional de D1 y el score calculado, para validar o ajustar la decisión automática. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta, para un cliente dado, el resultado de Experian, el histórico D1 y el score consolidado antes de aprobar o rechazar. |
| **Relaciones** | Casos de uso: CU-006. Requerimiento: RF-010. |
| **Referencias** | `b2b/fliipa-back/src/controllers/companies/lookup-company.ts`, `institutions/get-advance-score.ts`; `b2b/services/evaluations/src/third-party/Experian/*` *(ruta corregida y ampliada)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** |  la integración con Experian **sí existe** en el código (microservicio `evaluations`); Lo que sí sigue sin encontrarse es una pantalla o endpoint que **consolide en un solo lugar** Experian + histórico D1 + score para el analista; cada dato se consulta por endpoints separados. Recomendamos aclarar si esa consolidación visual es responsabilidad del portal administrativo (ver hallazgo crítico al final del documento). |

### Analista de cartera / Comité de Cartera

#### HU-018: Ver cartera segmentada por bucket de mora

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero ver la cartera segmentada por bucket de mora, para priorizar mi gestión de cobro diaria. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista consulta la cartera agrupada en pago anticipado y buckets 1 a 5, con los datos necesarios para priorizar su gestión. |
| **Relaciones** | Casos de uso: CU-012. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/02-mora-buckets.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-10 / 1.0 |
| **Comentarios** | El motor de reglas (`rules-engine`) que sí existe está enfocado en preaprobación, no en cobranza. Esta historia **no está respaldada por el código fuente entregado**; se recomienda validar si vive en un sistema externo de cobranza. Se mantiene la nota sobre la discrepancia de plazos de escalamiento documentada en RNF-017. |

#### HU-019: Registrar cada interacción de cobranza

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista de cartera |
| **Historia** | Como analista de cartera, quiero registrar cada interacción de cobranza (canal, tipo de contacto, resultado, compromiso de pago), para mantener trazabilidad completa del caso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El analista registra canal, tipo de contacto, resultado y monto comprometido de cada interacción, quedando disponible en el resumen de atención del cliente. |
| **Relaciones** | Casos de uso: CU-012. Requerimientos: RF-025, RF-026. |
| **Referencias** | `b2b/fliipa-back/src/controllers/clients/collection-notes.ts` *(ruta corregida)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-10 / 1.0 |
| **Comentarios** | **Confirmado**: el módulo está completamente implementado — creación, edición, eliminación y listado de notas de cobranza, más un resumen de atención (`getCollectionNotesAttentionSummary`). Sigue sin estar descrito explícitamente en el alcance de producto revisado. |

#### HU-020: Tablero semanal de priorización del Comité de Cartera

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Comité de Cartera |
| **Historia** | Como miembro del Comité de Cartera, quiero un tablero semanal con los casos priorizados (días de mora, monto, historial), para decidir alivios o escalamiento jurídico. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El comité visualiza semanalmente los casos priorizados según días de mora, flujo de caja, cuota vencida, historial y monto adeudado. |
| **Relaciones** | Casos de uso: CU-012, CU-013. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/04-gestion-escalamiento.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-10 / 1.0 |
| **Comentarios** | Confirmado: no se encontró ningún tablero de priorización automatizado en el código revisado. Depende de la misma ausencia de lógica de mora/buckets señalada en HU-018. |

#### HU-021: Recibir casos de escalamiento jurídico automáticamente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Analista jurídico / abogado |
| **Historia** | Como analista jurídico, quiero recibir automáticamente los casos que llegan al bucket de escalamiento legal, para iniciar el proceso de cobro jurídico sin depender de un traspaso manual. |
| **Prioridad** | Media |
| **Criterios de aceptación** | Los casos que alcanzan el bucket de escalamiento jurídico se enrutan automáticamente al analista jurídico. |
| **Relaciones** | — |
| **Referencias** | [Actores](../negocio/Actores/03-actores-comerciales-cobranza.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | Sin respaldo en código (consistente con la ausencia general de lógica de buckets de mora, ver HU-018). Depende de resolver primero la discrepancia de plazos de escalamiento (RNF-017). |

### Agente de servicio al cliente

#### HU-022: Recibir el caso escalado con contexto completo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero recibir el caso escalado por la IA con el contexto completo de la conversación, para no pedirle al cliente que repita su problema. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando la IA escala un caso, el agente humano ve el historial completo de la conversación antes de responder. |
| **Relaciones** | Casos de uso: CU-014. Requerimiento: RF-028. |
| **Referencias** | [Reglas Negocio](../negocio/reglas-negocio/09-servicio-cliente.md) |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-10 / 1.0 |
| **Comentarios** | Confirmado (ver HU-011): no existe módulo de IA conversacional ni de escalamiento en el código de `communications` ni en ningún otro servicio revisado. |

#### HU-023: Validar identidad en casos críticos

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

### Administrador del producto (portal administrativo)

#### HU-024: Buscar cliente y ver historial auditado

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero buscar un cliente por documento y ver su historial completo de operaciones auditadas, para resolver dudas o disputas rápidamente. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador busca por documento y consulta hasta 500 registros de auditoría del cliente (línea de crédito, desembolsos, pagos). |
| **Relaciones** | Casos de uso: CU-015. Requerimientos: RF-030, RF-031. |
| **Referencias** | `backends/admin/src/controllers/clients.controller.ts` (`getClientAuditedOperations`) — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Corrección respecto a v1.3**: implementada. El controlador `getClientAuditedOperations` en `backends/admin` sí existe y expone el historial auditado por cliente. |

#### HU-025: Ajustar cupo o fecha de corte

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero ajustar el cupo o la fecha de corte de una línea de crédito, para corregir casos excepcionales autorizados por negocio. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador puede ajustar dentro de los rangos válidos, quedando la acción registrada en auditoría. |
| **Relaciones** | Casos de uso: CU-015. Requerimiento: RF-018. |
| **Referencias** | `backends/admin/src/controllers/credit-lines.controller.ts` — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-30 / 1.1 |
| **Comentarios** | **Corrección respecto a v1.3**: implementada. Se confirma también el hallazgo de RF-018: el admin acepta `cutoffDay` en rango 0–31, mientras que redemption exige 1–31 — discrepancia real entre ambos módulos. |

#### HU-026: Simular plan de pago con distintas tasas

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero simular el plan de pago de un cliente en mora con distintas tasas, para preparar acuerdos de pago o alivios. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador ingresa tasa corriente, tasa de mora y umbral de días, y obtiene el plan de pago diario descargable en CSV. |
| **Relaciones** | Casos de uso: CU-016. Requerimiento: RF-024. |
| **Referencias** | `backends/admin/src/controllers/calculator.controller.ts` (`getCalculatorStatus`, recibe `currentInterestRate`, `overdueInterestRate`, `thresholdDays`); descarga CSV en `apps/admin/src/lib/generate-csv-file.ts` y `apps/admin/src/app/disbursements/consult/CalculatorDownloaderButton.tsx` — confirmado en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-30 / 1.1 |
| **Comentarios** | **Corrección respecto a v1.3**: implementada, exactamente con los campos descritos en la historia (tasa corriente, tasa de mora, umbral de días) y con descarga CSV real. |

#### HU-027: Administrar la lista negra (blacklist)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero agregar o retirar clientes de la lista negra, para bloquear casos de fraude confirmado. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El administrador agrega o retira clientes de la blacklist, validando que el cliente exista. |
| **Relaciones** | Casos de uso: CU-017. Requerimiento: RF-027. |
| **Referencias** | `backends/b2b/src/controllers/blacklist/add-client-to-blacklist.ts`, `backends/b2b/src/controllers/blacklist/remove-client-client-from-blacklist.ts` *(ruta corregida a `credits-platform-main`)* |
| **Autor / Fecha / Versión** | María Fernanda Herazo |
| **Comentarios** | **Nota**: a diferencia de HU-024/025/026/028, esta historia sí tenía respaldo real desde la v1.3, pero en `backends/b2b` — **no en un backend administrativo separado**. Se confirma el hallazgo original: no hay enforcement de la blacklist sobre checkout, evaluación de riesgo o desembolso en ningún archivo del repositorio (`blacklists` solo aparece como relación de lectura en `get-client-by-id.service.ts`, sin ninguna validación bloqueante). Este es un riesgo de negocio real y verificado. |

#### HU-028: Monitorear salud del sistema en tiempo real

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador con rol de sistema (SYS_ADMIN) |
| **Historia** | Como administrador con rol de sistema, quiero ver el estado del core bancario y de la base de datos en tiempo real, para detectar incidentes antes de que afecten a los clientes. |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador de sistema consulta latencia y disponibilidad del core bancario y de Cloud SQL desde el panel. |
| **Relaciones** | Casos de uso: CU-018. Requerimiento: RF-033. |
| **Referencias** | `backends/admin/src/controllers/system-core-health.controller.ts`, `system-cloud-sql.controller.ts` — confirmados en `credits-platform-main`. |
| **Autor / Fecha / Versión** | María Fernanda Herazo (con asistencia de Claude) / 2026-07-30 / 1.1 |
| **Comentarios** | **Corrección respecto a v1.3**: implementada, con un hallazgo adicional (ver RF-033): el monitoreo de terceros solo cubre GitHub, npm y GCP; no cubre Experian, Druo, el proveedor de biometría, Zenvia/Sendgrid ni el core bancario, a pesar de que la historia y el alcance del producto los describen como críticos para el negocio. |

## Conclusión de la revisión

La revisión de las historias de usuario permitió confirmar los principales hallazgos identificados en versiones anteriores y detectar algunos puntos que requerían actualización para mantener la documentación alineada con el repositorio vigente y con la definición funcional del producto.

## Fuentes consultadas

- [Actores](../negocio/Actores/README.md)
- [Procesos](../negocio/procesos/README.md)
- [Reglas Negocio](../negocio/reglas-negocio/README.md)
- [Casos De Uso](casos-de-uso.md)
- [Requerimientos Funcionales](requerimientos-funcionales.md)
- [Requerimientos No Funcionales](requerimientos-no-funcionales.md)
- Inventario funcional del código fuente `credits-platform-main` (base de la v1.0-1.2).
- La revisión de esta versión toma como referencia el repositorio `credits-platform-main`; los snapshots anteriores de `fliipa-main` se conservan únicamente como antecedente de las versiones previas.
- **Revisión directa del código fuente del repositorio `credits-platform-main.zip`** (incluyendo `backends/admin`, `backends/b2b`, `apps/admin`, `apps/checkout`, `apps/redemption`, `services/core/*`, `services/product/*`, `gateways/core-hub`), realizada como parte de la corrección v1.4. Este es el repositorio de código de referencia vigente.
