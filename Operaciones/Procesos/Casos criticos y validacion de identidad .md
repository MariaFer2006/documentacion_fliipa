# Casos Críticos y Validación de Identidad — Servicio al Cliente *PLACEHOLDER*

Bogotá · 2026 · Documento confidencial

## En palabras simples

**¿Qué es un caso crítico?** Es cuando el cliente mismo dice "esto no fui yo" o "no reconozco esto". No es algo que el sistema detecta solo — es el cliente quien lo reporta.

**¿Qué pasa cuando ocurre?**

1. El cliente reporta el problema por WhatsApp (asistente de IA) o llamando a la línea de atención.
2. Se identifica de qué tipo es: **suplantación de identidad** (alguien más está usando su cuenta) o **desconocimiento de compra** (hay un cobro que no reconoce).
3. Antes de bloquear nada, se revisa si es un simple malentendido (ej. el ticket de la tienda D1, el registro del sistema).
4. Si sigue habiendo duda real, se valida la identidad del cliente con dos verificaciones. Si pasa al menos una, se aprueba el caso; si no pasa ninguna, se bloquea la cuenta por 24 horas.
5. Todo queda registrado: qué dijo el cliente, la categoría y el resultado.

## Control de versiones

| Versión | Fecha | Autor | Descripción |
|---|---|---|---|
| 1.0 | 27 ago 2026 | María Fernanda Herazo | Creación del documento, a partir del Acta de Check-in de Producto del 27/08/2026. Sirve de referencia para [CU-014](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md) y [HU-029](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md). |
| 1.1 | 01 sep 2026 | María Fernanda Herazo | Se completan los criterios operativos de activación (sección 2.1), pendientes desde la v1.0: se precisa que un caso solo se clasifica como crítico cuando el **cliente lo reporta explícitamente** (no por detección proactiva del sistema), y se listan las frases/reportes que disparan cada categoría, así como los casos que quedan excluidos. Se agrega el flujo operativo (sección 3.1) y se deja pendiente formalizado el SLA de primera respuesta (sección 5). |


---

## 1. Objetivo

Definir qué constituye un **caso crítico** dentro de la atención al cliente y establecer el proceso obligatorio de validación de identidad que el agente de servicio al cliente debe aplicar antes de brindar información o proceder con una solicitud, cuando un caso se clasifica como crítico.

Este documento existe porque [CU-014](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md) y [HU-029](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md) referencian la validación de identidad en casos críticos, pero antes no existía un documento propio con la definición y el mecanismo. Se crea a partir de lo acordado en el Acta de Check-in de Producto del 27/08/2026.

---

## 2. Definición de caso crítico

Un caso crítico es aquel en el que existe riesgo de fraude, suplantación o uso indebido del producto, y que por tanto requiere validar la identidad del cliente antes de que el agente brinde cualquier información o proceda con la solicitud.

El proceso de Servicio al Cliente (ver [06 Servicio Cliente](06%20Servicio%20Cliente.md)) identificaba originalmente tres categorías: suplantación de identidad, desconocimiento de compra y uso indebido del cupo. Tras revisión (28/08/2026), se descarta **"uso indebido del cupo"** como categoría independiente: el cupo solo puede redimirse mediante el código que el sistema genera y que se valida físicamente en el punto de venta D1 (ver [CU-010](../../Funcional/Casos%20de%20Uso/3.%20Credito/CU-010%20Usar%20el%20cupo%20en%20tienda%20D1.md)); el cliente no tiene forma de usar el cupo en un lugar distinto a D1. Si alguien distinto al titular llega a redimir el código, ese escenario ya queda cubierto por la categoría de **suplantación de identidad**, no por una categoría aparte de "uso indebido".

Categorías vigentes:

| Categoría | Descripción | Estado de la definición |
|---|---|---|
| Suplantación de identidad | Alguien distinto al titular del cupo intenta operar la cuenta, solicitar información sobre ella, o redimir el código de compra en D1 en su nombre. | Definido — ver criterios operativos en 2.1. |
| Desconocimiento de compra | El cliente reporta una operación o cargo que no reconoce haber realizado. | Definido — ver criterios operativos en 2.1. |

### 2.1 Criterios operativos de activación

**Principio rector:** un caso se clasifica como crítico **únicamente cuando el cliente lo reporta explícitamente** — así lo establece el journey de Servicio al Cliente (*Journeys Fran finales.pdf*, Journeys Colpatria B2B, junio 2026, con participación de Francisco Javier Martínez Vargas), donde el carril "Cliente" es el origen de las tres situaciones críticas. El IA/agente no clasifica un caso como crítico por sospecha o criterio propio — no existe en la plataforma un motor de detección proactiva de fraude (ver sección 5) — sino que activa el protocolo cuando el reporte del cliente coincide con uno de los disparadores definidos a continuación.

**Ejemplos — Suplantación de identidad.** El caso se clasifica en esta categoría en escenarios como:
- El cliente dice que nunca solicitó el crédito, y resulta que un empleado de su tienda pidió el crédito con su cédula/RUT sin que él se enterara.
- El titular recibe un aviso de "cuota vencida" pero nunca abrió cuenta ni habló con el asistente de WhatsApp.
- El dueño del negocio descubre que su encargado de turno redimió el código de compra en D1 sin autorización.
- El cliente reporta que le robaron o perdió el celular con WhatsApp activo, y alguien siguió la conversación con el IA pidiendo aumento de cupo.
- Alguien llama a la línea de atención haciéndose pasar por el titular para pedir cambio de número de cuenta bancaria o de teléfono registrado.

