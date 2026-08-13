# 5. Dispersión de fondos

## Objetivo

Gestionar el desembolso de los recursos del crédito desde la fiducia hacia D1, emitir el bono correspondiente al cupo aprobado, registrar el uso del crédito por parte del cliente y administrar el retorno de los pagos hacia la fiducia.

> **Actualización (Acta de reunión Check-in, 29 jul 2026):** el equipo acordó separar la evaluación de renovación del cupo de este flujo de dispersión inicial. Dicho proceso ahora se documenta de forma independiente en un nuevo capítulo, **Flujo de Recurrencia**, a cargo de María Fernanda Herazo. El alcance de este documento queda enfocado exclusivamente en el ciclo inicial: fondeo, desembolso, emisión y uso del bono, y pago del crédito.

---

## Journey

![Journey Colpatria B2B — página 8](imagenes/page-08.png)

**Figura 8. Journey de Dispersión de Fondos.**

Este journey describe el flujo financiero del crédito una vez ha sido aprobado y firmado. Durante esta etapa se administran los recursos del crédito mediante una cuenta fiduciaria, se realiza el desembolso hacia D1, se emite el bono para el cliente y se registra el pago del crédito. La evaluación de renovación de cupo ya no forma parte de este journey (ver actualización más abajo).

> **⚠️ Pendiente de ajustar en el diagrama antes de presentar:**
> 1. Diferenciar la flecha Colpatria→Fiducia ("Fondeo inicial · único") de la flecha Fiducia→D1 ("Desembolso · 4x1000 por ciclo") — hoy ambas dicen "Desembolso · 4x1000" y pueden leerse como si el GMF se cobrara dos veces por crédito.
> 2. Documentar qué cambió exactamente en junio de 2026 en los dos pasos marcados como "Ajuste · jun 2026" (emisión del bono en D1 y uso del bono por el cliente) — pendiente de confirmar con el dueño del proceso.
> 3. Asignar el nivel de fricción (Bajo/Medio/Alto) a cada paso; ningún paso lo tiene aún pese a que la leyenda del diagrama lo define.
> 4. **(Actualizado, 29 jul 2026)** Eliminar del diagrama de este journey el nodo "¿Evalúa renovación de cupo?" y su rama de retorno al paso 3: por decisión del equipo, ese nodo pasa a formar parte del diagrama del nuevo Flujo de Recurrencia. En este journey, el ciclo debe representarse como finalizado en el paso 5 (pago del crédito).

*Los elementos marcados con asterisco (\*) corresponden a puntos aún no definidos técnicamente o pendientes de confirmación con el dueño del proceso; se detallan en cada paso y se listan de forma consolidada en "Pendientes de validación".*

---

## Descripción general

Una vez el contrato ha sido firmado y el crédito queda activo, Colpatria crea y fondea una **cuenta fiduciaria** desde donde se administran los recursos del piloto (**fondeo inicial, único**, no recurrente por crédito) *el Banco donde se creara la fiducia*.

> **Definición:** Una fiducia es un contrato mediante el cual una entidad fiduciaria administra recursos entregados por Colpatria (el fideicomitente) con una finalidad específica y previamente definida; en este caso, centralizar el fondeo de los desembolsos hacia D1 y el recaudo de los pagos de los clientes. 

Posteriormente la fiducia desembolsa el dinero a D1 para emitir el bono correspondiente al valor del cupo utilizado (**desembolso recurrente, uno por cada ciclo de crédito**).

Cuando el cliente utiliza el bono en una tienda D1, un **worker automatizado**\* (el mismo mecanismo de detección descrito en el documento 4, Calculadora y Cobro del Crédito) detecta la compra y el sistema registra la utilización del crédito, bloqueando el cupo remanente hasta finalizar el ciclo de pago. El bono tiene una **vigencia de 15 días calendario** para ser utilizado por el cliente (ver detalle en el paso 4).

