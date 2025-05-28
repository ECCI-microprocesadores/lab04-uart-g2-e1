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
2. Se transmite esta cadena por el puerto serial (UART) usando 
```c
cUART_WriteString().
```

## Diagramas

### Diagrama esquematico

![Esquematico uart](https://github.com/ECCI-microprocesadores/lab04-uart-g2-e1/blob/b590df00dbe48c9765f13c197b50395f50089645/imagenes/UART.png)

### Diagrama de flujo


## Implmentación


