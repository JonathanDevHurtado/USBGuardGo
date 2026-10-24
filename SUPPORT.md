# Soporte

## Antes de preguntar

La documentación resuelve la mayoría de las dudas:

| Documento | Contenido |
|---|---|
| [Instalación](docs/INSTALL.md) | Requisitos, paquetes, verificación y desinstalación |
| [Uso](docs/USAGE.md) | Pantallas, reglas, avisos y bandeja |
| [Cómo funciona](docs/HOW-IT-WORKS.md) | Detección, decisiones y motores de bloqueo |
| [Privacidad](docs/PRIVACY.md) | Qué se guarda y cómo borrarlo |
| [FAQ](docs/FAQ.md) | Dudas habituales y solución de problemas |
| [Historial](CHANGELOG.md) | Cambios de cada versión |

## Abrir un issue

Usa las plantillas del repositorio:

- **Bug** para fallos reproducibles.
- **Sugerencia** para ideas y mejoras.

Incluye siempre:

- Versión (`usbguardgo --version`).
- Distribución y versión.
- Escritorio y sesión (X11 o Wayland).
- Paquete usado (RPM, DEB, AppImage, Flatpak o portable).
- Si tienes `usbguard` y `udisks2`.
- Pasos exactos para reproducir el problema.
- Extracto del registro, **sin números de serie ni datos personales**.

## Tiempos de respuesta

Este es un proyecto mantenido por una persona. Los tiempos son orientativos:

| Tipo | Respuesta habitual |
|---|---|
| Bug reproducible | 3–7 días |
| Sugerencia | 7–14 días |
| Duda de uso | 7 días |
| Vulnerabilidad | 72 horas (ver [SECURITY.md](SECURITY.md)) |

No hay soporte comercial ni garantía de resolución. Las peticiones incompletas o fuera de alcance pueden cerrarse con una explicación.

## Qué no se ofrece

- Soporte para versiones anteriores a la 0.9.x.
- Compilaciones para ARM, 32 bits u otros sistemas.
- Asistencia para modificar el código, que es privado.
- Soporte de distribuciones o empaquetadores de terceros.
- Recuperación de datos de dispositivos bloqueados.
- Asesoría de seguridad para organizaciones.

## Seguridad

No publiques vulnerabilidades en issues. Sigue el canal privado descrito en [SECURITY.md](SECURITY.md).

## Licencia

USBGuardGo es software propietario. El soporte no incluye derechos de modificación, redistribución ni acceso al código fuente. Consulta [LICENSE](LICENSE).
