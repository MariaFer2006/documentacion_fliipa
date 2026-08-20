### CU-026: Visualizar y confirmar el cupo aprobado

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial |
| **Descripción** | El cliente, tras ser notificado de la aprobación de su crédito, reingresa a la plataforma y visualiza el monto de su cupo aprobado junto con las condiciones de uso del crédito, para luego confirmarlas y continuar con el flujo de firma. |
| **Precondiciones** | El cliente cuenta con una línea de crédito en estado Aprobado (ver [HU-044](../../Historias%20De%20Usuario/2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md)) y fue notificado por correo/WhatsApp para reingresar a la plataforma. |
| **Flujo principal** | 1. El cliente ingresa a la plataforma con su documento y PIN.<br>2. El sistema detecta el estado Aprobado y lo dirige al paso de condiciones del crédito.<br>3. El sistema muestra el valor del cupo aprobado y las condiciones del crédito (uso en tienda D1, plazo de pago, mejora de score, congelamiento por mora).<br>4. El cliente confirma/acepta las condiciones.<br>5. El sistema lo dirige al siguiente paso (plan de pagos y firma de contrato). |
| **Flujos alternativos / excepciones** | A1. El cliente no confirma las condiciones: permanece en la pantalla y no avanza en el flujo.<br>A2. El estado del crédito no es Aprobado ni Activo: se le restringe el acceso a este paso (ver [HU-011](../../Historias%20De%20Usuario/3.%20Credito/HU-011%20Ver%20mensaje%20de%20no%20disponibilidad%20de%20cr%C3%A9dito.md)). |
| **Postcondiciones** | El cliente confirmó el cupo aprobado y puede continuar con el plan de pagos y la firma digital del contrato. |
| **Reglas de negocio** | Esta consulta y confirmación es un paso obligatorio previo a la firma del contrato; no reemplaza ni sustituye la decisión de crédito tomada por el motor KYC/riesgo (ver [CU-006](../2.%20KYC/CU-006%20Consultar%20analisis%20de%20KYC%20y%20evaluaci%C3%B3n%20de%20credito.md)). |
| **Historias de usuario relacionadas** | [HU-045](../../Historias%20De%20Usuario/3.%20Credito/HU-045%20Visualizacion%20y%20confirmacion%20del%20cupo%20aprobado.md) (Visualización y confirmación del cupo aprobado) |
| **Estado en plataforma** | **Implementado.** La pantalla `credit-conditions` muestra el cupo aprobado y el botón "Aceptar condiciones" habilita el avance al plan de pagos. |
| **Referencias** | `apps/redemption/app/onboarding/credit-conditions/page.tsx`, `apps/redemption/app/onboarding/layout.tsx`, `apps/redemption/actions/auth.ts` — *Historias de Usuario — Fliipa*, carpeta "3. Credito" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
