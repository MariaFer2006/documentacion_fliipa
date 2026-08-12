# 8. Cobranza

## Objetivo

Gestionar la recuperación de la cartera vencida mediante un proceso escalonado que inicia con el cobro automático, continúa con acciones preventivas y de negociación, y finaliza con el escalamiento a procesos jurídicos cuando el cliente no regulariza su obligación.

---

## Journey

![Journey Colpatria B2B — página 10](imagenes/page-10.png)

**Figura 12. Journey de Cobranza.**

El journey se organiza en cuatro carriles (swimlanes): **Cliente**, **Sistema**, **Analista de cobranza** y **Legal/Jurídico**. Las cajas "Se envía WhatsApp/SMS..." y "Reporta a centrales de riesgo..." están marcadas como ajustes de junio de 2026. La caja "Se acuerda un castigo parcial con cancelación del cupo de crédito" está marcada en **rojo (Alto)** en la escala de puntos de fricción del journey — es decir, el propio diagrama la señala como uno de los puntos de mayor fricción de todo el proceso.

*Los elementos marcados con asterisco (\*) corresponden a puntos aún no definidos técnicamente o pendientes de confirmación con el dueño del proceso; se detallan en cada paso y se listan de forma consolidada en "Pendientes de validación".*

---

## Descripción general

Cuando el cliente no realiza el pago antes de la fecha de corte, el sistema intenta recaudar automáticamente mediante débito con Druo (día 0). Si el recaudo falla, se realiza un nuevo intento durante los primeros días de mora (días 1-5) y, si también falla, se inicia una gestión preventiva mediante WhatsApp/SMS (días 6-15) que ya incluye un **preaviso legal**: informa que, de no regularizar, la obligación será reportada a centrales de riesgo en 15 días.

El cliente puede pagar en cualquier momento a través del mismo enlace de pago por PSE — este enlace es un punto de pago compartido al que el flujo vuelve tanto si el cliente responde al mensaje preventivo, como si acepta pagar tras la llamada del analista, o si acepta las condiciones de una restructuración. Si el pago por PSE falla o el cliente no responde, el analista de cobranza lo contacta telefónicamente (días 6-15) con un guion estandarizado, bloqueando el cupo de crédito en ese momento. Si el cliente acepta negociar, se formaliza una restructuración, un acuerdo de pago, o —en el escenario de mayor fricción del proceso— un castigo parcial con cancelación del cupo (días 16-30). Si el cliente no acepta las condiciones o continúa sin pagar, la obligación se reporta a centrales de riesgo (día 15 de mora, equivalente al día 45 del crédito) y, si la recuperación administrativa no es posible, se aplica el castigo de cartera y el caso escala a cobro jurídico. De forma independiente a la ruta seguida, el cupo queda bloqueado de forma **permanente** al llegar al día 30 de mora.

---

## Explicación paso a paso

### 1. Inicio de la mora

**Actor:** Sistema.

**Sistemas involucrados:** Plataforma de crédito; sistema de recaudo.

**Información utilizada:** Fecha de corte, estado del crédito, valor pendiente de pago.

**Proceso:** El sistema detecta que el cliente no realizó el pago correspondiente antes de la fecha de corte establecida para su crédito, y dispara automáticamente el inicio del proceso de cobranza.

**Resultado:** Proceso de cobranza iniciado automáticamente.

**Tiempo:** Día 0 (fecha de corte).

---

### 2. Primer intento de débito automático

**Actor:** Sistema / Druo.

**Sistemas involucrados:** Druo, plataforma de recaudo.

**Información utilizada:** Cuenta bancaria registrada; valor de la cuota.

**Proceso:** El sistema activa el débito automático con Druo utilizando la cuenta bancaria registrada por el cliente en el onboarding (documento 2).

**Decisión:** ¿El débito automático fue exitoso?

- **Sí:** el pago queda registrado. Finaliza el proceso de cobranza.
- **No:** se programa un nuevo intento de recaudo.

**Resultado:** Pago recaudado, o reintento programado.

**Tiempo:** Día 0.

---

### 3. Reintento de débito automático

**Actor:** Sistema / Druo.

**Sistemas involucrados:** Druo, plataforma de recaudo.

**Información utilizada:** Estado del intento anterior; cuenta bancaria registrada.

