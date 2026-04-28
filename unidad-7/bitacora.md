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
 ¿Cuál es la diferencia entre una CPU y una GPU?
 - La CPU está diseñada para ejecutar pocas tareas complejas de forma secuencial, mientras que la GPU está diseñada para ejecutar muchas tareas simples en paralelo.



### Actividad 5

  
</details>

<details>
<summary>Bitácora de aplicación</summary>

### Fase 1
```
#include <glad/glad.h>
#include <GLFW/glfw3.h>
#include <iostream>
#include <cmath>

const unsigned int SCR_WIDTH = 800;
const unsigned int SCR_HEIGHT = 600;

unsigned int VAO, VBO;
unsigned int shaderProg;

const char* vertexShaderSource = R"(
#version 460 core
layout(location = 0) in vec3 aPos;
uniform vec2 offset;

void main() {
    vec3 newPos = aPos;
    newPos.x += offset.x;
    newPos.y += offset.y;
    gl_Position = vec4(newPos, 1.0);
}
)";

const char* fragmentShaderSource = R"(
#version 460 core
out vec4 FragColor;
uniform vec4 ourColor;

void main() {
    FragColor = ourColor;
}
)";

void setupTriangle() {
    float vertices[] = {
        -0.5f, -0.5f, 0.0f,
         0.5f, -0.5f, 0.0f,
         0.0f,  0.5f, 0.0f
    };

    glGenVertexArrays(1, &VAO);
    glGenBuffers(1, &VBO);

    glBindVertexArray(VAO);
    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3*sizeof(float), (void*)0);
    glEnableVertexAttribArray(0);

    glBindVertexArray(0);
}

unsigned int buildShaderProgram() {
    unsigned int vShader = glCreateShader(GL_VERTEX_SHADER);
    glShaderSource(vShader, 1, &vertexShaderSource, NULL);
    glCompileShader(vShader);

    unsigned int fShader = glCreateShader(GL_FRAGMENT_SHADER);
    glShaderSource(fShader, 1, &fragmentShaderSource, NULL);
    glCompileShader(fShader);

    unsigned int program = glCreateProgram();
    glAttachShader(program, vShader);
    glAttachShader(program, fShader);
    glLinkProgram(program);

    glDeleteShader(vShader);
    glDeleteShader(fShader);

    return program;
}

int main() {
    glfwInit();

    GLFWwindow* window = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Triangulo", NULL, NULL);
    glfwMakeContextCurrent(window);

    gladLoadGLLoader((GLADloadproc)glfwGetProcAddress);

    shaderProg = buildShaderProgram();
    setupTriangle();

    int offsetLoc = glGetUniformLocation(shaderProg, "offset");
    int colorLoc = glGetUniformLocation(shaderProg, "ourColor");

    while (!glfwWindowShouldClose(window)) {

        float time = glfwGetTime();

        float offsetX = sin(time) * 0.5f;
        float offsetY = cos(time) * 0.5f;

        float r = (sin(time) + 1) / 2;
        float g = (cos(time) + 1) / 2;

        glClearColor(0.1f, 0.1f, 0.1f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT);

        glUseProgram(shaderProg);

        glUniform2f(offsetLoc, offsetX, offsetY);
        glUniform4f(colorLoc, r, g, 0.3f, 1.0f);

        glBindVertexArray(VAO);
        glDrawArrays(GL_TRIANGLES, 0, 3);

        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    glfwTerminate();
    return 0;
}
```

### Evidencia 1 — Contexto y carga de OpenGL
Breackpoint: ```gladLoadGLLoader((GLADloadproc)glfwGetProcAddress);```



Explicación: Significa que GLFW ya creó correctamente la ventana y el contexto.

Justificación: Coloco el breakpoint en gladLoadGLLoader porque es el punto donde se conectan GLFW y OpenGL. Verifico que la ventana no sea NULL para asegurar que el contexto existe antes de cargar funciones.

### Evidencia 2 — Del arreglo al shader
Breackpoint: ```glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);```



Explicación: Que los datos están en CPU listos para enviarse a la GPU.

Justificación: Ubico el breakpoint en glBufferData porque es el momento exacto donde los datos pasan del CPU a la GPU. Verifico que el arreglo tenga los valores correctos antes de enviarlos.

### Evidencia 3 — Uniform y cambio visual
Breackpoint: ```glUniform2f(offsetLoc, offsetX, offsetY);```



Explicación: Que el valor cambia en cada frame (dinámico).

Justificación: Coloco el breakpoint en glUniform porque quiero demostrar que el cambio visual no depende del VBO sino de un valor dinámico enviado al shader.

### Evidencia 4 — Prueba de borde
Breackpoint: ```glUniform2f(offsetLoc, 5.0f, 5.0f);```



Explicación: Se salió del rango NDC [-1,1]

Justificación: El breakpoint se coloca en el envío del uniform extremo para verificar el valor enviado y correlacionarlo con la desaparición del objeto en pantalla.

### Evidencia 5 — Responsabilidad del pipeline
Breackpoint: ```glDrawArrays(GL_TRIANGLES, 0, 3);```



Explicación: Que el pipeline está listo: shader activo, datos cargados, VAO activo.

Justificación: Coloco el breakpoint en glDrawArrays porque es el punto donde todo el pipeline se ejecuta. Verifico que los IDs del VAO y shader estén activos para asegurar que la GPU tiene todo lo necesario para dibujar.

  
</details>

<details>
<summary>Bitácora de reflexión</summary>
  
</details>
