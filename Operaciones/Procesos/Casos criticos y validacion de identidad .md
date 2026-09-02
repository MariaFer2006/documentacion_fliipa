# Casos Críticos y Validación de Identidad — Servicio al Cliente Fliipa- PLACEHOLDER 

Bogotá · 2026 · Documento confidencial

---

## 1. Objetivo y principio rector

Definir qué es un **caso crítico** y el proceso obligatorio de validación de identidad que debe completarse **antes** de dar información o proceder con la solicitud del cliente.

Un caso se clasifica como crítico **únicamente cuando el cliente lo reporta explícitamente** (no hay detección automática de fraude en la plataforma). Antes de escalar, se revisa si es un simple malentendido (ticket D1, registro del sistema); solo si persiste la duda se activa la validación de identidad.

**Excluidos** (no son casos críticos): dudas de saldo/cupo/fecha de corte, solicitudes de prórroga o alivio, y reclamos sin una negación explícita ("no reconozco...", "no fui yo...").

---

## 2. Categorías, disparadores y qué hacer

| Categoría | Disparadores (ejemplos) | Qué hacer |
|---|---|---|
| **Suplantación de identidad** | • Empleado pidió el crédito sin autorización<br>• Aviso de "cuota vencida" sin haber abierto cuenta<br>• Redención de código en D1 sin autorización<br>• Robo/pérdida de celular con WhatsApp activo<br>• Alguien se hace pasar por el titular para cambiar cuenta o teléfono | Validar identidad (sección 3)<br>y continuar la atención normal. |
| **Desconocimiento de compra** | • Cuota de una compra no reconocida<br>• Cargo mayor al autorizado<br>• Código compartido usado indebidamente<br>• Dos cargos el mismo día<br>• Compra cancelada que igual se cobró | Validar identidad (sección 3)<br>y continuar la atención normal. |
| **Reclamación, demanda o tutela** | • El cliente dice que va a demandar<br>• Ya instauró tutela<br>• Consultó/contrató abogado | 1. Validar identidad<br>2. **Escalar de inmediato a Legal** (no cerrar desde Servicio al Cliente)<br>3. Dejar constancia escrita de fecha y hora del reporte |
| **Cancelación del bono o crédito** | • Solicitud expresa de cancelar/anular (no solo pausar)<br>• Surge como consecuencia de otro caso crítico ya reportado | 1. Validar identidad<br>2. Si es consecuencia de otro caso, resolver ese primero<br>3. Escalar a Crédito/Cobranza<br>4. Confirmar por escrito al cliente |
| **Reclamación ante la SIC*** | • El cliente dice que ya radicó o va a radicar queja ante un ente de vigilancia | 1. Validar identidad<br>2. **Escalar a Legal/Cumplimiento con prioridad alta** (plazos legales obligatorios)<br>3. No dar respuestas informales que contradigan la respuesta formal |
| **Derecho de petición** | • El cliente exige que su solicitud se tramite como derecho de petición, con respuesta por escrito | 1. Validar identidad<br>2. Escalar a Legal para trámite formal<br>3. Confirmar por escrito la fecha de radicación<br>4. No cerrar el caso en el canal de IA |


---

## 3. Validación de identidad — Guion "Verificación de Titularidad"

No se da información del crédito antes de completar esta verificación.

**Apertura:** *"Antes de darte información de tu crédito, necesito validar titularidad. Es rápido, solo un par de preguntas."*

Se eligen **3 preguntas distintas** de esta lista de 5 (rotando). El cliente debe acertar **las 3**:

| # | Pregunta | Dato que valida |
|---|---|---|
| 1 | ¿Con qué NIT o cédula solicitaste tu cupo Fliipa? | NIT / cédula registrado |
| 2 | ¿Cuál es el nombre completo del representante legal registrado? | Nombre del representante legal |
| 3 | ¿Cuál es el nombre de tu negocio o empresa? | Razón social / nombre comercial |
| 4 | ¿Cuál es el número de celular que registraste con nosotros? | Teléfono registrado |
| 5 | ¿Cuál es el valor de tu cupo aprobado? | Monto del cupo |

**Si acierta las 3:** *"Listo, validación exitosa. Cuéntame en qué te puedo ayudar."* → continúa la atención normal.

**Si no acierta las 3:** ⚠️ no definido en el material recibido (el guion menciona "primer intento", lo que sugiere un segundo paso que no llegó).

---

## 4. Pendientes abiertos

| Pendiente | Detalle |
|---|---|
| Umbral de aprobación | El documento base habla de "2 filtros, pasa con 1";<br>el guion de Titularidad habla de "3 preguntas, deben acertarse las 3".<br>Confirmar con Producto cuál rige. |
| Camino de fallo | Qué pasa si el cliente no acierta las 3 preguntas<br>(¿segundo intento?, ¿cuántos antes de bloquear?). |
| SLA de primera respuesta | Aún no definido el tiempo de respuesta del agente humano tras escalamiento. |
| Plazos legales | Confirmar con Legal los plazos de tutela, derecho de petición y SIC. |
| Plataforma | Ninguno de estos flujos está implementado hoy;<br>este documento describe el diseño acordado, no una funcionalidad existente. |

---

## 5. Referencias

CU-014 (Atender al cliente por IA y escalar a agente humano) · HU-029 (Validar identidad en casos críticos) · 06 Servicio Cliente · CU-010 (Usar el cupo en tienda D1) — repositorio `documentacion_fliipa`.

## 6. Fuentes consultadas

- Acta de Check-in de Producto, 27/08/2026 — decisión "Gestión de casos críticos y verificación".
- *Journeys Fran finales.pdf*, Journeys Colpatria B2B, junio 2026 (Francisco Javier Martínez Vargas) — origen del principio de que el caso crítico se origina en el reporte del cliente.
- Guion "Verificación de Titularidad" — entregado directamente por el usuario el 02/09/2026 (pendiente confirmar autor/origen interno).
