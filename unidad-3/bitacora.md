# Unidad 3

## Bitácora de proceso de aprendizaje

 ### Actividad 1 

  #### ¿Para qué sirven los breakpoints?
  > Son para poder compilar el programa en una linea especifica del codigo.

  #### ¿Para qué se usa la ventana de depuración Autos?
  > Para entrar o salir de funciones a la hora de compilar, tambien para compilar en orden consecutivamente segun cada linea de codigo 

 ### Actividad 2 
  #### C++
  ```
#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void swapPorValor(int a, int b) {
    int c = b;
    b = a;
    a = c;
    
}

// Función que modifica el parámetro pasado por referencia
void swapPorReferencia(int& a, int& b) {
    int c = b;
    b = a;
    a = c;

}

// Función que modifica el parámetro utilizando punteros
void swapPorPuntero(int* a, int* b) {
    int c = *b;
    *b = *a;
    *a = c;
    
}

int main() {
    int a = 10;
    int b = 30;

    swapPorValor(a, b);
    cout << "Swap Por Valor:" << endl;
    cout << "a: " << a << endl;
    cout << "b: " << b << endl;

    swapPorReferencia(a, b);
    cout << "Swap Por Referencia:" << endl;
    cout << "a: " << a << endl;
    cout << "b: " << b << endl;

    swapPorPuntero(&a, &b);
    cout << "Swap Por Puntero:" << endl;
    cout << "a: " << a << endl;
    cout << "b: " << b << endl;

    return 0;
}
  ```

##### Swap Por Valor:
<img width="1089" height="683" alt="image" src="https://github.com/user-attachments/assets/b075467e-447d-4166-a654-19fa6fc57685" />

##### Swap Por Referencia:
<img width="1181" height="607" alt="image" src="https://github.com/user-attachments/assets/60135ce6-39a1-41bc-925f-982afc9a960c" />

##### Swap Por Puntero:
<img width="1254" height="623" alt="image" src="https://github.com/user-attachments/assets/1bdfbc41-45ff-42e4-843e-5aba9394aefb" />


 ### Actividad 3 
#### Segmento de código:
 > Son todas las instrucciones y funciones que hemos puesto en el codigo que estan fuera del Main.

#### Variables globales y estáticas:
 > Son las variables que instanciamos en el Main y se pueden usar en todo el resto del codigo.

#### Heap:
 > Es lo que se guarda en memoria pero solo son las variables u objetos creados con "new"

#### Stack:
 > Son las variables locales que se crean en cada función y cuando salimos de cada función estas variables se eliminan.

 ### Actividad 4 
 
#### Experimento 1
##### ¿Qué ocurre? ¿Por qué?
 > Ocurre un error en la linea 18, al intentar escribir en la dirección de main ya que las instrucciones del programa (el segmento de texto, donde están las funciones) normalmente están en memoria marcada como ejecutable y de sólo lectura por el sistema operativo y el intentar escribir ahí viola la protección de memoria del proceso.

#### Experimento 2
##### ¿Qué ocurre? ¿Por qué?
 > Ocurre un error en la linea 22, ya que Las cadenas literales son de sólo lectura.

#### Experimento 3
##### ¿Qué ocurre? ¿Por qué?
 > Todo funciona correctamente ya las variables globales están inicializadas y no inicializadas y se puede escribir y leer de ellas libremente. Esto ocurre porque las variables globales residen en memoria accesible y no están sujetas a la protección de sólo lectura. Cambiar sus valores simplemente modifica esas celdas de memoria.

#### Experimento 4
##### ¿Qué ocurre? ¿Por qué? Qué pasa con las variables cada que entras y sales de la función? ¿Qué pasa con las variables locales estáticas?
 > El programa nos avisa de que hay un error de compilación esto ocurre ya que a la variable ```var_estatica``` no tiene un tipo de dat cuando esta en el main, funciona dentro de la función ```funcionConStatic``` ya que ahi si tiene tipo de dato y ya cuando nosotros salimos de esa función todas las variables que habain en ella se eliminan.

#### Experimento 5
##### ¿Qué ocurre? ¿Por qué? ¿Ves alguna diferencia entre las variables locales estáticas y no estáticas? ¿Qué pasa con las variables cada que entras y sales de la función?
 > ```funcSinStatic():``` cada llamada imprime 100 y luego incrementa su variable local automática. Pero ese incremento no se observa en la siguiente llamada porque la variable automática se crea de nuevo en cada invocación y su incremento no persiste. Esto pasa porque la local no estática vive en el stack, su valor no persiste necesariamente entre llamadas. Y la local estática vive en la sección de datos (misma que variables globales), se inicializa una vez y persiste por toda la ejecución.

