# Preguntas frecuentes

## Concepto

### ¿USBGuardGo es un antivirus?

No. No analiza archivos ni busca malware. Su función es **controlar qué dispositivos USB pueden entrar** y pedir una decisión explícita ante los desconocidos. Es una capa de control de acceso físico, complementaria a un antivirus.

### ¿Qué pasa si no respondo al aviso?

El dispositivo se bloquea automáticamente al terminar la cuenta atrás. Es el comportamiento **fail-closed**: el silencio no autoriza nada. También se bloquea si cierras el aviso sin elegir.

### ¿Necesito tener `usbguard` instalado?

No. USBGuardGo funciona por sí solo con su monitor integrado y el bloqueo suave mediante `udisksctl`. Si `usbguard` está instalado y funcionando, lo usa para aplicar bloqueos a nivel de kernel, que es más fuerte. El Panel indica en todo momento qué motor está activo.

### ¿Necesito permisos de root?

Para abrir y usar la aplicación, no. La detección se hace leyendo `sysfs`, que es de solo lectura. Las operaciones que afectan al hardware se delegan en `usbguard` o `udisksctl`, que aplican sus propias políticas de permisos.

### ¿Funciona en Wayland?

Sí, a través de XWayland. La aplicación usa X11/OpenGL; en sesiones Wayland se ejecuta con la capa de compatibilidad. El paquete Flatpak también incluye los sockets necesarios.

### ¿Funciona en ARM o en 32 bits?

Esta versión se distribuye para **Linux x86_64**. No hay paquetes para ARM ni para 32 bits.

### ¿Puedo usarlo en un servidor sin escritorio?

La aplicación es gráfica; necesita X11 o XWayland. Para servidores sin entorno gráfico, `usbguard` directamente es una opción más adecuada.

## Uso diario

### ¿Por qué la primera vez acepta todos mis dispositivos?

Para que el teclado, el ratón, la cámara o el disco de arranque no generen avisos que no puedas resolver. Esos dispositivos ya estaban conectados y se consideran parte del equipo. Puedes revisar y borrar esas reglas en **Reglas**.

### ¿Cuál es la diferencia entre «Una vez» y «Siempre»?

- **Una vez:** el permiso dura mientras el dispositivo esté conectado. No se guarda. Ideal para un USB prestado.
- **Siempre:** se crea una regla permanente. El dispositivo no volverá a preguntar hasta que borres la regla.

### ¿Qué diferencia hay entre «Bloquear» y desenchufar?

Desenchufar no impide que el dispositivo vuelva a conectarse. **Bloquear** crea una regla para que, si vuelve a aparecer, se neutralice y no pregunte de nuevo. Para quitar el bloqueo, borra la regla en **Reglas**.

### ¿Cerrar la ventana apaga la protección?

No, si el escritorio tiene bandeja del sistema. La ventana se oculta, la aplicación sigue en la bandeja y el monitor continúa. Para terminar del todo, usa **Salir** en el menú de la bandeja.

Si el escritorio no tiene bandeja, cerrar la ventana termina la aplicación. En ese caso, mantén la ventana abierta mientras quieras proteger el equipo.

### No veo el icono en la bandeja

Algunos escritorios no implementan bandeja o la tienen desactivada. USBGuardGo lo detecta y no intercepta el cierre de la ventana; al cerrarla, la aplicación termina. Puedes usar el Panel para activar o desactivar la protección mientras la ventana esté abierta.

### ¿Puedo bloquear un teclado o un ratón?

Sí, pero ten cuidado: si bloqueas el teclado o el ratón con el que controlas el equipo, puedes quedarte sin entrada. El primer arranque los marca como de confianza precisamente para evitar ese problema. Si necesitas bloquear uno, hazlo desde **Dispositivos** o **Reglas** y asegúrate de tener otra forma de controlar el sistema.

### He perdido un USB que estaba permitido. ¿Qué hago?

