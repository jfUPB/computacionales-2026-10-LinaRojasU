# Unidad 5
## Bitácora de proceso de aprendizaje
### Actividad 1

#### Parte 1
¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.
> El encapsulamiento es ocultar los datos internos de una clase y permitir que se acceda a ellos de forma controlada.

Ejemplo.
> Si tengo una clase CuentaBancaria, no sería buena idea que cualquiera pudiera cambiar el saldo directamente.

¿Por qué es útil?
> Porque evita errores, protege la información y hace que el programa sea más ordenado.


¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.
> La herencia es cuando una clase nueva toma características de otra clase.

Ejemplo.
> Si tengo una clase Vehiculo, puedo crear Carro y Moto como clases que heredan de Vehiculo, así no se tiene que repetir cosas como velocidad, color o moverse() en cada clase.

¿Por qué deberia usarse?
> Porque permite reutilizar código y organizar mejor el programa.


¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.
> El polimorfismo significa que una misma instrucción puede comportarse de forma distinta según el objeto real.

Ejemplo.
> Si tengo una lista de figuras y todas tienen el método Dibujar(), entonces puedo llamar Dibujar() a todas, pero cada figura dibuja algo distinto.

¿Qué significa que un código sea polimórfico?
> Que trabaja con un tipo general, pero al ejecutarse usa el comportamiento específico del objeto.


#### Parte 2
Encapsulamiento:
Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.

<img width="255" height="39" alt="image" src="https://github.com/user-attachments/assets/78aa86b6-2d3e-400a-be12-3174b2f9230b" />

> Esto es encapsulamiento porque el campo nombre no se puede cambiar directamente desde fuera de la clase.

¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?
> Porque así se controla mejor el acceso; nombre queda protegido, Nombre sirve como puerta de acceso controlada.

¿Qué problema se evita?
> Se evita que cualquier parte del programa cambie el nombre de forma incorrecta.


Herencia:
¿Cómo se evidencia la herencia en la clase Circulo?

<img width="333" height="31" alt="image" src="https://github.com/user-attachments/assets/dac033aa-13e6-4a32-9e40-6a6e40436db0" />

> Eso significa que Circulo hereda de Figura.

Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?
> También almacena lo que viene de Figura, como nombre.


Polimorfismo:
Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta; solo quiero que intentes razonar cómo podría ser.

> <img width="377" height="139" alt="image" src="https://github.com/user-attachments/assets/c764e4c8-0e2c-4ba5-8ff3-928433b3923d" />

> Aunque fig es de tipo Figura, en realidad puede contener un Circulo o un Rectangulo. Entonces, cuando se llama a fig.Dibujar(), el programa ejecuta el método correcto según el objeto real.

Mi hipótesis sería esta:

> El programa guarda qué tipo real tiene cada objeto, cuando llega la llamada Dibujar(), revisa ese tipo, luego ejecuta la versión correspondiente: si es Circulo, llama a Circulo.Dibujar() o si es Rectangulo, llama a Rectangulo.Dibujar().


#### Parte 3
Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?
> Cuando se crea un Rectangulo, ese objeto tiene todo junto: el nombre que viene de Figura, la base, la altura

¿Cómo lo imagino en memoria?
> Yo me lo imagino como un bloque único de memoria que contiene primero la parte heredada y luego la parte propia de la clase hija.

El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.
> Mi hipótesis es que cada objeto guarda una especie de referencia interna que le dice al programa qué versión del método debe ejecutar. Entonces, aunque la variable sea de tipo Figura, en tiempo de ejecución el programa revisa el objeto real y llama al método correcto, eso explicaría por qué Dibujar() cambia según el tipo del objeto.

La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?
> Yo creo que esto se revisa cuando se escribe y compila el código, no cuando el programa ya está corriendo. O sea: si intentas usar un miembro private desde afuera, el compilador te marca error, y no te deja ejecutar el programa.
> Y piesno esto ya que el problema es de reglas del lenguaje, no de comportamiento en pantalla.

### Actividad 2
Idea general de la aplicación.
> Este programa simula fuegos artificiales.
> Funciona así: cuando se hace clic en el mouse, aparece una partícula que sube desde abajo. Esa partícula va perdiendo estabilidad hasta que explota. Cuando explota, aparecen varias partículas nuevas con formas distintas: círculo, cuadrado, estrella.
> Todas las partículas se van actualizando y dibujando en pantalla y cuando una partícula termina su tiempo de vida, se elimina de memoria.

### Actividad 3

### Actividad 4

### Actividad 5 

## Bitácora de aplicación 


## Bitácora de reflexión
