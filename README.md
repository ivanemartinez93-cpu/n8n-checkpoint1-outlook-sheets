# Corrección de la entrega final

La versión corregida, los dos flujos sanitizados y las pruebas del Error Trigger están en [entrega-final/correccion](entrega-final/correccion/README.md). La captura histórica es de una versión anterior; la prueba de Slack y alerta se documenta por separado.

# Entrega final del curso

El proyecto final, su JSON sanitizado, la captura de ejecución y la explicación están en [entrega-final](entrega-final/README.md). La prueba utiliza Outlook en lugar de Gmail, como se explica allí.

# Checkpoint 1: registro de correo en Sheets

El flujo conecta Microsoft Outlook con Google Sheets y registra remitente, asunto, fecha de recepción e ID del mensaje. En las pruebas, un segundo procesamiento del mismo ID actualizó la fila existente en lugar de añadir otra. La imagen muestra una ejecución con estado Succeeded.

## Diferencias respecto de la consigna

La consigna pide Gmail Trigger y Append Row. Como la cuenta de Google disponible no tiene Gmail habilitado, se probó Outlook; se usó Append or Update Row para controlar repeticiones. El nodo Gmail permanece en el diagrama, pero no se ejecutó como origen funcional. El cuerpo del mensaje no se guardó. La aceptación de estas diferencias queda a criterio de Ticher.

## Reproducibilidad y límites

El JSON procede de la exportación de n8n; se sustituyeron los identificadores de credenciales y de la hoja por marcadores antes de compartirlo. Para ejecutarlo hay que configurar credenciales propias y seleccionar una hoja con columnas `Remitente`, `Asunto`, `Fecha` e `ID mensaje`. El filtro usa un asunto de prueba concreto.

El control se probó en dos ejecuciones secuenciales del mismo mensaje. No se probó la concurrencia ni se garantiza una deduplicación atómica. Las filas anteriores sin identificador necesitan revisión por separado. La captura es de una ejecución manual; el flujo no está publicado ni activo en segundo plano.
