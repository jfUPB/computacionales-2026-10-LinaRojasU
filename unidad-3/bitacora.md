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

 ### Actividad 5 

#### Explica qué ocurre al copiar un objeto en C++ y en C#. ¿Qué diferencias encuentras?
 > En C# no se puede copiar los objetos igual que en C++, ya que en C# original y copia continene la misma direccion en el Heap o sea que en la memoria son el mismo objeto.

#### ¿Qué es copia en C++ y en C#? ¿Es una copia independiente de original?
 > Una copia en C++ es copiar y pegar los contenidos del objeto original a la copia, o sea que creamos dos objetos diferentes, en C# la copia no es independiente de original por que solo hemos creado un objeto y la copia se convierte en ese mismo objeto.


 ### Actividad 6 

 ### Actividad 7 
 
 ### Actividad 8 

 ### Actividad 9 

 ### Actividad 10 


## Bitácora de aplicación 



## Bitácora de reflexión


