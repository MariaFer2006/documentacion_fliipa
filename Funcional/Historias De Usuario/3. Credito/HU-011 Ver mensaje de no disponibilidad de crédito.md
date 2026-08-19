
### HU-011: Ver mensaje de no disponibilidad de crédito

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero ver un mensaje claro cuando no tengo ninguna opción de crédito disponible, para entender mi situación cuando no puedo continuar con el proceso. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Cuando el cliente no puede continuar porque su solicitud fue rechazada, no existe una oferta disponible o no existe un crédito con el que pueda continuar, el portal muestra un mensaje claro indicando que actualmente no hay opciones de crédito disponibles, en lugar de mostrar un error o una pantalla vacía. |
| **Relaciones** | Casos de uso: [CU-009](../../Casos%20de%20Uso/3.%20Credito/CU-009%20Consultar%20cupo%2C%20plan%20de%20pagos%20y%20disponibilidad.md). Historias relacionadas: [HU-010](../3.%20Credito/HU-010%20Consultar%20cupo,%20plan%20de%20pagos%20y%20movimientos.md), [HU-034](../5.%20Gesti%C3%B3n%20Plataforma%20del%20admin/HU-034%20Administrar%20la%20lista%20negra.md). |
| **Referencias** | Relacionado con la lógica de ingreso y consulta del estado del crédito en `fliipa-redemption`. |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Confirmado en plataforma:** existe un mensaje claro para los casos en los que el cliente no puede continuar, principalmente cuando el estado del crédito no permite avanzar o no existe un match/oferta disponible. **Corrección v1.6:** estar incluido en una lista negra (blacklist) no debe documentarse como condición que dispara este mensaje en el ingreso actual, ya que no corresponde al comportamiento observado en el flujo vigente. |


