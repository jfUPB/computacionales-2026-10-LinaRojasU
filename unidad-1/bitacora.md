# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 01
#### Reporta tus observaciones para cada experimento en tu bitácora de aprendizaje.
 > R// -En el experimento número 1, el programa suma los números 1 y 2, guarda el resultado en RAM posición 16. El valor en 16 es 3. Pasa esto porque D empieza valiendo 1, luego se le suma 2 (dando 3) y al final M=D escribe ese 3 en la posición 16 escrita en A. A partir del ciclo 8 la CPU queda en un bucle permanente (salto a 7).
 > R// -En el experimento númreo 2, Funciona exactamente igual que el experimento anterior, con la diferencia que los números almacenados y sumados en D son el 5 y 10, y su resultado que es 15 se guarda en la memoria de RAM posicióin 20 en vez de la 16 como en el anterior experimento.

#### ¿Qué diferencia hay entre los datos almacenados en la memoria ROM y en la RAM?
 > R// La ROM guarda las instrucciones que le vamos dando, es basicamente lo que queremos que el computador haga. La RAM guarda los datos del programa, los números con los que el programa va a trabajar, estos valores pueden cambiarse progresivamente de posición y de valor como nosotros queramos en cualquier parte del programa.



### Actividad 02
#### Identifica una instrucción que use la ALU y explica qué hace.
 > R// En la posión 11 de la ROM: D=D-A 
 > La ALU calcula D - A y guarda el resultado en D. Si D = 16384 y A = 16384, el resultado es 0. 

#### ¿Para qué sirve el registro PC?
 > R// El registro PC guarda la posición ROM de la próxima instrucción a ejecutar. Después de cada instrucción PC se esta incrementa en 1, excepto cuando hay un salto que cambie PC a otra posición.

#### ¿Cuál es la diferencia entre @i y @READKEYBOARD?
 > R// Cuando se ejecuta @i el ensamblador lo convierte en @16 y, si despues se escribe M=..., Lo que guardaste se va almacenar en la posición 16 de la RAM.
 > @READKEYBOARD se usa para saltar a otro lugar del codigo en la ROM.

#### Describe qué se necesita para leer el teclado y mostrar información en la pantalla.
 > R// Leer teclado: leer la posición en memoria RAM 24576 (símbolo KBD). Si su contenido ≠ 0, el emulador indica que hay una tecla presionada por lo que pasa a pintar la pantalla.

#### Identifica un bucle en el programa y explica su funcionamiento.
 > R// El bucle que empieza en la etiqueta READKEYBOARD y vuelve a READKEYBOARD es básicamente la espera hasta que se apriete una tecla del programa.

#### Identifica una condición en el programa y explica su funcionamiento.
 > R// La condición de la instrucción D;JNE (justo después de leer KBD). D contiene lo que leyó del teclado. Si es distinto de 0 significa que hay una tecla presionada. Entonces el programa deja de esperar y ejecuta el código que maneja la tecla. Si D es 0, significa no hay tecla presionada, y el programa continúa en bucle esperando.

## Bitácora de aplicación 

 ### Activuidad 4

 ```
@12
M=0

@i
M=1

(LOOP)

@i
D=M
@6
D=D-A
@END
D;JEQ

@i
D=M
@12
M=D+M

@i 
M=M+1

@LOOP
0;JMP

@END
(END)
0;JMP

```

#### Resultado:

<img width="1543" height="798" alt="image" src="https://github.com/user-attachments/assets/01ac8ab7-10b7-4133-b9d9-5e5024d028a5" />


## Bitácora de reflexión

### Actividad 5

 #### Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?
  > R// Fetch: la CPU lee la siguiente instrucción desde la ROM, usando la posición que guarda el PC.
  > Decode: la CPU interpreta si es un valor en A, o si es una operación.
  > Execute: se realiza la operación, actualiza A o D y ejecuta la ALU.
  > El PC es el que recibe cada instruccion y cada una va incrementando a menos que haya un salto y se cambia de posición.

 #### ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.
  > R// Instrucción-A: pone un número en el registro A.
   > Ejemplo: @5. Pone 5 en A. 
  > Instrucción-C: le dice a ALU qué calcular y donde se va a guardar el resultado.
   > Ejemplo: D=D+A. La ALU suma D y y A, y se guarda el resultado en D. 
 
 #### Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.
  > R// Registro D: Se usa para guardar un valor temporalmente.
  > Registro A: Se usa para guardar direcciones o constantes.
  > La ALU: Es la parte que hace las cuentas u operaciones o D y A/M y nos lanza el resultado.

 #### ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).
  > R// Un salto condicional se implememnta cuando el computador mira un valor y decide si debe seguir con la siguiente instrucción o pasar a otro lugar del codigo.
  > Ejemplo: Salta si D es mayor que cero. La CPU revisa D y solo salta si cumple la condición de que D es mayor a cero. 

#### ¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).
 > R// Un loop se implememta con una etiqueta y un salto, la etiqueta marca el inicio y final del bloque se usa un salto para volver a la etiqueta del inicio.
 > Ejemplo: cuando una variable llega a 0. Mientras la condción no se cumple el programa vuelve al inicio del loop, cuadno se cumple sale del ciclo y continua con las siguientes instrucciones.

#### ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?
 > R// La diferencia es que la instrucción D=M es que el valor que tenga M se va a guardar en D y la instrucción M=D es al contrario, que el valor que hay en D se va a guardar en M.
 
#### Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).
 > R// Para leer el teclado, el computador solo necesita una dirección especial de memoria que representa el teclado. Si el valor que hay ahi no es 0, significa que una tecla esta siendo presionada.
 > Para pintar un pixel en pantalla el computador debe escrubir un valor en una zona especial de memoria que representa la pantalla. 





