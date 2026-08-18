#### HU-006: Completar la validación biométrica (KYC)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero completar la validación biométrica con el proveedor externo, para verificar mi identidad de forma segura sin tener que ir a una oficina. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El cliente completa el proceso de biometría con el proveedor externo definido, desde el dispositivo que tenga disponible, y el sistema registra el resultado (aprobado, rechazado o en revisión) asociado a su solicitud. |
| **Relaciones** | Casos de uso: CU-004. Historias relacionadas: HU-007, HU-022. |
| **Referencias** | [Procesos](../negocio/procesos/03-validacion-kyc.md); no se encontró en el repositorio lógica de biometría ni integración con un proveedor externo (se buscó "biometr*" y "Olimpia" en todo `b2b/`, sin resultados). |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.17 |
| **Comentarios** | **Historia separada de la HU-004 original (v1.5)**, que combinaba biometría y carga de soportes bancarios en un solo paso; al ser dos procesos distintos y no relacionados, deben documentarse como historias atómicas. Se elimina la restricción a "desde el celular": el cliente debe poder completar este paso desde el dispositivo que tenga disponible (celular, computador u otro), ya que la plataforma no debe limitarse a un flujo exclusivamente móvil. Se mantiene pendiente de confirmar si la biometría vive en un microservicio no incluido en este repositorio. |