Posteriormente el cliente paga su obligación y el dinero retorna nuevamente a la fiducia como cuenta de recaudo este retorno no vuelve a generar GMF adicional.

> **Aclaración :** el dinero recaudado a través de los canales de pago **no se reinvierte en su totalidad** en el fondeo de nuevos créditos. Únicamente el **capital recuperado** vuelve a utilizarse para fondear nuevos créditos; los intereses y demás cargos cobrados al cliente quedan excluidos de esa reinversión.

---

## Explicación paso a paso

Cada paso incluye el **proceso** (qué ocurre técnica u operativamente) y un **tiempo estimado** de referencia, pendiente de validar con Producto/Tecnología/Riesgo.

### 1. Creación y fondeo de la cuenta fiduciaria

**Actor:** Colpatria.

**Proceso:** Colpatria crea una cuenta fiduciaria destinada exclusivamente a administrar los recursos del piloto y la fondea con el capital destinado a los desembolsos. Esta cuenta centraliza tanto la salida del dinero hacia D1 como el retorno de los pagos realizados por los clientes.
*NOTA: El dinero que se recaude a través de los canales de pago no se reinvierte nuevamente en su totalidad en el portafolio; únicamente el capital recuperado se reutiliza para fondear nuevos créditos, excluyendo intereses y otros cargos.*

**Resultado:** Cuenta fiduciaria creada y fondeada, lista para operar los desembolsos del piloto.

**Tiempo estimado:** Actividad de fondeo puntual, **única al inicio de la operación del piloto** (o cuando se requiera reforzar el fondo), no ocurre en cada ciclo de crédito, a diferencia del desembolso hacia D1 (paso 3).

**Placeholder\*:** no está definido el monto exacto del fondo fiduciario ni la periodicidad con la que Colpatria debe reforzarlo a medida que se originan más créditos, ni el banco/entidad fiduciaria específica donde se constituirá la fiducia. **Pendiente para mañana:** llevar una cifra tentativa del monto de fondeo inicial, aunque sea preliminar, para no dejar el punto completamente abierto en la presentación.

---

### 2. Concentración de los fondos

**Actor:** Fiducia.

**Proceso:** Todos los recursos del crédito quedan concentrados en la cuenta fiduciaria, la cual administra tanto el origen del dinero de cada desembolso como el recaudo posterior de los pagos de los clientes. Este diseño reduce el impacto del GMF (4x1000), ya que únicamente se genera el movimiento correspondiente entre la fiducia y D1: por ciclo de $1'000.000 (un giro fiducia → D1), el GMF es de $4.000 (0,4%). Sobre el mismo capital, con 12 ciclos al año, esto equivale a $48.000 (4,8% anual). El retorno del pago del cliente hacia la fiducia (cuenta de recaudo) no genera un nuevo GMF adicional (Acta de reunión Check-in, 29 jul 2026).

**Resultado:** Fondos concentrados y listos para el desembolso hacia D1.

**Tiempo estimado:** Instantáneo (los fondos ya están disponibles en la cuenta fiduciaria).

**Placeholder\*:** si Colpatria crea la fiducia en el mismo banco donde ya tiene los fondos, se ahorra adicionalmente el 4x1000 **del fondeo inicial (paso 1)** — no está confirmado si esta condición (mismo banco) se cumplirá en la implementación definitiva. **Este ahorro aplica únicamente al fondeo inicial, no al desembolso recurrente Fiducia→D1 del paso 3, que sí genera GMF en cada ciclo independientemente del banco.**

---

### 3. Desembolso hacia D1 y emisión del bono

**Actor:** Fiducia / D1.

**Proceso:** Cuando el crédito queda disponible, la fiducia realiza el desembolso del valor aprobado hacia D1 (generando el GMF descrito en el paso 2, **0,4% por cada ciclo de crédito**). D1 recibe los recursos y genera un bono equivalente al valor del cupo, el cual queda disponible para que el cliente realice su compra. En esta etapa todavía no existe una obligación financiera activa hasta que el bono sea utilizado.