**Proceso:** Durante los primeros días de mora, el sistema realiza un nuevo intento de recaudo automático con Druo sobre la misma cuenta.

**Decisión:** ¿El reintento fue exitoso?

- **Sí:** el pago queda registrado. El proceso finaliza.
- **No:** se continúa con la gestión preventiva de cobranza.

**Resultado:** Pago recaudado, o escalamiento a gestión preventiva.

**Tiempo:** Días 1 al 5.

**Placeholder\*:** no está definido si hay más de un reintento dentro de la ventana de días 1-5, ni el intervalo exacto entre reintentos.

---

### 4. Gestión preventiva mediante mensaje (WhatsApp/SMS) con preaviso legal

**Actor:** Sistema.

**Sistemas involucrados:** Plataforma de mensajería; sistema de cobranza.

**Información utilizada:** Estado de mora; datos de contacto; valor pendiente.

**Proceso:** Cuando los intentos automáticos fallan, el sistema envía un mensaje por WhatsApp o SMS que combina dos elementos: (1) la solicitud de pago de la cuota, con el enlace de pago por PSE, y (2) un **preaviso formal**: informa que, si el cliente no regulariza su obligación, esta será reportada a centrales de riesgo en 15 días. El mensaje incluye además una advertencia sobre las consecuencias de mantener la mora.

**Resultado:** Cliente notificado, con enlace de pago y preaviso de reporte a centrales.

**Tiempo:** Días 6 al 15.

> **Nota (Ajuste · jun 2026):** este paso está marcado en el journey como un ajuste de junio de 2026.

---

### 5. Pago por PSE (punto de pago compartido)

**Actor:** Cliente.

**Sistemas involucrados:** Plataforma PSE; sistema de recaudo.

**Información utilizada:** Enlace de pago; valor pendiente.

**Proceso:** El cliente utiliza el enlace recibido para pagar la obligación por PSE. **Este mismo punto de pago es reutilizado en varios momentos del journey**: el cliente puede llegar a él directamente desde el mensaje preventivo (paso 4), después de aceptar pagar durante la llamada del analista (paso 6), o después de aceptar las condiciones de una restructuración o acuerdo de pago (paso 7) — en todos los casos, el pago efectivo se realiza a través de este mismo enlace de PSE.

**Decisión:** ¿El pago fue exitoso?

- **Sí:** el pago queda registrado. Finaliza el proceso de cobranza.
- **No:** el caso continúa hacia la gestión telefónica del analista.

**Resultado:** Pago recaudado, o escalamiento a gestión telefónica.

**Tiempo:** Variable — el cliente puede usar este enlace en cualquier punto desde el día 6 en adelante, incluso después de una negociación posterior.

---

### 6. Gestión telefónica del analista

**Actor:** Analista de cobranza.

**Sistemas involucrados:** Portal administrativo; sistema de cartera.

**Información utilizada:** Historial del crédito; días de mora; resultado de las gestiones anteriores.

**Proceso:** El analista de cobranza contacta al cliente utilizando un guion estandarizado para identificar la causa del incumplimiento. Durante esta gestión, el sistema **bloquea el cupo de crédito** y el analista refuerza la advertencia sobre las consecuencias de mantener la mora.

**Resultado:** Se determina si el cliente acepta negociar la obligación. Si acepta pagar, vuelve al punto de pago por PSE (paso 5); si no, el caso continúa hacia restructuración o reporte.

**Tiempo:** Días 6 al 15.

**Placeholder\*:** no está definido el guion estandarizado en detalle, ni el número de intentos de contacto telefónico dentro de esta ventana.

---

### 7. Restructuración, acuerdo de pago, o castigo parcial

**Actor:** Analista de cobranza / Sistema de cartera.

**Información utilizada:** Capacidad de pago; estado del crédito; política de cartera.

**Proceso:** Si el cliente acepta negociar, se formaliza una de dos alternativas:

- **Restructuración o acuerdo de pago:** el cliente acepta condiciones y, al aceptarlas, es dirigido nuevamente al enlace de pago por PSE (paso 5) para efectuar el pago acordado.
- **Castigo parcial con cancelación del cupo de crédito:** alternativa marcada explícitamente en el journey como punto de **fricción Alta**. Implica que el cliente pierde definitivamente su cupo de crédito como parte del acuerdo.

