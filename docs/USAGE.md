# Guía de uso

Esta guía explica cada pantalla y las decisiones que puedes tomar. USBGuardGo está pensado para que, en pocos minutos, entiendas qué está pasando y por qué.

## Primer arranque

La primera vez que abres USBGuardGo verás una pantalla de bienvenida. El programa:

1. Detecta los dispositivos USB conectados en ese momento.
2. Los marca como **de confianza** para que el teclado, el ratón, la cámara o el disco externo no generen avisos imposibles de resolver.
3. Te recuerda que, a partir de ahora, cualquier dispositivo nuevo preguntará antes de entrar.

Puedes revisar y cambiar esa lista en **Reglas**. Si prefieres no confiar en algo, bórralo: la próxima vez que se conecte, preguntará.

## La ventana

La interfaz tiene tres zonas:

- **Barra superior:** marca, estado de protección y controles de ventana (minimizar, maximizar, cerrar).
- **Barra lateral:** navegación entre Panel, Dispositivos, Reglas, Ajustes y Ayuda, además del interruptor de protección y la versión.
- **Área de página:** el contenido de la sección elegida.

El pie muestra la versión, un recordatorio de que los datos son locales y un aviso breve.

### Estado de protección

La píldora de la barra superior y la tarjeta de la barra lateral indican el estado:

- **Protegido** — el monitor está activo y los dispositivos nuevos preguntarán.
- **En pausa** — la protección está desactivada temporalmente; los dispositivos nuevos se permiten sin preguntar.

El interruptor **Desactivar protección / Activar protección** está en el Panel y en la barra lateral. Úsalo solo cuando sepas lo que estás haciendo: mientras está en pausa, USBGuardGo no bloquea nada.

## Panel

El Panel es la vista de un vistazo:

- Estado general y botón para activar o desactivar la protección.
- Contadores de **pendientes**, **conectados** y **reglas**.
- **Actividad reciente:** permisos, bloqueos, cambios de configuración y errores.
- **Consejo de seguridad:** recomendaciones breves.
- **Motor de protección:** te dice si estás usando `usbguard` (kernel) o la vigilancia integrada.
- **Exportar registro:** guarda una copia legible en `~/usbguardgo-registro.txt` para compartir en un reporte.

Si hay un dispositivo pendiente de decisión, aparecerá destacado con acceso directo al aviso.

## Dispositivos

Muestra lo que está conectado ahora mismo. Cada tarjeta incluye:

- Nombre legible (fabricante y producto).
- Tipo: ratón, teclado, cámara, audio, almacenamiento, móvil, hub, etc.
- Identificador `VID:PID` y número de serie, si está disponible.
- Estado: permitido, bloqueado o pendiente.
- Acciones disponibles según el estado.

### Acciones

| Acción | Efecto | Se guarda |
|---|---|---|
| **Permitir una vez** | Permite el dispositivo mientras siga conectado | No |
| **Permitir siempre** | Crea una regla permanente de permiso | Sí |
| **Bloquear** | Bloquea el dispositivo y crea una regla de bloqueo | Sí |
| **Desbloquear** | Elimina la regla de bloqueo | Sí |
| **Quitar regla** | Olvida la regla de permiso o bloqueo | Sí |

Los permisos de sesión («una vez») nunca se escriben en disco. Si desconectas el dispositivo y lo vuelves a conectar, volverá a preguntar.

## Reglas

Las reglas son la memoria permanente de USBGuardGo. Hay dos tipos:

- **Permitidos:** el dispositivo entra sin preguntar.
- **Bloqueados:** el dispositivo se neutraliza y se recuerda.

Cada regla se identifica por `VID:PID` y, opcionalmente, por número de serie. Cuando existe una regla con serie exacta, tiene prioridad sobre la regla genérica del mismo modelo. Así puedes permitir tu teclado concreto y no todos los teclados del mismo modelo.

### Crear una regla a mano

Si conoces el `VID:PID` de un dispositivo (por ejemplo, `046d:c52b`), puedes añadirlo desde **Reglas → Añadir regla**. El formulario valida que ambos valores sean hexadecimales de cuatro dígitos y permite elegir entre permitir o bloquear.

### Editar y borrar

