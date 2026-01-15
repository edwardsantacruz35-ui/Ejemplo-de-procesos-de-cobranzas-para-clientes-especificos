📧 Smart Collections UX: Motor de Cobranza Agrupada

📋 El Problema

En la gestión de cobranza B2B, enviar un correo por cada factura vencida genera "Fatiga de Notificaciones". Si un cliente debe 10 facturas, recibe 10 correos individuales, lo que satura su bandeja de entrada, reduce la probabilidad de lectura y daña la relación comercial.

💡 La Solución

Desarrollé un algoritmo en Google Apps Script que transforma el proceso de notificación mediante Consolidación Inteligente.

El sistema agrupa todas las obligaciones pendientes de un cliente en un único Estado de Cuenta Digital en tiempo real, aplicando Psicología del Color para comunicar la urgencia de manera visual y clara.

⚙️ Lógica Técnica

El script utiliza una estructura de Diccionario (Hash Map) para agrupar las filas de la hoja de cálculo antes de procesar el envío, optimizando el uso de la API de Gmail:

Ingesta: Lee el barrido de facturas pendientes desde Google Sheets.

Agrupación: Crea un objeto donde la clave es el Email del cliente y el valor es un Array con todas sus facturas.

Evaluación de Severidad (Max-Pooling): Recorre el grupo para encontrar la factura con el nivel de urgencia más alto.

Ejemplo: Si hay 4 facturas "Azules" (Nuevas) y 1 "Roja" (Vencida), todo el correo se vuelve "Rojo".

Renderizado: Construye una tabla HTML responsiva con los datos del grupo.

🎨 Sistema de Semáforo Visual

El diseño del correo se adapta dinámicamente según el riesgo detectado:

🔵 Azul (Nivel 1): Informativo / Envío para registro contable.

🟠 Naranja (Nivel 2): Advertencia / Facturas próximas a vencer o recién vencidas.

🔴 Rojo (Nivel 3): Crítico / Mora avanzada o acción inmediata requerida.

🚀 Características Clave

HTML Dinámico: Generación de tablas limpias y profesionales dentro del cuerpo del correo (MailApp) con estilos en línea (CSS inline).

Búsqueda Recursiva de Adjuntos: El script busca en Google Drive los PDFs correspondientes a todas las facturas del grupo y los adjunta en un solo paquete.

Reprogramación Sincronizada: Calcula la próxima fecha de seguimiento para todo el grupo, evitando la desincronización de contactos futuros.

Auditoría: Registro automático en una hoja de "Historial" con la referencia única del envío.

📦 Instalación y Uso

Crear una Google Sheet con las columnas de control requeridas (Email, Fecha, Hora, Nivel, etc.).

Abrir Extensiones > Apps Script y pegar el archivo Code.gs.

Configurar la constante ID_CARPETA_FACTURAS con el ID de la carpeta de Drive donde se alojan los soportes.

Configurar un activador (Trigger) por tiempo (ej: cada hora) para que el script revise la agenda automáticamente.

Desarrollado por Edward Gabriel Santacruz - Especialista en Automatización Financiera & RevOps
