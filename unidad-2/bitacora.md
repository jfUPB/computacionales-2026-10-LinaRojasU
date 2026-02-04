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
```

## Bitácora de aplicación 



## Bitácora de reflexión
