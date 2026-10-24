# Política de seguridad

## Versiones soportadas

| Versión | Soporte |
|---|---|
| 0.9.x | ✅ Activa |
| 0.8.x y anteriores | ❌ Sin soporte |

Solo se aceptan reportes sobre la versión pública más reciente. Si usas una versión antigua, actualiza antes de reportar.

## Reportar una vulnerabilidad

**No abras un issue público con detalles explotables.**

Usa el canal privado de GitHub:

1. Entra en la pestaña **Security** del repositorio.
2. Pulsa **Report a vulnerability**.
3. Rellena el formulario con toda la información posible.

Este canal crea un aviso privado visible solo para el mantenedor. Si no estuviera disponible, escribe a **JonathanHurtadoDev@proton.me** con el asunto `[SECURITY] USBGuardGo` y sin adjuntar exploits públicos.

### Qué incluir

- Versión exacta (`usbguardgo --version`).
- Distribución y versión del sistema.
- Escritorio y sesión gráfica (X11 o Wayland).
- Si tienes `usbguard` y `udisks2` instalados.
- Pasos para reproducir el problema.
- Impacto que crees que tiene.
- Prueba de concepto, si es posible.
- Registro relevante, **sin números de serie reales ni datos personales**.

### Qué esperar

- Acuse de recibo orientativo en **72 horas**.
- Evaluación inicial en **7 días**.
- Notificación cuando haya una corrección o una decisión sobre el reporte.
- Crédito público si lo deseas, una vez publicada la corrección.

No hay programa de recompensas económicas.

## Alcance

Entran en alcance, entre otros:

- Inyección de comandos o de argumentos en las llamadas a `usbguard`, `udisksctl`, `lsusb` o `notify-send`.
- Escalada de privilegios.
- Lectura o escritura de archivos fuera de `~/.config/usbguardgo/`.
- Elusión del bloqueo sin consentimiento del usuario.
- Persistencia indebida de datos personales.
- Permisos incorrectos en la configuración o el registro.
- Vulnerabilidades en dependencias incluidas en los binarios.

Quedan fuera de alcance:

- Ataques que requieran acceso físico con privilegios de root.
- Ingeniería social.
- Denegación de servicio que requiera control local de la cuenta del usuario.
- Fallos del propio demonio `usbguard` o del kernel.
- Falta de funciones que no forman parte del producto.
- Informes generados automáticamente sin una prueba de concepto clara.

## Divulgación responsable

Pide confirmación antes de publicar detalles. El objetivo es corregir y publicar una actualización antes de cualquier divulgación pública. Si el reporte no se atiende en un plazo razonable, puedes escalar escribiendo de nuevo al correo de contacto.

## Salvo conducto

Si actúas de buena fe, respetas esta política y no accedes a datos de terceros ni degradas servicios, no se tomarán medidas legales contra ti por el reporte. Esta declaración no autoriza pruebas contra sistemas que no sean de tu propiedad ni contra infraestructura de GitHub.

## Buenas prácticas para usuarios

- Mantén actualizado USBGuardGo y tu distribución.
- Instala y configura `usbguard` si necesitas bloqueo a nivel de kernel.
- No concedas permisos permanentes a dispositivos que no controles.
- Revisa el registro local si algo no cuadra.
- No ejecutes la aplicación con `sudo`: no lo necesita.
