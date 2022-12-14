## Usar Salida Digital

Se usa salida digital mediante el pin 2 `Pin(2, Pin.OUT)`, el programa hace encender y apagar el pin seleccionado en intervalos de 1 segundo, adicionalmente se muestra información de la acción con la función `print()`

```python
from machine import Pin
from time import sleep

led = Pin(2, Pin.OUT)

try:
    while True:
        led.on()
        print("on")
        sleep(1)
        led.off()
        print("off")
        sleep(1)
except:
    led.off()
    print("finaliza")
```

## Usar Entrada Digital

Se usa la entrada digital mediante el pin 23 `Pin(23, Pin.IN)`, el programa lee el estado del pin mediante la función `pb.value()` la cual retorna 1 si lee voltaje o 0 si no lo hay, de otra forma 1 cuando el boton el presionado y 0 cuando no. Dependiendo del estado se realiza una acción u otra.

```python
from machine import Pin
from time import sleep

pb = Pin(23, Pin.IN)
led = Pin(2, Pin.OUT)

try:
    while True:
        estado = pb.value()
        sleep(1)
        if estado == 0:
            led.on()
            print("led on")
        else:
            led.off()
            print("led off")
except:
    led.off()
    print("finaliza")
```

## Usar Entrada Analógica

Uso de entrada analogica usando el pin 34 `ADC(Pin(34))`, y se lee el voltaja analógico mediante la función `entradaAnalogica.read()`. Ese valor que retorna la función _._read()_ se puede ajustar a un rango específico mediante `lectura / 4095.0 * 100.0` ese número 100 se puede cambiar por el rango que necesite..

```python
from machine import Pin, ADC
from time import sleep

entradaAnalogica = ADC(Pin(34))

try:
    while True:
        lectura = entradaAnalogica.read()
        ajusteEscala = lectura / 4095.0 * 100.0
        print("lectura: ", lectura, "ajuste Escala: ",ajusteEscala)
        sleep(1)
except:
    print("finaliza")
```

## Usar función input

La función `input()` permite ingresar datos desde teclado, destacando que siempre se guardan como texto sin importar si se trata de números, por tanto si desea leer números puede usar la función `int()` para convertir a números enteros o `float()` para números con coma; además puede usar _input()_ dentro de estas funciones para usar menos líneas de código.

```python
nombre = ""
edad = 0

try:
    print("Bienvenido al bar La Oficina!")
    nombre = input("¿Cuál es su nombre? ")
    edad = int(input("¿Cuántos años tiene? "))
    if edad < 18 :
        faltan = 18 - edad
        print("Lo siento ", nombre, " no puede entrar")
        print("Le faltan ", faltan, "año(s)")
    else:
        print("Adelante " + nombre)
except:
        
```

## Uso de listas o arrays

Las listas o arrays o también llamados vectores, permiten agrupar una serie de datos de manera ordenada y se puede acceder a ellos a través de la posición: `listaX[posición]` donde la _posición_ es un valor entero que empieza en cero para el primer valor.

```python
listado = ["Esto", "es", "una", "lista"]

try:
    # imprime el último de la lista de 4, el primero sería el 0
    print(listado[3])

    # cambio el valor del tercero de la lista 
    listado[2] = "UNA"

    # forma rápida de imprimir la lista
    print(listado)
    
    # forma de recorrer la lista para llenarla o cambiar valores
    for posicion in range( len(listado) ):
        listado[posicion] = input("Digite un valor: ")
    
    # otra forma de recorrer la lista, generalmente para mostar valores únicamente.
    for recorreLista in listado:
        print(recorreLista)
except:
    print("finaliza")
```

## Recorrer una lista a voluntad

Para recorrer la lista de manera manual se debe controlar la posicion de la lista, para tal fin se puede usar una variable a modo de conteo para que en determinado suceso haya un incremento de esta variable. una implementación rápida podría ser la siguiente:

```python
from machine import Pin, ADC
from time import sleep

entradaAnalogica = ADC(Pin(34))

conteo = 0

personas = ["Monica", "Saul", "Alex"]

try:
    while True:
        
        lectura = entradaAnalogica.read()

        if lectura < 1000:
            
            print("Ahora le toca a: ", personas[conteo])
            
            conteo = conteo + 1

            if conteo == 3:
                conteo = 0

except:
    print("finaliza")
```

![Sin control de cambios](../imgs/Sincontrol.gif)

El problema de la anterior solución es que si la condición no cambia rápido el conteo se incrementa rápidamente y por ende la lista se recorre en un solo ínstante; para evitar este problema hay que llevar registro de los valores anteriores de esta forma si ya sucedió un cambio antes que no se repita hasta que se vuelva a presentar la situación, de esta forma el coódigo queda de la siguiente manera:

```python
from machine import Pin, ADC
from time import sleep

entradaAnalogica = ADC(Pin(34))

conteo = 0

debeCambiar = False
cambioAnterior = False

personas = ["Monica", "Saul", "Alex"]

try:
    while True:
        
        lectura = entradaAnalogica.read()

        if lectura < 1000:
            debeCambiar = True
        else:
            debeCambiar = False

        if debeCambiar == True and cambioAnterior == False:
            
            print("Ahora le toca a: ", personas[conteo])
            
            conteo = conteo + 1

            if conteo == 3:
                conteo = 0
        
        cambioAnterior = debeCambiar

except:
    print("finaliza")
```

![Con control de cambios](../imgs/controlado.gif)

## Uso de entrada Analogica para controlar una salida

Usar el valor de la entrada analógica para controlar una salida digital.

```python
from machine import Pin, ADC
from time import sleep

entradaAnalogica = ADC(Pin(34))

switch = Pin(22, Pin.IN)

led = Pin(2, Pin.OUT)

try:
    while True:
        
        lectura = entradaAnalogica.read()

        modoOperacion = switch.value()

        if modoOperacion == 1:

            print("modo automatico")

            if lectura < 1000:
                print("regando planta")
                led.on()
            else:
                led.off()

        else:

            print("modo manual")
        
        sleep(1)
except:
    print("finaliza")
```

![Simulación parte ejercicio](../imgs/analog_outdig.gif)