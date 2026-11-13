# Proyecto final: corrección

Automatización de práctica con Outlook → Google Sheets → IF → Airtable → Slack. Se utiliza Outlook porque no se dispone de Gmail, como sustitución explícita del requisito del curso; se solicita evaluar la alternativa sin presentar Gmail como implementado.

## Cambios
- Fecha de recepción añadida al registro de Airtable; aviso de Slack con remitente, asunto, fecha y vínculo al registro.
- Error Trigger separado, enlazado en la configuración del flujo principal, que envía un aviso por Outlook a la propia cuenta si un error no manejado detiene el flujo.
- La ruta de error de Airtable intenta alertar por Slack; si Slack falla, el gestor global constituye un canal alternativo. Un error tratado por una salida de error no equivale a un fallo global.
- Flujo principal sin publicar. El filtro de Outlook limita el ensayo a un asunto específico; n8n local debe estar encendido.

## Evidencia verificada el 13/11/2026
- Ejecución manual de la versión corregida: n8n informó éxito y se observaron elementos hasta el nodo Slack. Al usarse un asunto repetido, no se identificó inequívocamente qué correo se procesó.
- Ensayo automático aislado en una copia: ejecución 71 llegó a Slack y recibió channel_not_found al configurar intencionalmente un canal inexistente. La ejecución 72 del Error Trigger figura exitosa; su entrada identifica la ejecución 71 como origen y el nodo de Outlook ejecutó el envío. La copia se despublicó después del ensayo. El gestor permanece publicado y enlazado al borrador principal.
- La captura previa de la ejecución 60 corresponde a una versión anterior y no demuestra la prueba de error ni las correcciones actuales.

## Archivos
Los dos JSON son exportaciones sanitizadas: no incluyen credenciales, destinatario ni identificadores de recursos. Para importarlos se deben configurar credenciales, hoja, base, tabla y canal propios; reemplazar el enlace de Airtable y la dirección de alerta; publicar el manejador y seleccionarlo como Error Workflow en la configuración del principal. El ensayo de error usó una copia con canal inválido; el JSON principal conserva la lógica normal, sin ese fallo deliberado. La sustitución de Gmail y de Append Row por Append or Update sigue sujeta a aceptación del evaluador. La ejecución manual no demuestra que el gestor actúe ante una falla real; esa prueba corresponde a la ejecución automática 71/72.