Si el cliente **no** acepta las condiciones ofrecidas, el caso continúa hacia el reporte a centrales de riesgo (paso 8).

**Resultado:** Acuerdo formalizado (con retorno al pago por PSE), castigo parcial aplicado, o escalamiento hacia reporte a centrales.

**Tiempo:** Días 16 al 30.

**Placeholder\*:** no están definidos los criterios exactos para ofrecer restructuración/acuerdo de pago frente a castigo parcial (¿depende del monto en mora, del historial del cliente, o de ambos?), ni el detalle de qué implica exactamente la "cancelación del cupo" en el castigo parcial (¿cancelación total e inmediata, o progresiva?).

---

### 8. Reporte a centrales de riesgo

**Actor:** Sistema.

**Sistemas involucrados:** Plataforma de reporte a centrales.

**Información utilizada:** Días de mora; estado de la obligación.

**Proceso:** Si el cliente no acepta las condiciones de negociación o continúa sin pagar, la obligación se reporta a las centrales de riesgo. El journey precisa este momento con dos referencias equivalentes: **día 15 de mora**, que corresponde al **día 45 del crédito** (contando desde el origen del crédito, no solo desde el inicio de la mora) — esto es consistente con el preaviso enviado en el paso 4 (mensaje que ya anunciaba el reporte a 15 días).

**Resultado:** Reporte registrado en las centrales de riesgo.

**Tiempo:** Días 16 al 30 (referencia puntual: día 15 de mora / día 45 del crédito).

> **Nota (Ajuste · jun 2026):** este paso está marcado en el journey como un ajuste de junio de 2026.

---

### 9. Bloqueo permanente del cupo

**Actor:** Sistema.

**Proceso:** De forma independiente a la ruta seguida (restructuración, castigo parcial o reporte), cuando la mora alcanza el **día 30**, el sistema bloquea el cupo de crédito de forma **permanente**.

**Resultado:** Cupo bloqueado de manera definitiva para ese cliente.

**Tiempo:** Día 30 de mora.

**Placeholder\*:** no está confirmado si este bloqueo permanente aplica incluso a clientes que ya formalizaron una restructuración o acuerdo de pago (paso 7), o únicamente a quienes no regularizaron su obligación.

---

### 10. Castigo de cartera y cobro jurídico

**Actor:** Sistema de cartera / Área Jurídica.

**Sistemas involucrados:** Sistema de cartera; sistema jurídico.

**Información utilizada:** Historial de mora; gestión realizada; política de recuperación.

**Proceso:** Cuando las acciones de cobranza administrativa no permiten recuperar la obligación, se aplica el castigo de cartera definido por la organización y el caso se transfiere al Área Jurídica, que inicia el cobro jurídico para la recuperación de la obligación.

**Resultado:** Proceso jurídico de recuperación iniciado. Con esta actividad concluye el journey de cobranza.

**Tiempo:** Posterior al día 30, sin un límite superior definido en el journey.

**Placeholder\*:** no está definido el tiempo máximo o el criterio exacto que determina cuándo se aplica el castigo de cartera después del reporte a centrales (paso 8).

---

## Actores involucrados

| Actor | Rol dentro del proceso |
|--------|------------------------|
| Cliente | Realiza el pago del crédito, responde a las gestiones de cobranza y puede aceptar acuerdos de pago para normalizar su obligación. |
| Sistema de cobranza | Ejecuta automáticamente los intentos de recaudo, envía notificaciones (incluyendo el preaviso legal) y controla el avance del proceso según los días de mora. |
| Druo | Procesa los débitos automáticos desde la cuenta bancaria registrada por el cliente. |
| Analista de cobranza | Contacta al cliente, identifica la causa de la mora, negocia acuerdos de pago (o castigo parcial) y realiza el seguimiento de la recuperación de la cartera. |
| Plataforma PSE | Permite al cliente realizar el pago mediante el enlace enviado durante la gestión de cobranza, reutilizado en varios puntos del journey. |
| Centrales de riesgo | Reciben el reporte de la obligación cuando la mora cumple las condiciones definidas por la política de crédito (día 15 de mora / día 45 del crédito). |
| Área Jurídica | Gestiona el proceso de recuperación judicial cuando las acciones de cobranza no logran normalizar la obligación. |

---

## Reglas de negocio

