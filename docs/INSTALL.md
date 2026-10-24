# Guía de instalación

USBGuardGo se distribuye como aplicación compilada para **Linux x86_64**. No es necesario compilar nada ni instalar un entorno de desarrollo.

## Requisitos

| Requisito | Detalle |
|---|---|
| Sistema | Linux x86_64 con X11 o XWayland |
| OpenGL | Controladores gráficos con soporte OpenGL |
| Espacio | ~30 MB instalado; los paquetes ocupan entre 11 y 13 MB |
| Escritorio | GNOME, KDE Plasma, Xfce, Cinnamon, MATE, Budgie, COSMIC o similar |
| Bandeja | Opcional; sin ella, cerrar la ventana no oculta la aplicación |

Dependencias recomendadas (no obligatorias para abrir la aplicación):

| Paquete | Función |
|---|---|
| `usbguard` | Bloqueo a nivel de kernel, la opción más fuerte |
| `udisks2` | Bloqueo suave: desmontar y apagar el dispositivo |
| `usbutils` | Respaldo de detección mediante `lsusb` |
| `libnotify` / `libnotify-bin` | Notificaciones de escritorio |

## Descargar

Abre la página de **[Releases](https://github.com/JonathanDevHurtado/USBGuardGo/releases/latest)** y descarga el archivo correspondiente a tu distribución, junto con `SHA256SUMS.txt`.

| Distribución | Archivo recomendado |
|---|---|
| Fedora 39–44 | `usbguardgo-0.9.0-1.fc44.x86_64.rpm` |
| Debian 12/13 | `usbguardgo_0.9.0_amd64.deb` |
| Ubuntu 24.04 | `usbguardgo_0.9.0_amd64.deb` |
| Cualquier Linux x86_64 | `USBGuardGo-0.9.0-x86_64.AppImage` |
| Cualquier Linux con Flatpak | `USBGuardGo-0.9.0.flatpak` |
| Sin instalador | `usbguardgo-0.9.0-linux-amd64.tar.gz` |

## Verificar la descarga

Descarga `SHA256SUMS.txt` en la misma carpeta que el paquete y ejecuta:

```bash
sha256sum -c --ignore-missing SHA256SUMS.txt
```

La línea de tu archivo debe terminar en `OK` o «La suma coincide». Si falla, vuelve a descargar el paquete.

## Fedora y derivados

```bash
sudo dnf install ./usbguardgo-0.9.0-1.fc44.x86_64.rpm
```

El paquete instala:

- `/usr/bin/usbguardgo`
- lanzador en el menú de aplicaciones
- iconos escalable y de 256 px
- página de manual `usbguardgo(1)`
- metadatos AppStream para el centro de software
- licencia y avisos de terceros en `/usr/share/licenses/usbguardgo/`

Para desinstalar:

```bash
sudo dnf remove usbguardgo
```

## Debian / Ubuntu / derivados

```bash
sudo apt install ./usbguardgo_0.9.0_amd64.deb
```

El paquete DEB está compilado sobre **Debian 12** para funcionar con glibc 2.36 o superior (Debian 12/13 y Ubuntu 24.04). Instala los mismos componentes que el RPM, con la documentación en `/usr/share/doc/usbguardgo/`.

Para desinstalar:

```bash
sudo apt remove usbguardgo
```

## AppImage

```bash
chmod +x USBGuardGo-0.9.0-x86_64.AppImage
./USBGuardGo-0.9.0-x86_64.AppImage
```

El AppImage incluye las bibliotecas X11 auxiliares y utiliza OpenGL y la glibc del sistema (≥ 2.36). Necesita FUSE 2:

```bash
# Fedora
sudo dnf install fuse-libs

# Debian / Ubuntu
sudo apt install libfuse2
```

Si tu sistema no permite FUSE, puedes extraer el AppImage y ejecutar el binario interno:

```bash
./USBGuardGo-0.9.0-x86_64.AppImage --appimage-extract
./squashfs-root/AppRun
```

## Flatpak

```bash
flatpak install --user ./USBGuardGo-0.9.0.flatpak
flatpak run io.github.jonathandevhurtado.usbguardgo
```

El Flatpak usa el runtime `org.freedesktop.Platform` 24.08 y funciona con X11 o Wayland a través de XWayland. Para desinstalarlo:

```bash
flatpak uninstall io.github.jonathandevhurtado.usbguardgo
```

## Binario portable

```bash
tar -xzf usbguardgo-0.9.0-linux-amd64.tar.gz
cd usbguardgo-0.9.0-linux-amd64
./usbguardgo
```

El archivo incluye el binario, el lanzador, los iconos, la página de manual, la licencia y los avisos de terceros. No instala nada en el sistema.

## Primer arranque

1. Abre USBGuardGo desde el menú de aplicaciones o ejecuta `usbguardgo`.
2. La primera pantalla explica el funcionamiento y marca como de confianza los dispositivos que ya están conectados.
3. Revisa esa lista. Si algo no debería estar permitido, cámbialo en **Reglas**.
4. Enchufa un USB nuevo para comprobar el aviso y la cuenta atrás.

La configuración se crea en `~/.config/usbguardgo/` con permisos `600`; la carpeta usa `700`. No se necesitan permisos de root para abrir la aplicación.

## Actualizar

- **RPM:** descarga el nuevo `.rpm` y ejecuta `sudo dnf upgrade ./usbguardgo-*.rpm`.
- **DEB:** descarga el nuevo `.deb` y ejecuta `sudo apt install ./usbguardgo_*_amd64.deb`.
- **AppImage:** sustituye el archivo anterior por el nuevo.
- **Flatpak:** `flatpak update io.github.jonathandevhurtado.usbguardgo`.

Las reglas y la configuración se conservan entre actualizaciones. Para empezar de cero, usa **Ajustes → Olvidar todo y empezar de cero** o `usbguardgo --reset-config`.

## Solución de problemas

### La ventana no abre

Comprueba que tienes X11 o XWayland y OpenGL:

```bash
glxinfo -B
```

Si `glxinfo` no existe, instala `mesa-utils` o `glx-utils`.

### No aparece el icono en la bandeja

Algunos escritorios no implementan bandeja del sistema. En ese caso, cerrar la ventana termina la aplicación; la protección solo está activa mientras la ventana o el proceso siguen abiertos. Usa el botón **Desactivar protección** del Panel para controlarla manualmente.

### El aviso no bloquea el dispositivo

Comprueba el modo en el Panel:

- **usbguard** requiere el demonio instalado y configurado.
- **Vigilancia integrada** requiere `udisksctl` para desmontar y apagar el dispositivo. Si falta, instala `udisks2`.

### La aplicación no ve un dispositivo

USBGuardGo lee `/sys/bus/usb/devices`. En contenedores o entornos muy restringidos puede no tener acceso. Ejecutarla fuera del contenedor suele resolverlo.

### El AppImage no arranca

Instala FUSE 2 o extrae el AppImage como se indica arriba.

### Quiero reportar un fallo

Abre un issue con la plantilla de error e incluye la versión (`usbguardgo --version`), la distribución, el escritorio y los pasos para reproducirlo. **No incluyas números de serie reales ni datos personales**; puedes redactarlos.
