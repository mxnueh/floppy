# Floppy — Sistema de Monitoreo de Nivel de Agua

Sistema web para monitorear el nivel de agua y prevenir inundaciones, con datos de sensores enviados a **ThingSpeak**.

## 1. Descripción

Floppy muestra en un dashboard las lecturas de nivel de agua almacenadas en ThingSpeak (campo 2), con gráficas en tiempo real, historial y configuración de perfil. Incluye además una aplicación de escritorio (Tkinter) para administrar el monitoreo y las alertas.

## 2. Características

- Login con sesión y rutas protegidas.
- Landing page pública y dashboard con gráficas (**Chart.js**).
- Vista dedicada al nivel de agua (`/water-level`) e historial de lecturas (`/history`).
- Endpoint proxy `/api/thingspeak-data` para consultar ThingSpeak sin problemas de CORS.
- Configuración de perfil y cambio de contraseña.
- Envío de alertas por correo (SMTP) cuando se detectan niveles peligrosos.
- App de escritorio con gráficas (matplotlib), exportación a CSV y sistema de alertas.

## 3. Tecnologías

- Python 3 · Flask
- requests · pytz · smtplib
- ThingSpeak (API REST)
- HTML · CSS · JavaScript · Chart.js
- Tkinter · matplotlib · numpy (app de escritorio)

## 4. Instalación

```bash
pip install -r requirements.txt
python app.py
```

La app de escritorio está en `Inundaciones v.1 app Escritorio/`:

```bash
cd "Inundaciones v.1 app Escritorio"
pip install -r requirements.txt
python water_level_monitor.py
```

(`tkinter` viene incluido con la instalación estándar de Python; en Linux puede requerir el paquete `python3-tk`.)

## 5. Configuración

En `app.py` ajusta:

- `THINGSPEAK_URL`: canal y campo de ThingSpeak.
- `app.secret_key`: clave secreta de sesión.
- `USERS`: usuarios de acceso.
- Parámetros SMTP para las alertas por correo.

> **Importante:** no guardes contraseñas ni claves en el código ni en el repositorio. Usa variables de entorno o un archivo de configuración fuera del control de versiones (la app de escritorio incluye `config_example.py` como plantilla).

## 6. Rutas principales

| Ruta | Descripción |
|------|-------------|
| `/` · `/landing` | Página de presentación |
| `/login` · `/logout` | Autenticación |
| `/dashboard` | Panel principal |
| `/water-level` | Nivel de agua |
| `/history` | Historial de lecturas |
| `/config` | Perfil y contraseña |
| `/api/thingspeak-data` | Datos de ThingSpeak en JSON |

## 7. Despliegue

Incluye `render.yaml` para desplegar en Render.

## 8. Estructura

```
floppy/
├── app.py
├── requirements.txt
├── render.yaml
├── templates/        # landing, login, dashboard, water-level, history, config
├── static/           # css e imágenes
└── Inundaciones v.1 app Escritorio/
    ├── water_level_monitor.py
    ├── config_example.py
    ├── setup.py
    └── install.bat
```