**Ejemplos — Desconocimiento de compra.** El caso se clasifica en esta categoría en escenarios como:
- El cliente ve en su estado de cuenta una cuota de una compra que dice no haber hecho ese día en D1.
- Autorizó una compra por un monto y en el sistema aparece un cargo mayor, sin reconocer la diferencia.
- Compartió el código de redención con un empleado para una compra puntual, pero el empleado lo usó para algo distinto o de mayor valor.
- Aparecen dos cargos el mismo día y el cliente solo recuerda haber hecho una compra.
- Dice que canceló la compra en tienda, pero igual le llegó la cuota a cobrar.

**Antes de escalar a bloqueo: revisar primero.** No todo reporte es fraude real. Casos como una compra duplicada o una cuota que no llegó a cancelarse a menudo se resuelven revisando el ticket de D1 o el registro del sistema, sin necesidad de bloquear la cuenta. El protocolo de los dos filtros de verificación (sección 3) aplica cuando, después de esa revisión inicial, sigue existiendo duda real sobre si fue el titular quien actuó.

**Casos que NO se clasifican como críticos.** Para evitar sobre-activación del protocolo, quedan expresamente excluidos:
- Dudas sobre saldo, cupo disponible o fecha de corte.
- Solicitudes de prórroga, alivio de pago o quejas generales de servicio.
- Reclamos que no incluyen una negación explícita de una operación o de la identidad (es decir, no contienen un "no reconozco..." o "no fui yo...").


---

## 3. Proceso de validación de identidad

Acordado en el Check-in de Producto del 27/08/2026: la validación de identidad en un caso crítico es un **proceso obligatorio** que debe completarse **antes** de que el agente brinde información al cliente o proceda con su solicitud.

**Mecanismo:** el agente valida la identidad del cliente mediante **dos filtros de verificación**.



### 3.1 Resultado de la validación

| Resultado | Acción |
|---|---|
| El cliente pasa **al menos uno** de los dos filtros | El agente continúa atendiendo el caso con normalidad. |
| El cliente **no pasa ninguno** de los dos filtros | Se bloquea la cuenta del cliente por **24 horas**. El caso no se aprueba. |

### 3.2 Flujo operativo propuesto

1. El cliente reporta la situación por WhatsApp (IA) o por la línea de atención al cliente.
2. El IA/agente identifica si el reporte coincide con alguno de los disparadores definidos en 2.1 y **registra la frase textual del cliente** como evidencia del reporte.
3. Se clasifica el caso como crítico y se activa el protocolo de validación de identidad de la sección 3 (dos filtros de verificación).
4. Si el caso viene escalado desde el IA, el agente humano lo recibe con el contexto completo, incluyendo la frase que originó la clasificación.
5. El caso queda registrado en el log de auditoría con: canal de reporte, texto del reporte del cliente, categoría asignada (suplantación / desconocimiento de compra) y resultado de la validación (aprobado / cuenta bloqueada 24h).


---

## 4. Relación con otros procesos y fichas

- [CU-014 — Atender al cliente por IA y escalar a agente humano](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md): el paso 5 del flujo principal referencia este documento cuando el caso escalado a un agente humano es crítico.
- [HU-029 — Validar identidad en casos críticos](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md): historia de usuario cubierta por CU-014, con los mismos criterios de aceptación.
- [06 Servicio Cliente](06%20Servicio%20Cliente.md): proceso general de atención al cliente donde se originan las categorías de caso crítico (paso 3, "Recepción del caso por el agente humano").
- [CU-010 — Usar el cupo en tienda D1](../../Funcional/Casos%20de%20Uso/3.%20Credito/CU-010%20Usar%20el%20cupo%20en%20tienda%20D1.md): confirma que el cupo solo se redime mediante código validado en el punto de venta D1, base para descartar "uso indebido del cupo" como categoría de caso crítico (ver sección 2).

---

## 5. Estado en plataforma

No se encontró en el repositorio ningún módulo de asistente conversacional de IA, de escalamiento a agente humano, ni de validación de identidad para casos críticos. Este documento describe el diseño acordado, no una funcionalidad implementada hoy (mismo hallazgo que en CU-014 y HU-029).

**Pendiente abierto:** aún no está definido el SLA de primera respuesta del agente humano tras el escalamiento de un caso crítico. Se recomienda fijarlo en la próxima revisión de este documento (ver también el placeholder equivalente en [06 Servicio Cliente](06%20Servicio%20Cliente.md)).

---



## 6. Fuentes consultadas

- Acta de Check-in de Producto, 27/08/2026 (Google Meet / Gemini Notes) — decisión "Gestión de casos críticos y verificación".
- *Journeys Fran finales.pdf* (Journeys Colpatria B2B, junio 2026, con participación de Francisco Javier Martínez Vargas) — origen del principio de que el caso crítico se origina en el reporte del cliente (carril "Cliente" del journey).
- [06 Servicio Cliente](06%20Servicio%20Cliente.md) — *Operaciones/Procesos*, repositorio `documentacion_fliipa`.
- [CU-010 — Usar el cupo en tienda D1](../../Funcional/Casos%20de%20Uso/3.%20Credito/CU-010%20Usar%20el%20cupo%20en%20tienda%20D1.md) — *Funcional*, repositorio `documentacion_fliipa`.
- [CU-014](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md) y [HU-029](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md) — *Funcional*, repositorio `documentacion_fliipa`.