**Resultado:** Bono emitido y disponible para el cliente.

**Tiempo estimado:** Instantáneo a segundos (transferencia y generación del bono, una vez el crédito está aprobado y firmado).

**Nota (Ajuste · jun 2026):** este paso está marcado en el journey (página 8) como un ajuste de junio de 2026. *(Pendiente para mañana: confirmar con el dueño del proceso qué cambió exactamente en la emisión del bono en esta actualización, para poder explicarlo si se pregunta en la presentación.)*

---

### 4. Uso del bono por parte del cliente

**Actor:** Cliente / Sistema (worker automatizado).

**Proceso:** El cliente recibe el bono y realiza la compra en una tienda D1. Cuando el **worker automatizado** de consulta de bono detecta una compra realizada, el sistema registra la utilización efectiva del crédito y comienza formalmente el ciclo de vida de la obligación financiera. Aunque el bono queda emitido y disponible desde el desembolso (paso 3), la obligación financiera formal del cliente solo inicia cuando el sistema detecta que el bono fue efectivamente utilizado en una compra en D1. Después del primer uso, el sistema bloquea automáticamente el cupo remanente para evitar compras adicionales durante el mismo ciclo de crédito.

**Vigencia y expiración del bono :** el bono tiene un plazo de **15 días calendario** para que el cliente lo utilice. Este plazo se implementará como una **variable configurable** en el panel administrativo, en lugar de un valor fijo en el código, de modo que pueda ajustarse sin requerir nuevos despliegues.

**Resultado:** Crédito activado mediante el uso del bono; cupo remanente bloqueado hasta finalizar el ciclo.

**Tiempo estimado:** Depende de la periodicidad del worker automatizado (mismo placeholder señalado en el documento 5); no es instantáneo respecto al momento exacto de la compra.

**Placeholder\*:** ver placeholder del documento 5 (paso 2) sobre la periodicidad exacta del worker que detecta el uso del bono; este mismo mecanismo aplica aquí. También queda pendiente definir la frecuencia y el canal exactos del flujo de recordatorios, y qué ocurre operativamente si el cliente no usa el bono dentro de los 15 días (ver Excepciones).

**Nota (Ajuste · jun 2026):** este paso también está marcado en el journey como ajuste de junio de 2026. *(Mismo pendiente que el paso 3: confirmar el detalle del ajuste con el dueño del proceso antes de presentar.)*

---

### 5. Pago del crédito

**Actor:** Cliente / Fiducia.

**Proceso:** Cuando llega la fecha de pago, el cliente realiza el pago correspondiente a su obligación mediante **Pagos Seguros en Línea (PSE)** o **débito automático** (ver documento 4). El dinero no retorna a D1: se consigna nuevamente en la cuenta fiduciaria, que funciona como cuenta de recaudo del producto, cerrando el ciclo financiero del crédito.

**Prepago voluntario:** si el cliente desea realizar un prepago voluntario de su obligación, este únicamente puede efectuarse a través de **PSE**; no está habilitado por débito automático.

**Resultado:** Pago recibido por la fiducia; ciclo financiero cerrado.

**Tiempo estimado:** Depende del método de pago utilizado (ver documento 4: PSE es prácticamente inmediato; débito automático ocurre en la fecha de corte, sujeto además a los tiempos de la red ACH — ver documento 5, paso 6b).

---

> **Nota sobre alcance (Acta de reunión Check-in, 29 jul 2026):** el proceso de evaluación de renovación del cupo, anteriormente documentado como paso 6 de este journey, se traslada a un documento independiente — **Flujo de Recurrencia** — para mantener este journey enfocado exclusivamente en el ciclo inicial de dispersión. Cualquier referencia a "renovación de cupo" o al reinicio del ciclo desde el paso 3 debe consultarse en ese nuevo documento.

---