- El proceso inicia automáticamente cuando el cliente no realiza el pago en la fecha de corte.
- El sistema realiza un intento inicial de recaudo mediante débito automático con Druo (día 0), seguido de un reintento (días 1-5).
- La gestión preventiva (días 6-15) incluye notificaciones por WhatsApp o SMS que ya contienen un preaviso formal de reporte a centrales en 15 días.
- El cliente puede regularizar la obligación mediante PSE en cualquier momento desde el día 6 en adelante, incluso después de haber negociado una restructuración.
- El analista de cobranza puede negociar restructuraciones, acuerdos de pago, o —como alternativa de mayor fricción— un castigo parcial con cancelación del cupo.
- El cupo de crédito se bloquea durante la gestión telefónica del analista (días 6-15) y queda bloqueado de forma **permanente** al llegar al día 30 de mora, independientemente de la ruta seguida.
- El reporte a centrales de riesgo ocurre en el día 15 de mora, equivalente al día 45 del crédito.
- Cuando no es posible recuperar la obligación mediante cobranza administrativa, el caso se remite a recuperación jurídica.

---

## Entradas

- Crédito con pago vencido.
- Fecha de corte.
- Cuenta bancaria registrada.
- Información del cliente.
- Estado de la cartera.

---

## Salidas

- Pago exitoso del crédito.
- Acuerdo de pago, restructuración, o castigo parcial con cancelación del cupo.
- Reporte a centrales de riesgo.
- Bloqueo permanente del cupo (día 30 de mora).
- Castigo de cartera.
- Inicio del proceso de recuperación jurídica.

---

## Excepciones

- El débito automático falla.
- El cliente no realiza el pago mediante PSE.
- El cliente rechaza la negociación propuesta.
- Se aplica bloqueo permanente del cupo por política de mora (día 30).
- La obligación debe escalar al proceso jurídico para su recuperación.

---

## Consideraciones

- El enlace de pago por PSE es un **punto de pago compartido**: el journey lo reutiliza como destino común tanto desde el mensaje preventivo como después de aceptar pagar en la llamada del analista o de aceptar una restructuración, en lugar de ser un paso único y lineal.
- El castigo parcial con cancelación del cupo está señalado explícitamente en el journey como el punto de **mayor fricción (Alto)** de todo el proceso de cobranza — un dato relevante para priorizar mejoras de experiencia o alternativas antes de llegar a ese punto.
- El reporte a centrales de riesgo tiene dos referencias temporales equivalentes en el journey (día 15 de mora / día 45 del crédito), consistentes con el preaviso enviado en la gestión preventiva.
- El bloqueo permanente del cupo al día 30 de mora aplica de forma transversal, independiente de si el cliente negoció o no una restructuración — esto debe confirmarse con el dueño del proceso.
- Este proceso se conecta directamente con el documento 5 (Calculadora y Cobro del Crédito), que ya señalaba el mecanismo de débito automático con Druo y advertía sobre la necesidad de alinear los reintentos de ambos procesos para evitar duplicidad.

---

## Pendientes de validación

> **Pendiente de validar con el dueño del proceso:**
>
> - Confirmar si hay más de un reintento de débito automático dentro de la ventana de días 1-5, y el intervalo exacto entre reintentos. *(placeholder — paso 3)*
> - Confirmar el guion estandarizado de la llamada del analista y el número de intentos de contacto telefónico permitidos. *(placeholder — paso 6)*
> - Confirmar los criterios exactos para ofrecer restructuración/acuerdo de pago frente a castigo parcial, y qué implica técnicamente la cancelación del cupo en ese escenario. *(placeholder — paso 7)*
> - Confirmar si el bloqueo permanente del cupo (día 30 de mora) aplica también a clientes que ya formalizaron una restructuración o acuerdo de pago. *(placeholder — paso 9)*
> - Confirmar el tiempo máximo o criterio que determina cuándo se aplica el castigo de cartera después del reporte a centrales de riesgo. *(placeholder — paso 10)*
> - Alinear los reintentos de débito automático con Druo de este proceso con los ya descritos en el documento 5 (Calculadora y Cobro del Crédito), para evitar reintentos duplicados o contradictorios.

---

## Fuentes consultadas

- *Journeys Colpatria B2B* (junio de 2026), página 10.
- Documento de Alcance del Producto.
