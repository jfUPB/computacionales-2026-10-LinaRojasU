# Unidad 2

## Bitácora de proceso de aprendizaje

### Actividad 1
```
(start)


@SCREEN
M=1

@END
(END)
0;JMP
```

### Actividad 2
```
(start)


@SCREEN
M=-1

@END
(END)
0;JMP
```

### Actividad 3
```
(start)
// i = SCREEN
@SCREEN
D=A
@i
M=D
//Inicio la pantalla pintando una linea
@SCREEN
M=-1

(LOOP)
@KBD
D=M
@100
D=D-A
@derecha
D;JEQ 

@KBD
D=M
@105
D=D-A
@izquierda
D;JEQ 
@LOOP
0;JMP

(derecha)
@i
A=M
M=0
A=A+1
M=-1
D=A
@i
M=D
@LOOP
0;JMP

(izquierda)
@i
A=M
M=0
A=A-1
M=-1
D=A
@i
M=D
@LOOP
0;JMP

@END
(END)
0;JMP
```

### Actividad 4
```
@sum
M=0        // sum = 0
@i
M=1        // i = 1

(LOOP)
 @i
 D=M       // D = i
 @100
 D=D-A     // D = i - 100
 @END
 D;JGT     // si D > 0  (i > 100) -> saltar a END

 @i
 D=M       // D = i  (preparamos a sumar)
 @sum
 M=M+D     // sum = sum + i

 @i
 M=M+1     // i = i + 1

 @LOOP
 0;JMP     // volver al inicio del bucle

(END)
 @END
 0;JMP     // bucle final (detener)
```

### Actividad 5
 #### Programa 1
```
// int a = 10;
@10
D=A
@a
M=D

// int* p;
// p = &a;
@a
D=A
@p
M=D

// *p = 20;
@20
D=A
@p
A=M
M=D

(END)
@END
0;JMP
```

 #### Programa 2
```
// int a = 10;
@10
D=A
@a
M=D

// int b = 5;
@5
D=A
@b
M=D

// int *p;
 // p = &a;
@a
D=A
@p
M=D

// b = *p;
@p
A=M
D=M
@b
M=D

(END)
@END
0;JMP
```

### Actividad 6
```
// ---------- Inicializar arreglo en RAM[16..25] ----------
@1
D=A
@16
M=D

@20
D=A
@17
M=D

@13
D=A
@18
M=D

@24
D=A
@19
M=D

@55
D=A
@20
M=D

@96
D=A
@21
M=D

@87
D=A
@22
M=D

@83
D=A
@23
M=D

@98
D=A
@24
M=D

@102
D=A
@25
M=D

// ---------- Variables ----------
@26
M=0        // sum = 0

@16
D=A
@27
M=D        // p = 16 (puntero al inicio del arreglo)

@26
D=A
@28
M=D        // end = 26 (dirección después del último elemento: 16+10=26)

// ---------- Loop: while (p < end) { sum += *p; p = p + 1; } ----------
(LOOP)
  @27
  D=M        // D = p

  @28
  D=D-A      // D = p - end
  @END
  D;JGE      // si p >= end -> saltar a END

  @27
  A=M        // A = p (señala la celda actual del arreglo)
  D=M        // D = RAM[p] (valor actual del arreglo)

  @26
  M=M+D      // sum = sum + D

  @27
  M=M+1      // p = p + 1

  @LOOP
  0;JMP

(END)
  @END
  0;JMP
```

### Actividad 7
```
(start)

//int result = 0;

@result
M=0

/*
int main()
{
  result = sum(3, 4);
  std::cout << "The sum: " << result << std::endl;
}
*/

// Load sum arguments
@3
D=A
@R0
M=D
@4
D=A
@R1
M=D

// Save return address
@returnFromSum
D=A
@R15
M=D

// call sum
@sum
0;JMP

// return after sum
// and store result
(returnFromSum)
@R0
D=M
@result
M=D

@fin
(fin)
0;JMP

/*
int sum(int a, int b)
{
    return a + b;
}
*/

(sum)
@R0
D=M
@R1
D=D+M
@R0
M=D
@R15
A=M
0;JMP
```

## Bitácora de aplicación 


 #### Actividad 8
 
 > ##### Problema 1:
```
#include <iostream>

void swap(int* pa, int* pb){
    int tmp = *pa;
    *pa = *pb;
    *pb = tmp;
}

int main()
{
    int a = 10;
    int b = 20;
    std::cout<<"a: " << a <<" b: "<< b<< std::endl;
    swap(&a,&b);
    std::cout<<"a: " << a <<" b: "<< b<< std::endl;
    return 0;
}
```

 > ##### Lenguaje ensamblador
