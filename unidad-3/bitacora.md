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
<img width="1178" height="723" alt="image" src="https://github.com/user-attachments/assets/b7a65bba-1602-4dc9-a1f0-6ec6dfa5e15e" />

##### Swap Por Puntero:
<img width="1254" height="623" alt="image" src="https://github.com/user-attachments/assets/1bdfbc41-45ff-42e4-843e-5aba9394aefb" />

 ### Actividad 3 

 ### Actividad 4 

 ### Actividad 5 

 ### Actividad 6 

 ### Actividad 7 
 
 ### Actividad 8 

 ### Actividad 9 

 ### Actividad 10 


## Bitácora de aplicación 



## Bitácora de reflexión