Borra su regla en **Reglas**. Así, si alguien lo encuentra y lo conecta, USBGuardGo volverá a preguntar en lugar de aceptarlo automáticamente.

### ¿Puedo permitir un dispositivo por el puerto USB?

No. Las reglas se basan en `VID:PID` y, opcionalmente, en el número de serie. El puerto se muestra como información, pero no se usa como criterio de autorización.

### ¿La aplicación analiza el contenido del USB?

No. Solo decide si el dispositivo puede conectarse. No monta, escanea ni ejecuta archivos automáticamente.

## Configuración y datos

### ¿Dónde están las reglas y el registro?

En `~/.config/usbguardgo/`:

- `config.json` — reglas y ajustes, permisos `600`.
- `usbguardgo.log` — registro local con rotación.

### ¿Cómo empiezo de cero?

**Ajustes → Olvidar todo y empezar de cero**, o en terminal:

```bash
usbguardgo --reset-config
```

La próxima apertura se comporta como la primera vez.

### ¿Se pierden las reglas al actualizar?

No. Las actualizaciones de paquetes conservan `~/.config/usbguardgo/`. Solo se borran si usas la opción de empezar de cero o eliminas la carpeta manualmente.

### ¿La telemetría me espía?

No. Está apagada por defecto, solo cuenta números agregados y no se transmite automáticamente. Puedes verla y borrarla desde Ajustes. Consulta [Privacidad](PRIVACY.md).

### ¿Puedo cambiar el idioma?

Sí. **Ajustes → Idioma** cambia la interfaz al instante entre español, inglés, chino, ruso, alemán, portugués, coreano y árabe.

## Instalación y problemas

### ¿Qué paquete elijo?

- Fedora: RPM.
- Debian/Ubuntu: DEB.
- Cualquier distribución: AppImage o Flatpak.
- Sin instalación: binario portable.

Consulta la [guía de instalación](INSTALL.md) para comandos exactos.

### El AppImage no abre

Necesita FUSE 2. Instala `fuse-libs` en Fedora o `libfuse2` en Debian/Ubuntu. También puedes extraerlo:

```bash
./USBGuardGo-0.9.0-x86_64.AppImage --appimage-extract
./squashfs-root/AppRun
```

### El DEB no instala por dependencias

El paquete declara las bibliotecas X11/GL necesarias. En sistemas muy minimalistas puede que falte `libgl1` o `libx11-6`. Instálalas con tu gestor de paquetes y vuelve a intentarlo.

### El bloqueo no funciona

Comprueba el motor en el Panel:

- Si dice **usbguard**, el demonio debe estar instalado y configurado.
- Si dice **vigilancia integrada**, necesitas `udisksctl` (paquete `udisks2`) para desmontar y apagar dispositivos de almacenamiento.

### ¿Cómo reporto un fallo?

Abre un issue con la plantilla de error e incluye:

- Versión (`usbguardgo --version`).
- Distribución y versión.
- Escritorio y sesión (X11/Wayland).
- Si tienes `usbguard` y `udisks2`.
- Pasos para reproducirlo.
- Extracto del registro, **sin datos personales ni números de serie reales**.

### ¿Cómo reporto una vulnerabilidad?

No abras un issue público. Sigue las instrucciones de [SECURITY.md](../SECURITY.md).

## Licencia

### ¿El código fuente es público?

No. USBGuardGo es software propietario. Este repositorio distribuye binarios, paquetes y documentación; el código no se publica. Consulta [LICENSE](../LICENSE).

### ¿Puedo redistribuir el RPM o el DEB?

No sin permiso. La licencia concede un uso limitado de la aplicación, pero no permite redistribuir, modificar ni vender el software. Para distribución oficial, usa los enlaces de este repositorio.

### ¿Puedo contribuir?

No se aceptan contribuciones de código mientras el código sea privado. Los reportes de errores, las ideas y los comentarios de uso son bienvenidos en los issues.
