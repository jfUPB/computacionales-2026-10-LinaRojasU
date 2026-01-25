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



## Bitácora de reflexión


