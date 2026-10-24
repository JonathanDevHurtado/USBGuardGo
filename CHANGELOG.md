# Historial de versiones

Todas las versiones públicas de USBGuardGo se documentan aquí. El formato sigue las ideas de [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y el versionado semántico `MAYOR.MENOR.PARCHE`.

## [0.9.0] — 2026-10-24

**Primer release público.** Interfaz Aurora, auditoría interna completa y paquetes para Linux x86_64.

### Añadido

- Interfaz **Aurora**: azul de Zorin OS, grafito y naranja de Pop!_OS, tipografías Fira Sans/Fira Mono, navegación lateral, tarjetas redondeadas y controles de ventana al estilo Windows 11.
- Panel con estado de protección, contadores, actividad reciente, motor activo y exportación del registro.
- Página **Dispositivos** con agrupación en nuevos, externos e internos, y acciones por dispositivo.
- Página **Reglas** con permisos y bloqueos permanentes, creación manual por `VID:PID` y eliminación.
- Página **Ajustes** con tiempo de espera, idioma, arranque automático, telemetría opcional y reinicio de la configuración.
- Página **Ayuda** integrada, en lenguaje claro.
- Aviso de USB nuevo con cuenta atrás y bloqueo automático al agotarse.
- **8 idiomas**: español, inglés, chino simplificado, ruso, alemán, portugués, coreano y árabe (con RTL).
- Bandeja del sistema con Mostrar, Activar/Desactivar protección y Salir.
- Arranque automático oculto en la bandeja con `--tray`.
- Integración con `usbguard` para bloqueo a nivel de kernel.
- Bloqueo suave con `udisksctl` cuando `usbguard` no está disponible.
- Registro local con rotación y exportación manual.
- Página de manual `usbguardgo(1)`.
- Metadatos AppStream para centros de software.
- Paquetes **RPM**, **DEB**, **AppImage** y **Flatpak** para Linux x86_64.

### Corregido

- Precedencia de reglas: una regla con serie exacta gana sobre la regla genérica del mismo `VID:PID`.
- Carreras entre el monitor y la interfaz: los eventos se despachan en el hilo gráfico.
- Callbacks de los controles de Ajustes que se disparaban al construir la página.
- Desbordes de layout en ventanas de 1180×760 y en la página de Ajustes.
- Timeouts en comandos externos para evitar bloqueos indefinidos.
- Resolución de enlaces simbólicos en `sysfs`.
- Guardado atómico de la configuración y permisos `700/600`.
- Permisos de sesión que ya no se persisten.
- Normalización de reglas inválidas al cargar la configuración.
- Gestión de errores cuando no hay discos que desmontar (`ErrNoDisks`).
- Botón de minimizar oculto en configuraciones sin bandeja.

### Seguridad

- Auditoría interna de reglas, monitor, almacenamiento, notificaciones y UI.
- Comandos externos sin shell, con argumentos separados y tiempo límite.
- Configuración y registro con permisos restrictivos.
- Telemetría local, opcional y apagada por defecto.
- Pruebas con detector de carreras (`go test -race`).
- Prueba de humo real bajo Xvfb para primer arranque, bandeja, `--version` y `--reset-config`.

### Paquetes

- RPM para Fedora 39–44 x86_64 (compilado en Fedora 44).
- DEB para Debian 12/13 y Ubuntu 24.04 amd64 (glibc ≥ 2.36).
- AppImage y Flatpak para otras distribuciones x86_64.
- Binario portable y archivo `SHA256SUMS.txt`.

### Limitaciones conocidas

- Solo Linux x86_64.
- El sondeo integrado no es instantáneo; para BadUSB se recomienda `usbguard`.
- El bloqueo suave está orientado a dispositivos de almacenamiento.
- La aplicación no analiza el contenido de los dispositivos.
- No sustituye a un antivirus, al cifrado ni a una política de seguridad completa.

---

## Versiones anteriores

Las versiones 0.1.0–0.8.0 fueron iteraciones internas de desarrollo. No se publicaron como releases independientes. La 0.9.0 es la primera versión distribuida públicamente e incluye todo el trabajo anterior.