#### Experimento 6
##### ¿Qué ocurre? ¿Por qué? Comenta la línea de genera el error y analiza las siguientes preguntas: ¿Qué diferencias notas entre el comportamiento y la gestión del Heap en comparación con el Stack? ¿Qué consecuencias tendría no liberar la memoria reservada con new? ¿Por qué es importante usar delete[] al liberar memoria asignada para un arreglo?
 > Acceder a arrayHeap[0] después de delete[] es comportamiento indefinido ya que delete[] libera la memoria al allocator del proceso. El puntero arrayHeap queda pendiente y apunta a memoria que el programa ya no posee. Leer/escribir ahí es UB.
 > En el Stack la gestión automática por el compilador/CPU, al salir de la función, la memoria del stack se libera automáticamente y tiene un tamaño limitado.
 > En el Heap: la gestión manual, persiste hasta que la liberes explícitamente y puede fragmentarse; su performance depende del allocator.

 > Memory leak: el proceso consume más memoria con el tiempo. En programas cortos puede no notarse, pero en servidores o procesos prolongados provoca agotamiento de memoria y degradación de rendimiento.

 > delete[] asegura que se llamen los destructores de cada elemento del arreglo y que el allocator libere el bloque correctamente. Usar delete (sin []) para memoria asignada con new[] es UB: el comportamiento es indefinido y puede corromper el heap o provocar fugas/destructor faltantes.

### Actividad 5 
##### ¿Qué ocurre? ¿Por qué? 

#### Explica qué ocurre al copiar un objeto en C++ y en C#. ¿Qué diferencias encuentras?
 > En C# no se puede copiar los objetos igual que en C++, ya que en C# original y copia continene la misma direccion en el Heap o sea que en la memoria son el mismo objeto.

#### ¿Qué es copia en C++ y en C#? ¿Es una copia independiente de original?
 > Una copia en C++ es copiar y pegar los contenidos del objeto original a la copia, o sea que creamos dos objetos diferentes, en C# la copia no es independiente de original por que solo hemos creado un objeto y la copia se convierte en ese mismo objeto.


## Bitácora de aplicación 

 ### 1. Diagnóstico del problema (análisis):
#### Error A
¿Cuál es el error?
 > Se reserva memoria con ```new int[3]``` en el constructor y por ende nunca se libera porque no hay ```delete[]``` en destructor.

¿Por qué ocurre? Explica el mecanismo a nivel de memoria (stack, heap, punteros)
 > ```estadisticas``` apunta a un bloque en el heap. Cuando ```simularEncuentro()``` termina, los objetos locales (heroe, copiaHeroe) se destruyen, pero como no hay destructor que haga delete[] en ```estadisticas```, el bloque del heap queda sin referencia por lo que nadie puede liberarlo.

¿Cuál es su consecuencia?
 > Con ejecuciones repetidas (o muchos personajes), el juego consumirá cada vez más RAM y terminará agotando la memoria.

#### Error B
¿Cuál es el error?
 > La copia ```Personaje copiaHeroe = heroe;``` usa el copy-constructor por defecto copia bit a bit el puntero ```estadisticas```.Lo que resulta que ambos objetos apuntan al mismo arreglo en heap.

¿Por qué ocurre? Explica el mecanismo a nivel de memoria (stack, heap, punteros)
 > El puntero ```estadisticas``` es sólo un valor (dirección). El copy por defecto copia esa dirección; no lo duplica. Así ```heroe.estadisticas == copiaHeroe.estadisticas``` (mismo puntero).

¿Cuál es su consecuencia?
 > Si alguien modifica ```copiaHeroe.estadisticas[0]```, también modifica ```heroe.estadisticas[0]```.
 > Si se implementa un destructor que haga ```delete[] estadisticas;```, entonces cuando se destruyan ambos (al salir del scope), se hará ```delete[]``` dos veces sobre la misma dirección.

 ### 2. Usa el depurador:
#### Error A
<img width="1862" height="531" alt="image" src="https://github.com/user-attachments/assets/1cf8f826-4f68-47c6-a9de-a08cf1672308" />
 > Se puede envidenciar una fuga en la memoria.

#### Error B
<img width="1483" height="853" alt="image" src="https://github.com/user-attachments/assets/76480a8e-f69c-4a6e-bd97-f581a3a84a43" /> 
 > se realiza una copia superficial del objeto.
