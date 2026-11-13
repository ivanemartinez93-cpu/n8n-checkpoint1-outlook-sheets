# Proyecto final: flujo de prueba con Outlook y n8n

Este prototipo recibe un correo de Outlook con asunto de prueba, registra o actualiza una fila en Google Sheets por ID de mensaje, evalúa si el asunto contiene «urgente» y, en la rama verdadera, crea o actualiza un registro de Airtable por correo y avisa en Slack. La rama falsa termina sin notificación. La rama de error de Airtable envía una alerta a Slack.

## Diferencias con la consigna

Se usa Outlook en lugar de Gmail a pedido del alumno. Gmail no se ejecutó. Se utiliza Append or Update en vez de Append Row. El prototipo es local, se ejecuta manualmente, está filtrado al asunto exacto de prueba y no está listo para producción. La disponibilidad depende de que n8n esté encendido.

## Evidencia verificada

En n8n, ejecución manual #60, estado Succeeded: Outlook → Sheets → IF verdadero → Airtable → Slack, con un correo de prueba enviado a la misma cuenta. Se observó que el trigger procesó un mensaje de prueba anterior con el mismo asunto; no se demostró que detectara específicamente el nuevo correo enviado durante esa espera. En pruebas anteriores se observaron las dos ramas del IF. Para probar errores se cargó temporalmente un usuario inválido en Airtable: la API respondió 422, el elemento pasó a la salida Error y el nodo Slack de alerta devolvió ok=true. La configuración de Airtable fue restaurada y volvió a responder con éxito.

El manejo de errores probado cubre la falla de Airtable cuando Slack está disponible. No se probó un aviso alternativo para una caída de Slack ni el Error Trigger global. El estado general Succeeded no prueba por sí solo que no haya errores tratados; hay que inspeccionar ramas y resultados. La clave de coincidencia de Airtable es el correo, no se probó concurrencia y el campo Name contiene el asunto para este ensayo, no el nombre de un contacto real.

## Importación

Importar el JSON en n8n y asignar credenciales propias de Outlook, Sheets, Airtable y Slack. Reemplazar los identificadores de la hoja, base, tabla y canal; se han retirado intencionalmente. Crear en la tabla de Airtable los campos Name y Email, y en la hoja los campos Remitente, Asunto, Fecha e ID mensaje. El bot de Slack debe pertenecer al canal. Nunca publicar claves ni datos de personas.

La captura de la ejecución aún no se ha incorporado a este paquete. El envío y la evaluación siguen pendientes.

