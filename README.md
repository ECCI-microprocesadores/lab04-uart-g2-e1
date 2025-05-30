[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=19508560&assignment_repo_type=AssignmentRepo)
# Lab04: Comunicación UART en PIC18F45K22

## Integrantes

Sofy Parra

Carlos Sierra

Edisson Fonseca

## Documentación
Implementamos  un programa el cual nos permite leer el valor de una señal analógica a través del módulo ADC del microcontrolador PIC18F45K22, convertir este valor a voltaje y enviarlo mediante comunicación serial UART al monitor serial el cual se puede visualizar ya sea en el monitor serial de Arduino o en este caso por medio del programa putty. 

### Inicialización del sistema:
1. Confirguramos el  oscilador interno a 16 MHz.
2. Se inicializan los módulos UART y ADC.
### Lectura del ADC:
1. Lee una señal analógica conectada al pin RA0 (AN0) del microcontrolador.
2. El valor que lee  es un número entre 0 y 1023 (resolución de 10 bits).
3. Este valor es convertido a voltaje usando la fórmula:

![Esquematico uart](https://github.com/ECCI-microprocesadores/lab04-uart-g2-e1/blob/b0cf529045f8000e33a2f0713ee7b01376f31af2/imagenes/formula.png)

### Envío por UART:
1. Se usa ```c sprintf()``` para formatear una cadena de texto con el valor ADC y el voltaje calculado.
2. Se transmite esta cadena por el puerto serial (UART) usando ``` UART_WriteString().```
### Codigo:
 Definimos que el  PIC está trabajando con una frecuencia de 16 MHz
 ```#define _XTAL_FREQ 16000000UL``` 
 Inicializacion del sistema de lectura:
1. Registro OSCCON nos permite el control del oscilador, nos permite establecer la velocidad (frecuencia) del reloj
```c 
OSCCON= 0b01110010
```
2. Inicializa el módulo de comunicación serial (UART) y el módulo de conversión analógica-digital (ADC).
```c 
UART_Init()
ADC_Init()
```
3. Lee el valor digital (entre 0–1023)desde el canal AN0.
```c 
uint16_t adc_val = ADC_Read();
```
4. Convierte el valor digital a voltaje real (0–5V), suponiendo una referencia de voltaje de 5V
```c 
float volt = (adc_val * 5.0f) / 1023.0f;
```
5. Formatea y transmite por UART el valor leido y el voltaje en formato legible.
```c 
sprintf(buffer, "Adc:%04u Voltaje:%.2fV\r\n", adc_val, volt);
UART_WriteString(buffer);
```
% → Indica el inicio de un especificador de formato.

0 → Rellena con ceros a la izquierda si el número tiene menos cifras.

4 → Ancho total del número: 4 dígitos como mínimo.

u → Tipo de dato: entero sin signo (uint16_t).

#### Si adc_val = 23, se imprimirá como:
Adc:0023
%.2f
Este es un formato de impresión para números de punto flotante (float), y se desglosa así:

% → Comienzo del formato.

.2 → Muestra 2 cifras decimales.

f → Tipo de dato: float (número real).

#### Si volt = 3.45678, se imprimirá como:
    Voltaje:3.46
#### Finalmente podremos visualizarlo de la siguiente manera: 
```c 
Adc:0235 Voltaje:1.15V  (Monitor serial Putty)
```

## Implementación: 

![Montaje](https://github.com/ECCI-microprocesadores/lab04-uart-g2-e1/blob/e5e83744b1f735c9da46457d89507e6abeb4b129/imagenes/ImplementacionUART.png)

### Visualiacion en Putty:
El potenciómetro funciona como un divisor de voltaje. Al girar el eje, el voltaje en el pin RA0 varía de 0V a 5V, lo que se refleja en la lectura del ADC y en el monitor serial.


## Diagramas

### Diagrama esquematico

![Esquematico uart](https://github.com/ECCI-microprocesadores/lab04-uart-g2-e1/blob/b590df00dbe48c9765f13c197b50395f50089645/imagenes/UART.png)

### Diagrama de flujo
![Diagrama de flujo](https://github.com/ECCI-microprocesadores/lab04-uart-g2-e1/blob/7ad270ec55b76cc3f9ace54f70b7ac90650bdebd/imagenes/flujoUART.png)





