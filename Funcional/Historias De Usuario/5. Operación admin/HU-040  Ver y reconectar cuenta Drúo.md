#### HU-040 — Ver y reconectar la cuenta Druo del cliente

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador / operaciones |
| **Historia** | Como administrador, quiero consultar el estado de la cuenta Druo del cliente y solicitar su conexión o reconexión cuando sea necesario, para desbloquear los procesos de onboarding o cobro. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | 1. Desde la ficha del cliente, un administrador con los permisos correspondientes puede consultar el estado actual de la cuenta Druo.<br><br>2. El administrador puede iniciar una solicitud de conexión o reconexión cuando la cuenta lo requiera.<br><br>3. Al enviar la solicitud, el sistema debe registrar la operación como **pendiente** y no debe asumir ni mostrar una conexión exitosa hasta recibir la respuesta de Druo.<br><br>4. El sistema debe esperar la respuesta del proceso de Druo, considerando que esta puede tardar entre **1 y 2 días**.<br><br>5. Cuando Druo responda, el sistema debe actualizar el estado de la cuenta según el resultado real de la operación.<br><br>6. Si la conexión o reconexión es exitosa, el sistema debe reflejar la cuenta como conectada y permitir que continúen los procesos que dependan de ella.<br><br>7. Si la operación falla, el sistema debe reflejar el estado correspondiente y permitir la gestión de una nueva reconexión cuando aplique.<br><br>8. El sistema no debe simular respuestas exitosas ni completar la conexión antes de recibir la confirmación de Druo. |
| **Relaciones** | Cuenta bancaria en onboarding; HU-014 (débito automático, aún pendiente de punta a punta). |
| **Autor** | María Fernanda Herazo |
| **Fecha** | 20/08/2026 |
| **Versión** | V.1.8 |
| **Comentarios** | **Corrección v1.8 (Check-in de Producto, 20 ago 2026):** se incorpora la lógica de espera asíncrona para la respuesta de Druo (1-2 días), evitando que el sistema simule o asuma una conexión exitosa antes de recibir confirmación real. Esta misma lógica de espera aplica también al flujo de débito automático (ver HU-014). |
