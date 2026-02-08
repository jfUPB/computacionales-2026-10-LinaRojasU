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



## Bitácora de reflexión