- **Editar** cambia el nombre o la acción de una regla existente.
- **Borrar** elimina la regla. Si el dispositivo estaba bloqueado, la próxima conexión volverá a preguntar.
- **Olvidar todo y empezar de cero** (en Ajustes) borra todas las reglas de una vez.

## Aviso de dispositivo nuevo

Cuando conectas un dispositivo sin regla, aparece un aviso con:

- Nombre, tipo e identificador del dispositivo.
- Tres botones: **Permitir una vez**, **Permitir siempre** y **Bloquear**.
- Una cuenta atrás visible. Al llegar a cero, se bloquea automáticamente.

La cuenta atrás se puede ajustar entre 5 y 300 segundos en **Ajustes → Tiempo de espera**. Si cierras el aviso sin decidir, también se bloquea.

### ¿Qué opción elegir?

- **Permitir una vez:** ideal para un USB prestado, una presentación o un dispositivo que no volverás a usar.
- **Permitir siempre:** para tus propios aparatos: teclado, ratón, cámara, disco de copias.
- **Bloquear:** para cualquier cosa que no reconozcas, un dispositivo que no esperabas o algo que se conectó sin que lo hicieras tú.

## Ajustes

| Ajuste | Qué hace |
|---|---|
| **Tiempo de espera** | Segundos antes del bloqueo automático (5–300) |
| **Idioma** | Cambia la interfaz al instante entre 8 idiomas |
| **Arrancar al iniciar sesión** | Crea una entrada de autostart que arranca oculto en la bandeja |
| **Telemetría** | Contadores locales opcionales, apagados por defecto |
| **Olvidar todo** | Borra reglas, preferencias y telemetría; la próxima apertura es como la primera |

Los ajustes se guardan automáticamente en `~/.config/usbguardgo/config.json`.

## Bandeja del sistema

Si el escritorio tiene bandeja, cerrar la ventana **no detiene la protección**:

- **Mostrar** — vuelve a abrir la ventana.
- **Activar / Desactivar protección** — cambia el estado sin abrir la ventana.
- **Salir** — detiene el monitor y cierra la aplicación por completo.

Al cerrar la ventana por primera vez, USBGuardGo muestra un aviso explicando que sigue en la bandeja. Si el escritorio no tiene bandeja, la aplicación se cierra al cerrar la ventana; en ese caso, mantén la ventana abierta mientras quieras proteger el equipo.

## Idiomas

La interfaz está disponible en:

- Español
- English
- 中文 (chino simplificado)
- Русский (ruso)
- Deutsch (alemán)
- Português (portugués)
- 한국어 (coreano)
- العربية (árabe, con disposición de derecha a izquierda)

El cambio se aplica al instante desde **Ajustes → Idioma** y no requiere reiniciar.

## Datos y registro

- Configuración: `~/.config/usbguardgo/config.json` (permisos `600`).
- Registro: `~/.config/usbguardgo/usbguardgo.log` (rotación automática).
- Exportación: `~/usbguardgo-registro.txt` al pulsar **Exportar registro**.

Para borrar la configuración sin abrir la aplicación:

```bash
usbguardgo --reset-config
```

El registro sirve para diagnosticar problemas. Antes de compartirlo, revisa que no contenga números de serie o nombres de dispositivos que prefieras mantener privados.

## Atajos y línea de comandos

| Comando | Efecto |
|---|---|
| `usbguardgo` | Abre la ventana principal |
| `usbguardgo --tray` | Arranca oculto en la bandeja |
| `usbguardgo --version` | Muestra la versión |
| `usbguardgo --reset-config` | Borra la configuración y sale |

## Buenas prácticas

- Mantén `usbguard` instalado si tu distribución lo soporta; el bloqueo de kernel es más fuerte que el bloqueo suave.
- No permitas «siempre» un dispositivo solo porque tiene un nombre conocido: los nombres se pueden falsificar.
- Revisa **Reglas** de vez en cuando y borra aparatos que ya no uses.
- Si encuentras un dispositivo bloqueado que necesitas, desbloquéalo desde **Dispositivos** o **Reglas**, no desactives toda la protección.
- Recuerda que USBGuardGo no sustituye al cifrado ni al control físico del equipo.
