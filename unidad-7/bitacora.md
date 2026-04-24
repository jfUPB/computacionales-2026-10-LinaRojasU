# Unidad 7

<details>
<summary>Bitácora de proceso de aprendizaje</summary>

### Actividad 1
Una captura de pantalla del triángulo funcionando en tu máquina.
<img width="399" height="421" alt="image" src="https://github.com/user-attachments/assets/83c0fc0a-acd6-4a61-924c-9e2f552b8d04" />

Al menos tres preguntas que te surjan al ver el código.
- ¿Cómo sabe el programa dónde dibujar el triángulo en la pantalla?
- ¿Qué función cumplen los shaders dentro del programa?
- ¿Por qué es necesario usar estructuras como VBO y VAO?

Una primera hipótesis: ¿Qué crees que necesita el programa para dibujar ese triángulo?
Para dibujar el triángulo, el programa necesita definir los vértices en el CPU, enviarlos a la GPU mediante buffers (como VBO y VAO), y procesarlos usando shaders que determinan su posición y color en pantalla.

### Actividad 2
Resumen
Para que un programa OpenGL funcione en Windows no basta con escribir código en C++, sino que se necesita una conexión entre varias capas que permiten que lo que escribo termine ejecutándose en la GPU.
Primero, GLFW se encarga de crear la ventana y el contexto OpenGL. Es decir, sin GLFW no tendría dónde dibujar ni cómo interactuar con teclado o mouse.
Luego aparece opengl32.lib, que es la biblioteca base de Windows. Esta permite enlazar el programa con OpenGL, pero solo ofrece funciones antiguas (hasta la versión 1.1). Aun así, es necesaria porque actúa como punto de entrada al sistema gráfico.
Sin embargo, como hoy en día usamos funciones modernas de OpenGL (3.3, 4.6), esas funciones no están en opengl32.lib, sino en los drivers de la GPU. Aquí es donde entra GLAD, que funciona como un cargador: consulta al driver y obtiene las direcciones de esas funciones para poder usarlas en el programa.
Por otro lado, GLM es una biblioteca matemática que facilita trabajar con vectores y matrices. No es obligatoria, pero es muy útil para transformaciones como mover, rotar o escalar objetos.


### Actividad 3
¿Qué pasa? ¿Qué observas? ¿Qué crees que está pasando?
El triángulo solo se dibuja en una parte de la pantalla (esquina superior izquierda o derecha dependiendo de los valores).

Resumen
En esta actividad entendí que para dibujar con OpenGL no basta con escribir funciones, sino que se necesita un contexto OpenGL, que es el entorno donde se guarda todo el estado gráfico (shaders, buffers, configuraciones, etc.).

Ese contexto lo crea GLFW, que además se encarga de crear la ventana y manejar eventos. Una vez creado, OpenGL puede comunicarse con la GPU a través de ese contexto.

También comprendí que el dibujo no ocurre directamente en pantalla, sino en el framebuffer, que es una memoria donde la GPU construye la imagen antes de mostrarla. Luego, mediante el doble buffering, esa imagen se intercambia y se muestra en pantalla.

Otro concepto clave es el viewport, que define qué parte del framebuffer se usa para dibujar. Si este no coincide con el tamaño del framebuffer, la imagen puede verse deformada o incompleta.

Finalmente, entendí que el programa funciona dentro de un game loop, donde en cada iteración se procesan eventos, se limpia la pantalla y se vuelve a dibujar la escena.

¿Qué pasa si cambias el primer parámetro de glDrawArrays a GL_LINES? ¿Qué pasa si lo cambias a GL_POINTS? ¿Qué pasa si cambias el tercer parámetro a 2? ¿Qué pasa si lo cambias a 4?
GL_LINES: Se ven líneas en lugar de triángulo.
GL_POINTS: Se ven puntos.
Parámetro a 2: No se forma un triángulo.
Parámetro a 4: Comportamiento inesperado (puede intentar formar más figuras).

### Actividad 4

### Actividad 5

  
</details>

<details>
<summary>Bitácora de aplicación</summary>
  
</details>

<details>
<summary>Bitácora de reflexión</summary>
  
</details>