```
// ----------------- Datos (variables) -----------------
// Reservamos 'a' y 'b' en memoria (el ensamblador asignará direcciones
// a partir de 16; aquí usaremos las direcciones 16 y 17 conceptualmente).
// Para claridad uso las etiquetas simbólicas: a, b, etc.

@10
D=A
@a
M=D        // a = 10

@20
D=A
@b
M=D        // b = 20

// ----------------- MAIN: preparar llamada a swap(&a, &b) -----------------

// poner en R0 la dirección de a (por convención los argumentos van en R0, R1,...)
@a
D=A
@R0
M=D        // R0 = &a

// poner en R1 la dirección de b
@b
D=A
@R1
M=D        // R1 = &b

// guardar la dirección de retorno en R15 (direccion label RETURN_FROM_SWAP)
@RETURN_FROM_SWAP
D=A
@R15
M=D        // R15 = address(RETURN_FROM_SWAP)

// saltar a la función swap
@SWAP
0;JMP

// cuando la función termine, volveremos aquí (dirección puesta en R15)
(RETURN_FROM_SWAP)

// --- Aquí estaría la segunda std::cout en C++ (omitida) ---
// Podemos leer a y b en la memoria para ver que se intercambiaron.

// fin del programa: bucle infinito
(END)
  @END
  0;JMP

// ----------------- Función swap (usa los registros R0=pa, R1=pb) -----------------
(SWAP)
  // tmp = *pa
  @R0
  A=M      // A = R0 (la dirección almacenada en R0)
  D=M      // D = *pa
  @R13
  M=D      // R13 = tmp

  // *pa = *pb
  @R1
  A=M      // A = R1 (dirección apuntada por pb)
  D=M      // D = *pb
  @R0
  A=M      // A = pa (direccion)
  M=D      // *pa = *pb

  // *pb = tmp
  @R13
  D=M      // D = tmp
  @R1
  A=M      // A = pb (direccion)
  M=D      // *pb = tmp

  // return: saltar a la dirección guardada en R15
  @R15
  A=M
  0;JMP
```
<img width="420" height="817" alt="image" src="https://github.com/user-attachments/assets/a6dcb725-cde2-4ae4-8a12-a15de0fc4f4b" /><br/> 
<img width="974" height="751" alt="image" src="https://github.com/user-attachments/assets/23a4df07-03f8-4632-a6f1-a33951c1621d" />


 > ##### Problema 2:
```
#include <iostream>

int calSum(int* parr,int arrSize){
    int sum = 0;
    for(int i= 0; i < arrSize;i++){
        sum = sum + *(parr+i);
    }
    return sum;
}

int main()
{
    int arr[] = {10,15,2,3,50};
    int sum = calSum(arr,5);
    std::cout<<"Sum: " << sum << std::endl;
    return 0;
}
```

 > ##### Lenguaje ensamblador
```
// =====================
// Inicializar arreglo arr = {10,15,2,3,50}
// arr empieza en RAM[16]
// =====================
@10
D=A
@16
M=D

@15
D=A
@17
M=D

@2
D=A
@18
M=D

@3
D=A
@19
M=D

@50
D=A
@20
M=D

// =====================
// MAIN: llamar calSum(arr, 5)
// =====================

// R0 = &arr
@16
D=A
@R0
M=D

// R1 = arrSize = 5
@5
D=A
@R1
M=D

// Guardar dirección de retorno
@RETURN
D=A
@R15
M=D

// Llamar función
@CALSUM
0;JMP

(RETURN)
// Aquí R0 tiene la suma final

(END)
@END
0;JMP

// =====================
// FUNCIÓN calSum
// R0 = parr
// R1 = arrSize
// =====================
(CALSUM)

// sum = 0
@0
D=A
@R13
M=D

// i = 0
@0
D=A
@R14
M=D

(LOOP)
// if (i == arrSize) salir
@R14
D=M
@R1
D=D-M
@FIN
D;JEQ

// sum = sum + *(parr + i)
@R0
D=M
@R14
A=D+M
D=M
@R13
M=D+M

// i++
@R14
M=M+1

@LOOP
0;JMP

(FIN)
// return sum
@R13
D=M
@R0
M=D

// regresar a main
@R15
A=M
0;JMP
```

<img width="427" height="822" alt="image" src="https://github.com/user-attachments/assets/e9a02ecb-5b6f-45c7-ad57-0a0438f6aa16" /><br/>
<img width="972" height="824" alt="image" src="https://github.com/user-attachments/assets/677f9faf-f3fa-41cf-917c-f400ae66482c" />


## Bitácora de reflexión




