# Support Triage Bot

Sistema automatizado de clasificación y enrutamiento de tickets de soporte, construido con n8n y un modelo de IA corriendo 100% local (Ollama). No depende de ninguna API externa de pago ni de servicios en la nube para funcionar.

## ¿Qué hace?

Recibe mensajes entrantes de clientes (consultas, reclamos, pedidos) y automáticamente:
1. Clasifica el mensaje por categoría (consulta / reclamo / venta) y prioridad
2. Detecta el sentimiento (positivo / neutral / negativo)
3. Enruta según la clasificación: auto-respuesta para FAQs, notificación urgente para reclamos graves, registro en planilla para seguimiento de ventas
4. Guarda un historial completo y auditable de cada ticket procesado

## Por qué es distinto

- **Cero dependencia externa**: el modelo de IA corre localmente vía Ollama, no hay llamadas a APIs pagas ni límites de cuota
- **Privacidad**: los datos nunca salen de la máquina donde corre el sistema
- **Manejo de errores real**: reintentos automáticos y modo degradado si el modelo no responde

## Stack

- **n8n** (local) — orquestación del workflow
- **Ollama** + Llama 3.1 8B — clasificación de tickets vía IA, 100% local
- **Google Sheets** — almacenamiento y registro de tickets
- **Telegram** — notificaciones de tickets urgentes

## Estructura del proyecto