# Casos Críticos y Validación de Identidad — Servicio al Cliente *PLACEHOLDER*

Bogotá · 2026 · Documento confidencial

## Control de versiones

| Versión | Fecha | Autor | Descripción |
|---|---|---|---|
| 1.0 | 27 ago 2026 | María Fernanda Herazo | Creación del documento, a partir del Acta de Check-in de Producto del 27/08/2026. Sirve de referencia para [CU-014](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md) y [HU-029](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md). |


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
| Suplantación de identidad | Alguien distinto al titular del cupo intenta operar la cuenta, solicitar información sobre ella, o redimir el código de compra en D1 en su nombre. | Pendiente de precisar criterios operativos (¿qué señales dispara esta sospecha?). |
| Desconocimiento de compra | El cliente reporta una operación o cargo que no reconoce haber realizado. | Pendiente de precisar criterios operativos. |


---

## 3. Proceso de validación de identidad

Acordado en el Check-in de Producto del 27/08/2026: la validación de identidad en un caso crítico es un **proceso obligatorio** que debe completarse **antes** de que el agente brinde información al cliente o proceda con su solicitud.

**Mecanismo:** el agente valida la identidad del cliente mediante **dos filtros de verificación**.



### 3.1 Resultado de la validación

| Resultado | Acción |
|---|---|
| El cliente pasa **al menos uno** de los dos filtros | El agente continúa atendiendo el caso con normalidad. |
| El cliente **no pasa ninguno** de los dos filtros | Se bloquea la cuenta del cliente por **24 horas**. El caso no se aprueba. |


---

## 4. Relación con otros procesos y fichas

- [CU-014 — Atender al cliente por IA y escalar a agente humano](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md): el paso 5 del flujo principal referencia este documento cuando el caso escalado a un agente humano es crítico.
- [HU-029 — Validar identidad en casos críticos](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md): historia de usuario cubierta por CU-014, con los mismos criterios de aceptación.
- [06 Servicio Cliente](06%20Servicio%20Cliente.md): proceso general de atención al cliente donde se originan las categorías de caso crítico (paso 3, "Recepción del caso por el agente humano").
- [CU-010 — Usar el cupo en tienda D1](../../Funcional/Casos%20de%20Uso/3.%20Credito/CU-010%20Usar%20el%20cupo%20en%20tienda%20D1.md): confirma que el cupo solo se redime mediante código validado en el punto de venta D1, base para descartar "uso indebido del cupo" como categoría de caso crítico (ver sección 2).

---

## 5. Estado en plataforma

No se encontró en el repositorio ningún módulo de asistente conversacional de IA, de escalamiento a agente humano, ni de validación de identidad para casos críticos. Este documento describe el diseño acordado, no una funcionalidad implementada hoy (mismo hallazgo que en CU-014 y HU-029).

---



## 6. Fuentes consultadas

- Acta de Check-in de Producto, 27/08/2026 (Google Meet / Gemini Notes) — decisión "Gestión de casos críticos y verificación".
- [06 Servicio Cliente](06%20Servicio%20Cliente.md) — *Operaciones/Procesos*, repositorio `documentacion_fliipa`.
- [CU-010 — Usar el cupo en tienda D1](../../Funcional/Casos%20de%20Uso/3.%20Credito/CU-010%20Usar%20el%20cupo%20en%20tienda%20D1.md) — *Funcional*, repositorio `documentacion_fliipa`.
- [CU-014](../../Funcional/Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md) y [HU-029](../../Funcional/Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md) — *Funcional*, repositorio `documentacion_fliipa`.
