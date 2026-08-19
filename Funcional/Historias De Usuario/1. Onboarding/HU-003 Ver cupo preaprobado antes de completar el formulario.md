### HU-003: Ver cupo preaprobado antes de completar el formulario

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero consultar mi cupo preaprobado antes de completar el formulario, para decidir si continúo con el proceso de solicitud. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Una vez identificada la preaprobación del cliente, el sistema muestra el valor del cupo preaprobado o sugerido antes de exigirle completar todos los pasos del onboarding. El valor mostrado corresponde al cupo disponible para el proceso de solicitud según la información de preaprobación cargada y procesada por la plataforma. |
| **Relaciones** | Casos de uso: CU-002. Requerimiento: RF-005. Historias relacionadas: HU-002, HU-004. |
| **Referencias** | [Procesos — 01 Onboarding Digital](../../../Operaciones/Procesos/01%20Onboarding%20Digital.md); `b2b/fliipa-back/src/controllers/checkouts/create-checkout.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Confirmado en plataforma:** la preaprobación y el cupo sugerido están operativos en el motor de riesgo. La plataforma permite cargar los clientes preaprobados mediante archivo, consultar/procesar la información de preaprobación y obtener el cupo sugerido utilizado en el flujo. Por tanto, esta funcionalidad no corresponde únicamente a un diseño documental, sino que cuenta con soporte operativo en el motor de riesgo. |
