# Python-para-sistemas-embebidos
Repositorio público con información de guía para el desarrollo de prácticas de programación de micropython en sistemas embebidos (esp32)

---

# La tarjeta de desarrollo [ESP32]
![ESP32 Pinout](https://4cc2f608-a-e6add100-s-sites.googlegroups.com/a/astro.unam.mx/oan_mantenimiento/sbc/esp32/ESP32-Pinout.jpg?attachauth=ANoY7cpKJQvl5Gh0RuLbnbABFOUnOTHbB4Ce3Um5mrP_wwhcx6hrRtv0l-33Of9o1wQWPjbEF8mllIe13A1BuV9xsn2eQi0QKKcOswoDlZ7eusmB92eSwPI4znLhVBKXKNrfxsaIcYjvj24064-I1F2UAYtcK7Xuja4kYeFBopWcfTXG151FYyiQ7yxN_8HqGlB3GD_2JXmaeMoP45NHrbapVi_TeEZmum58gBufjplluyqeQG_Xt6M%3D&attredirects=0)

ESP32 es una familia de microcontroladores de la empresa **Espressif Systems**. Cuenta con un microprocesador de 32-bits (dual core o single core), comunicación inalámbrica Wifi y Bluetooth. Su versión de dos núcleos se podría realizar un proyecto que intercambie información a la nube y en simultáneo administre datos de un sensor.

# MicroPython
Es una implementación sencilla y eficiente del lenguaje de programación **Python 3** que incluye un pequeño subconjunto de la biblioteca estándar de Python y está optimizado para ejecutarse en microcontroladores y en entornos restringidos.

# Instalación de micropython en Esp32

1. Descargar la herramienta `esptool.exe` _([para windows](https://dl.espressif.com/dl/esptool-2.3.1-windows.zip))_
2. Descargar el firmware `esp32-ota-20220618-v1.19.1.bin`, la carga de este archivo binario a la tarjeta esp32 permitirá programar en micropython.
3. Guardar los dos archivos dentro de la misma carpeta
4. Abrir cmd dentro de la carpeta mencionada, _puede acceder rápidamente a la carpeta escribiendo "cmd" en la ruta del explorador de archivos_.
5. Borrar todo programa guardado previamente en la esp32:
```cmd
esptool.exe --chip esp32 --port COM6 erase_flash
```
 - **Nota:** Recuerde seleccionar el puerto COM adecuado según donde se haya conectado la tarjeta.
 - Si el sistema operativo no reconoce la tarjeta, asegúrese de que tiene instalador el controlador requerido `CP210x` [Ir a página de descarga](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads)
6. Cargar el firmware:
```cmd
esptool.exe --chip esp32 --port COM6 --baud 460800 write_flash -z 0x1000 esp32-ota-20220618-v1.19.1.bin
```
 - **Nota:** En algunas tarjetas hay que mantener presionado el [ pulsador EN ] para forzar a la tarjeta a recibir el programa.
 
 # Instalación de Thonny _(entorno práctico de programación)_
 
 1. Descargue e instale el programa desde el [siguiente enlace](https://thonny.org/). _Durante la instalación puede traducirlo al español si lo desea_.
 2. Vaya a: Herramientas > Opciones [Se abre ventana de opciones]
 3. En la pestaña |Intérprete|, en el menú desplegable selecciones `MicroPython (ESP32)`
 4. Abajo en Puerto o WebREPL seleccione el puerto COM de la tarjeta. Finalmente presione [OK].
 
 - Thonny tiene dos entornos de trabajo, el superior es donde se desarrollan los códigos y en la parte inferior está la consola, con la cual puede interactuar directamente con la esp32.
 - Los programas los puede ejecutar directamente presionando el botón de play que se encuentra al lado del botón de guardar, o puede presionar la tecla [F5].
 - Para detener la ejecución del programa presiona Stop, o [Ctrl] + [F2].
 - **IMPORTANTE:** el programa se pierde una vez se detiene o se desconecta la tarjeta; para asegurar que el programa quede guardado en esta y que adicionalmente se ejecute en el arranque debe guardar el programa como `main.py` directamente en la tarjeta dando Archivo > Guardar como... si la tarjeta está conectada aparecerá una ventana que permite elegir si el código será guardado en el PC o directamente en la tarjeta.
 
 ## Uso adecuado de pines de la placa esp32
 
 La tarjeta opera a 3.3 voltios, y es sensible a voltajes superiores _(no tolera 5 voltios, se puede averiar)_ y a descarga estática por mala manipulación.
 Algunos pines se recomienda no usarlos ya que intervienen en algunas configuraciones de arranque, otros pines solo funcionan como entradas, en [este enlace](https://randomnerdtutorials.com/esp32-pinout-reference-gpios/) se detalla la disponibilidad de cada pin.
 
 # MicroPython para ESP32 en entorno de simulación
 
 **Wokwi** es un simulador de electrónica en línea. Puede usarlo para simular Arduino, ESP32 y muchas otras placas, piezas y sensores populares. Esta es una herramienta poderosa y versátil que incluso permite simular la tarjeta esp32 junto con programación en micropython.
 La plataforma es de libre acceso y se puede acceder haciendo [clic aquí](https://wokwi.com/projects/new/micropython-esp32).
 
 ---
 
 Info