Esto significa que el puntero estadisticas se copia tal cual, no el contenido que apunta.

 ### 3. Induce los fallos:
#### Error A
<img width="1893" height="866" alt="image" src="https://github.com/user-attachments/assets/7d46e1ce-fe7b-47e1-8194-bead52b34c65" />

<img width="1869" height="608" alt="image" src="https://github.com/user-attachments/assets/93074974-0b32-421f-b6f0-de4f8ef5f8e8" />
 > En cada iteración se reserva memoria dinámica en el heap mediante new int[3].
Al finalizar la función simularEncuentro(), los objetos locales se destruyen, pero el bloque de memoria del heap permanece sin liberar debido a la ausencia de un destructor con delete[].
Esto produce una fuga de memoria acumulativa, evidenciada por el incremento progresivo del uso de RAM en el depurador.

#### Error B
<img width="945" height="983" alt="image" src="https://github.com/user-attachments/assets/df460b33-a2bf-4d46-9e1f-35dcde69ad59" />

<img width="1327" height="849" alt="image" src="https://github.com/user-attachments/assets/d814f1e7-92a4-4cc4-86a4-b817f7da2ab9" />
 > Al copiar el objeto Personaje, el compilador realiza una copia superficial del puntero estadisticas.
Como resultado, ambos objetos apuntan al mismo bloque del heap.
Al finalizar la función, ambos destructores intentan liberar la misma dirección de memoria, produciendo doble liberación, corrupción del heap y fallo de ejecución.

 ### 4. Solución y refactorización (síntesis y creación):
```
#include <iostream>
#include <string>
#include <array>

class Personaje {
public:
    std::string nombre;
    std::array<int, 3> estadisticas; // vida, ataque y defensa

    // Constructor
    Personaje(const std::string& n, int vida, int ataque, int defensa)
        : nombre(n), estadisticas{ vida, ataque, defensa }
    {
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    // Método para imprimir
    void imprimir() const {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }

    // Ejemplo de método para modificar una estadistica
    void setVida(int v) { estadisticas[0] = v; }
    int getVida() const { return estadisticas[0]; }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```

 ### 5. Justificación de la Solución:
> Elimina la gestión manual de memoria (```new[]/delete[]```):
```std::array<int,3>``` es un objeto valor que contiene los 3 int directamente en la instancia. No hay heap dinámico interno, por tanto no hay fugas relacionadas con esas estadísticas.

> Copia segura por defecto (semántica de valor):
El copy-constructor por defecto para ```std::array``` realiza una copia de los elementos. Al hacer ```Personaje copiaHeroe = heroe```;, ```estadisticas``` se copian (cada objeto obtiene su copia de los 3 ints). No hay aliasing, no hay doble free ni efectos colaterales.

> Sin destructor manual hace que hayan menos posibilidades de error: no hay que escribir delete ni implementar la Regla de Tres. std::string y std::array manejan sus propios recursos.

> Semántica clara ya que las modificaciones en la copia no afectan al original, lo que es lo esperado en la mayoría de los casos.

## Bitácora de reflexión

 ### 1. recuperación de conocimiento (Retrieval Practice)
  #### Explica con tus propias palabras qué es el stack y qué es el heap en C++.
  >

  #### Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.
  >

  #### ¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?
  >

  #### Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?
  >

 ### 2. transferencia y análisis de situación nueva
  #### Análisis de problemas: identifica al menos dos problemas serios en este código relacionados con el manejo de memoria. Explica por qué cada uno es problemático.
  >

  #### Predicción de comportamiento: ¿Qué valor mostrará totalEnemigos después de ejecutar el programa? ¿Por qué ocurre esto?
  >

  #### Propuesta de solución: escribe una versión corregida de la clase Enemigo que solucione los problemas identificados. Explica brevemente cada cambio que hiciste.
  >

 ### 3. reflexión metacognitiva
  #### De todos los conceptos que exploraste en esta unidad (stack vs heap, paso de parámetros, ciclo de vida de objetos, etc.), ¿Cuál consideras que es el más crítico para evitar errores en programas reales? ¿Por qué?
  >

  #### ¿Cómo cambió tu comprensión sobre lo que realmente es un “objeto” después de comparar C++ con C#? ¿Qué implicaciones prácticas tiene esta diferencia?
  >

  #### Si tuvieras que explicar a un compañero de semestres anteriores por qué es importante entender la gestión de memoria en programación, ¿Qué le dirías en máximo 3 oraciones?
  >



