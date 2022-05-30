QU� ES USBaspLoader
===================
USBaspLoader es uno de los varios bootloaders que QMK Toolbox reconoce para
flashear firmware a trav�s del puerto USB del teclado.

Un bootloader es un programa que reside en la memoria flash del microcontrolador
junto con el firmware principal y que toma el control en primer lugar al
conectarlo/resetearlo. Puede encargarse de varias tareas, como chequear
el hardware presente (ej. m�dulos Bluetooth), inicializarlo, etc. En el caso
de un teclado Powered by QMK el bootloader se ocupa de dejarlo en estado
programable para recibir un nuevo firmware por el puerto USB o pasarle el
control al programa de usuario para funcionar con normalidad. El bootloader
debe flashearse en el microcontrolador al principio de su vida �til. Una
vez instalado permite flashear cualquier firmware de QMK sobre USB.

QMK Toolbox soporta una lista cerrada de bootloaders que funcionan de manera
diferente. USBaspLoader se basa en comprobar en el momento del arranque/reset
si el usuario tiene pulsado el bot�n "Boot" de su teclado. En caso afirmativo
lo ancla como dispositivo serie (COM) preparado para ser flasheado desde QMK
Toolbox. En caso negativo lo ancla como dispositivo HID listo para trabajar.


MATERIAL NECESARIO
==================
Un bootloader no puede flashearse por USB. Se necesita un programador
In-Circuit que se que se conecta a la cabecera de pines ICSP del Torn,
como por ejemplo el USBasp dise�ado por Thomas Fischl. Para completar el
proceso de flasheo del bootloader en Windows con programador se necesita:

- Programador ICSP con sus correspondientes drivers. Para el USBasp:
  http://www.fischl.de/usbasp/usbasp-windriver.2011-05-28.zip
- AVRdudess.
  https://github.com/ZakKemble/AVRDUDESS/releases/download/v2.14/AVRDUDESS-2.14-setup.exe
- El archivo "USBaspLoader.hex" espec�fico del Torn.


PROCEDIMIENTO PARA FLASHEAR EL BOOTLOADER
=========================================
1) Instalar correctamente los drivers proporcionados con el programador ICSP.
2) Conectar el programador a la cabecera de 6 pines ICSP del Torn
   (vigilando el orden correcto del pin GND) y al PC por USB.
3) Abrir el ARVdudess.
4) En el apartado "Programmer" seleccionar el tipo de programador que se est�
   utilizando (ej. USBasp, http://www.fischl.de/usbasp/).
5) En el apartado "Bitclock" seleccionar 16KHz si el teclado tiene un ATmega328P
   de f�brica o 1.5MHz si tiene un ATmega328P pre-configurado.
6) En el apartado "Flash" buscar el archivo "USBaspLoader.hex" del Torn.
7) En el apartado "MCU" pulsar el bot�n "Detect", que deber�a identificar
   al ATmega328P.
8) Pulsar el bot�n "Program!".
9) En el apartado "Fuses & Lock bits" escribir los siguientes valores y
   pulsar "Write":
   L: 0xd7
   H: 0xd0
   E: 0xfc
   
   
PROCEDIMIENTO PARA FLASHEAR EL FIRMWARE DE QMK
==============================================
En este punto el teclado ya tiene instalado el USBaspLoader y se puede
flashear el firmware de QMK por USB:
1) Abrir el QMK Toolbox.
2) Conectar el Torn al PC manteniendo pulsado el bot�n "Boot".
   Si el teclado ya estaba conectado pulsar la siguiente secuencia:
   Pulsar y dejar pulsado "Boot", pulsar y soltar "Reset", soltar "Boot".
3) Una vez que QMK Toolbox detecta el teclado ya se puede subir un
   archivo .hex precompilado o compilar y subir una carpeta de QMK.


M�S INFORMACI�N
===============
C�digo fuente del USBaspLoader para el ATmega328P:

   https://github.com/rtitmuss/USBaspLoader/tree/torn

M�s informaci�n en espa�ol sobre bootloaders y teclados:

    https://www.tecleate.com
	
--
Versi�n actual:
   (c) 2022 by Exon David Brice�o
       tecleate@gmail.com

   (c) 2022 by Pablo Hurl�
       pablohurle79@gmail.com

Versi�n original:
   (c) 2018 by Richard Titmuss
   (c) 2013 by Stephan Baerwolf
   (c) 2008 by OBJECTIVE DEVELOPMENT Software GmbH.