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

```
triage-bot/
├── README.md
├── dataset/
│   └── tickets_sample.csv       # Dataset de ejemplo de tickets de soporte
├── docs/
│   └── Support_Triage_Bot_Plan_de_Mejoras.pdf   # Plan de mejoras técnico del sistema
└── workflows/
    └── Support_Triage_Bot_v3_simple.json        # Workflow exportado de n8n
```

## Integraciones y canales de entrada

Además del webhook principal, el sistema suma canales y visualización mediante estas herramientas:

- **Google Sheets** — [Support Triage Bot - Tickets](https://docs.google.com/spreadsheets/d/1MtOhCwH04kSzLU8CC2oNJT2JjFWHQmvZIUroPFy4kGA/edit?gid=0#gid=0): almacenamiento de cada ticket clasificado (fecha, canal, mensaje, categoría, prioridad, sentimiento)
- **Lovable** — [Dashboard "Soporte Inteligente"](https://soporte-inteligente.lovable.app/) ([proyecto en Lovable](https://lovable.dev/projects/bb10cb85-6639-4859-8d88-69590f422ab3)): visualización en tiempo real de los tickets de la Sheet, con métricas por canal y sentimiento
- **Tactiq** — [Workflows de transcripción](https://app.tactiq.io/workflows): transcribe llamadas/reuniones y las envía como canal de entrada adicional de tickets
- **Zapier** — [Zap de integración](https://zapier.com/editor/377275166/draft/377275167/sample): conecta Tactiq con el webhook de n8n cuando una transcripción está lista

> Nota: n8n corre self-hosted (local), sin URL pública asociada al proyecto.