## Reglas de negocio

- Colpatria debe crear y fondear la cuenta fiduciaria antes de realizar cualquier desembolso. **Este fondeo es un evento único al inicio del piloto (no se repite por cada crédito).**
- Todos los desembolsos del piloto se realizan desde la cuenta fiduciaria hacia D1. **Este desembolso sí es recurrente: ocurre una vez por cada ciclo de crédito y genera GMF en cada ocasión.**
- D1 únicamente recibe los recursos para emitir el bono correspondiente al cliente.
- El bono representa el valor del cupo utilizado por el cliente y tiene una **vigencia de 15 días calendario**, configurable mediante variable en el panel administrativo.
- El crédito se considera utilizado únicamente cuando el bono es redimido en una tienda D1, y su detección depende del worker automatizado que revisa las compras en D1.
- Después del primer uso del bono, el sistema bloquea el cupo remanente hasta finalizar el ciclo.
- Los pagos del cliente se realizan por PSE o débito automático y retornan siempre a la cuenta fiduciaria, sin generar GMF adicional en ese retorno. El prepago voluntario solo puede realizarse por PSE.
- El GMF del modelo aplica únicamente sobre el giro fiducia → D1 (0,4% por ciclo sobre el capital desembolsado); **el fondeo inicial Colpatria→Fiducia es un evento aparte y puede generar GMF propio, salvo que la fiducia esté en el mismo banco donde Colpatria tiene los fondos.**
- Si la fiducia se crea en el mismo banco donde Colpatria tiene los fondos, se ahorra el 4x1000 **del fondeo inicial únicamente** (no exime el GMF del desembolso recurrente a D1).
- Del dinero recaudado por pagos de los clientes, **solo el capital recuperado** se reutiliza para fondear nuevos créditos; los intereses y otros cargos quedan excluidos de la reinversión.
- **La evaluación de renovación de cupo y sus reglas de negocio asociadas ya no forman parte de este documento; se documentan en el Flujo de Recurrencia.**

---

## Entradas

- Crédito aprobado y firmado.
- Recursos disponibles para el piloto.
- Cuenta fiduciaria creada.
- Valor del cupo aprobado.
- Información del cliente.
- Compra realizada en D1 (detectada por el worker automatizado).
- Pago realizado por el cliente (PSE o débito automático).

---

## Salidas

- Recursos desembolsados hacia D1.
- Bono emitido al cliente (con vigencia de 15 días calendario).
- Crédito activado mediante el uso del bono.
- Pago recibido por la fiducia.

---

## Excepciones

- La cuenta fiduciaria no puede ser creada o fondeada.
- El desembolso hacia D1 falla.
- El bono no puede emitirse correctamente.
- El cliente no utiliza el bono dentro del plazo de 15 días calendario y este expira. **Placeholder\*:** el tratamiento operativo de un bono expirado no utilizado (p. ej., si el cupo queda disponible nuevamente o el ciclo se cierra sin uso) aún no está definido; pendiente de confirmar con el dueño del proceso.
- El worker automatizado no detecta oportunamente la compra en D1 (retraso en la activación del bono).
- El cliente no realiza el pago del crédito.
- El pago no retorna correctamente a la fiducia.

---

## Consideraciones

