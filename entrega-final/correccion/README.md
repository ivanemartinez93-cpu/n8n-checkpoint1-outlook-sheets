# Proyecto final: corrección

Automatización de práctica con Outlook → Google Sheets → IF → Airtable → Slack. Se utiliza Outlook porque la cuenta disponible no tiene Gmail habilitado y el alumno eligió continuar sin crear una cuenta Gmail. El disparador implementado y ejecutado es Outlook; se solicita evaluar esta sustitución como alternativa al requisito de Gmail.

## Cambios
- Fecha de recepción añadida al registro de Airtable; aviso de Slack con remitente, asunto, fecha y vínculo al registro.
- Error Trigger separado, enlazado en la configuración del flujo principal, que envía un aviso por Outlook a la propia cuenta si un error no manejado detiene el flujo.
- La ruta de error de Airtable intenta alertar por Slack; si Slack falla, el gestor global constituye un canal alternativo. Un error tratado por una salida de error no equivale a un fallo global.
- Flujo principal sin publicar. El filtro de Outlook limita el ensayo a un asunto específico; n8n local debe estar encendido.

## Evidencia verificada el 13/11/2026
- Ejecución manual 74: correo sintético de asunto único procesado por Outlook → Sheets → filtro URGENTE → Airtable → Slack. Slack devolvió ok=true y el mensaje contenía remitente, asunto, fecha, vista previa del cuerpo y enlace al registro. La ejecución 73 terminó sin elementos y no demuestra el recorrido.
- Ensayo automático aislado en una copia: ejecución 71 llegó a Slack y recibió channel_not_found al configurar intencionalmente un canal inexistente. La ejecución 72 del Error Trigger figura exitosa; su entrada identifica la ejecución 71 como origen y el nodo de Outlook ejecutó el envío. La copia se despublicó después del ensayo. El gestor permanece publicado y enlazado al borrador principal.
- La captura previa de la ejecución 60 corresponde a una versión anterior y no demuestra la prueba de error ni las correcciones actuales.

## Archivos
Los dos JSON son exportaciones sanitizadas: no incluyen credenciales, destinatario ni identificadores de recursos. Para importarlos se deben configurar credenciales, hoja, base, tabla y canal propios; reemplazar el enlace de Airtable y la dirección de alerta; publicar el manejador y seleccionarlo como Error Workflow en la configuración del principal. El ensayo de error usó una copia con canal inválido; el JSON principal conserva la lógica normal, sin ese fallo deliberado. La sustitución de Gmail y de Append Row por Append or Update sigue sujeta a aceptación del evaluador. La ejecución manual no demuestra que el gestor actúe ante una falla real; esa prueba corresponde a la ejecución automática 71/72.


La exportación actual incorpora nombres descriptivos y un asunto de prueba único. El archivo solicitado está como `ProyectoFinal_IvanMartinez.json`. Por privacidad la vista previa del cuerpo de un correo se transmite al canal de Slack de prueba: antes de adaptar el flujo a correos reales, acordar el alcance y minimizar los datos compartidos. La captura anterior corresponde a la ejecución 60; la [captura de la ejecución 74](ejecucion-74.png) muestra la versión corregida y la rama de error.
