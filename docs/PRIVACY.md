# Privacidad

USBGuardGo está diseñado para funcionar sin enviar datos a ningún servidor. Esta página explica qué información se guarda, dónde vive y cómo borrarla.

## Resumen

| Pregunta | Respuesta |
|---|---|
| ¿Envía datos a Internet? | **No** |
| ¿Tiene telemetría automática? | **No**; existe un contador local opcional y apagado por defecto |
| ¿Necesita una cuenta? | **No** |
| ¿Guarda nombres de dispositivos? | **Sí, localmente**, para que las reglas sean legibles |
| ¿Guarda números de serie? | **Solo si el dispositivo los expone y se usa para una regla** |
| ¿Se puede borrar todo? | **Sí**, desde Ajustes o con `--reset-config` |
| ¿El registro sale del equipo? | **Solo si tú lo exportas y lo compartes** |

## Qué se guarda

La configuración vive en:

```text
~/.config/usbguardgo/config.json
```

Contiene:

- Reglas permanentes: `VID`, `PID`, serie opcional, nombre y acción (permitir o bloquear).
- Idioma de la interfaz.
- Segundos de espera antes del bloqueo automático.
- Estado de la protección y preferencia de arranque automático.
- Contadores de telemetría, solo si el usuario los activa.

El archivo se crea con permisos `600` dentro de una carpeta con permisos `700`. Solo el usuario propietario puede leerlo o modificarlo.

## Registro de actividad

El registro vive en:

```text
~/.config/usbguardgo/usbguardgo.log
```

Contiene eventos como:

- Dispositivo nuevo detectado.
- Permiso concedido una vez.
- Regla permanente creada.
- Dispositivo bloqueado.
- Error al aplicar un bloqueo.
- Cambio de idioma o de configuración.

El registro se rota automáticamente para no crecer sin control. Se puede exportar a `~/usbguardgo-registro.txt` desde el Panel. **Ese archivo no se envía a ningún sitio**: solo existe si tú pulsas el botón.

Antes de compartir un registro en un issue, revisa si contiene nombres o números de serie que prefieras ocultar. Puedes editarlo o redactarlos.

## Telemetría opcional

La telemetría está **apagada por defecto**. Si la activas:

- Solo cuenta números: bloqueos, permisos y tipos de fallo.
- No incluye nombres de dispositivos, series, `VID:PID`, rutas ni datos personales.
- Se guarda en el mismo `config.json`.
- Se puede ver y borrar desde **Ajustes → Telemetría**.
- No se transmite automáticamente a ningún servidor.

El objetivo es permitir que el usuario comparta estadísticas agregadas si quiere ayudar a priorizar mejoras. No es un sistema de analítica remota.

## Notificaciones

Los avisos de escritorio se envían mediante `notify-send` al servicio de notificaciones del sistema. El contenido es el nombre del dispositivo y su identificador; no se envía fuera del equipo.

## Conexiones de red

USBGuardGo **no abre conexiones de red** para funcionar. No comprueba actualizaciones, no envía informes y no consulta servicios externos.

Las descargas de paquetes y las actualizaciones se hacen a través de GitHub Releases cuando tú las solicitas; esa interacción es la de tu navegador o tu gestor de paquetes, no la de la aplicación.

## Borrar los datos

Desde la interfaz:

**Ajustes → Olvidar todo y empezar de cero**.

Desde la terminal:

```bash
usbguardgo --reset-config
```

Esto elimina `config.json`. El registro se puede borrar a mano:

```bash
rm ~/.config/usbguardgo/usbguardgo.log
```

Si quieres eliminar también la carpeta completa:

```bash
rm -rf ~/.config/usbguardgo
```

La próxima apertura creará una configuración nueva y volverá a tratar los dispositivos conectados como primera ejecución.

## Datos de terceros

USBGuardGo no comparte datos con terceros. Los componentes de terceros incluidos (Fyne, Go, Fira) se ejecutan localmente y no añaden analítica ni conexiones de red. Sus licencias están en [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md).

## Cambios en esta política

Si una versión futura añade alguna función que implique red o recopilación de datos, se documentará aquí y en las notas de la versión antes de activarla. La telemetría nunca se activará por defecto sin un aviso claro.