- La cuenta fiduciaria concentra tanto el origen como el recaudo de los recursos del crédito.
- El modelo reduce el impacto del GMF (4x1000): solo se genera en el giro fiducia → D1 (0,4% por ciclo de $1'000.000, equivalente a $48.000 al año sobre 12 ciclos del mismo capital); el retorno del pago del cliente a la fiducia no genera GMF adicional.
- Si Colpatria crea la fiducia en el mismo banco donde tiene los fondos, se ahorra además el 4x1000 del fondeo inicial (evento único, distinto del desembolso recurrente por ciclo).
- El crédito inicia efectivamente cuando el bono es utilizado por el cliente y detectado por el worker automatizado (mismo mecanismo del documento 5, Calculadora y Cobro del Crédito).
- El bloqueo del cupo remanente evita nuevas compras durante el mismo ciclo.
- El bono tiene una vigencia de 15 días calendario, y su vencimiento se acompaña de un flujo automatizado de recordatorios (WhatsApp o correo) para incentivar su uso oportuno.
- Solo el capital recuperado de los pagos se reinvierte en nuevos créditos; los intereses y demás cargos quedan excluidos.
- **Aún no se ha asignado nivel de fricción (Bajo/Medio/Alto) a ninguno de los pasos de este journey; se recomienda hacerlo antes de la siguiente versión del diagrama.**
- **La evaluación de renovación del cupo se documenta ahora de forma separada, en el Flujo de Recurrencia, por decisión del equipo.**

---

## Notas

- El cálculo del GMF mostrado en el journey corresponde al diseño financiero del piloto y puede modificarse en futuras versiones del producto.
- El monto del fondo fiduciario, el banco/entidad donde se constituirá la fiducia, y la vigencia exacta del bono (configurable) son parámetros sujetos a cambios durante la evolución del producto.
- Los dos pasos marcados como "Ajuste · jun 2026" en el diagrama (emisión del bono y uso del bono) requieren confirmación del dueño del proceso sobre qué cambió exactamente, para dejarlo documentado en la próxima versión.
- **El proceso de evaluación de renovación del cupo, antes incluido como paso 6 de este journey, se trasladó al nuevo documento Flujo de Recurrencia, según acuerdo del equipo en la reunión del 29 de julio de 2026.**

---

## Pendientes de validación

> **Pendiente de validar con el dueño del proceso (para mañana):**
>
> - Confirmar el monto exacto del fondo fiduciario y la periodicidad con la que debe reforzarse; llevar al menos una cifra tentativa. *(placeholder — paso 1)*
> - Confirmar el nombre de la entidad fiduciaria y si se creará en el mismo banco donde Colpatria tiene los fondos, para efectos del ahorro adicional de GMF en el fondeo inicial. *(placeholder — pasos 1 y 2)*
> - Confirmar qué cambió exactamente en junio de 2026 en la emisión del bono (paso 3) y en el uso del bono por el cliente (paso 4), marcados como "Ajuste · jun 2026" en el diagrama. *(pendiente — pasos 3 y 4)*
> - Confirmar la periodicidad exacta del worker que detecta el uso del bono en D1 (mismo pendiente señalado en el documento 5, paso 2). *(placeholder — paso 4)*
> - Definir la frecuencia y el canal definitivo del flujo automatizado de recordatorios del bono (a cargo de Alejandra Suárez). *(pendiente — paso 4)*
> - Definir el tratamiento operativo de un bono no utilizado que expira a los 15 días. *(pendiente — paso 4)*
> - Asignar el nivel de fricción (Bajo/Medio/Alto) a cada paso del journey, conforme a la leyenda del diagrama. *(pendiente — todo el journey)*
> - Actualizar el diagrama para eliminar el nodo de renovación de cupo y su rama de retorno al paso 3, dado que ese proceso ahora se documenta en el Flujo de Recurrencia. *(pendiente — diagrama)*

---

## Fuentes consultadas

- *Journeys Colpatria B2B* (junio de 2026), página 8.
- Documentación del modelo operativo del producto.
- Documento de alcance del producto.
- Validación del diagrama "Flujo de dispersión" realizada previo a la presentación (identificación de discrepancias entre fondeo inicial y desembolso recurrente, ajustes de junio 2026 sin documentar y niveles de fricción pendientes).
- **Acta de reunión "Producto: Check-in" (29 de julio de 2026):** decisiones sobre separación del flujo de recurrencia, definición de fiducia, aclaración de reinversión de capital, política de vigencia y expiración del bono (15 días calendario, configurable), flujo automatizado de recordatorios, y métodos de pago/prepago.
