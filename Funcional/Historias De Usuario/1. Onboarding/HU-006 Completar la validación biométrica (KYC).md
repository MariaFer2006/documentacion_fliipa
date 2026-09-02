#### HU-006: Completar la validaci贸n biom茅trica con el proveedor externo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Cliente empresarial |
| **Historia** | Como cliente empresarial, quiero completar la validaci贸n biom茅trica con el proveedor externo, para verificar mi identidad de forma segura sin tener que ir a una oficina. |
| **Prioridad** | Media |
| **Criterios de aceptaci贸n** | El cliente completa el proceso de biometr铆a con el proveedor externo definido, desde el dispositivo que tenga disponible, y el sistema registra el resultado (aprobado, rechazado o en revisi贸n) asociado a su solicitud. |
| **Relaciones** | Casos de uso: [CU-004](../../Casos de Uso/2. KYC/CU-004 Completar validaci髇 biometrica.md). Historias relacionadas:[HU-007](../2. KYC/HU-007 Cargar soportes bancarios.md), [HU-022](../2. KYC/HU-022 Revisi髇 Biometria.md), [HU-046](../2. KYC/HU-046 Manejo de rechazo en biometr韆.md). |
| **Referencias** | [Procesos](../../../Operaciones/Procesos/02 Validacion Kcy Y Evaluaci髇 Riesgo.md); no se encontr贸 en el repositorio l贸gica de biometr铆a ni integraci贸n con un proveedor externo (se busc贸 "biometria" y "Olimpia" en todo `b2b/`, sin resultados). |
 **Autor** | Mar铆a Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versi贸n** | V.1.7 |
| **Comentarios** | **Historia separada de la HU-004 original (v1.5)**, que combinaba biometr铆a y carga de soportes bancarios en un solo paso; al ser dos procesos distintos y no relacionados, deben documentarse como historias at贸micas. Se elimina la restricci贸n a "desde el celular": el cliente debe poder completar este paso desde el dispositivo que tenga disponible (celular, computador u otro), ya que la plataforma no debe limitarse a un flujo exclusivamente m贸vil. Se mantiene pendiente de confirmar si la biometr铆a vive en un microservicio no incluido en este repositorio, se implementara post-piloto. |
