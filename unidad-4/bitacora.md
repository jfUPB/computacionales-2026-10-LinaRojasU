# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 1
```ofApp.h``` se declaran las clases, ```ofApp.cpp``` se definen las clases

 #### Observaciones 
> Al modificar la variable ```interpolationFactor``` entre mas cerca este del 0 más lentos van a llegar los nodos al movimiento del mouse, y entra más cerca del 1 más rapido van a seguir el mouse.
> En el codigo de ```void ofApp::setup()``` Se crea el fondo junto con la serpierte que comienza con 20 nodos.
> En el codigo de ```void ofApp::update()```, Se empieza con ```target``` que empieza en la posición del mouse, el ```interpolationFactor``` controla la velocidad de los nodos hacia el mouse y ```target = pos;``` es que cada nodo sigue el anterior en modo cadena/serpiente.
> En el codigo de ```void ofApp::draw()```, se empieza con ```ofColor``` que coloca dos colores y se pinta el fondo en degradado con esos dos colores, luego cuando entra al ```if``` se crea la linea que une a los nodos colocandole color a la linea y por ultimo crea en cada nodo un circulo colocandole color y tamaño segun en que posicion fue creado, siendo de grande a pequeño.
> En el codigo ```void ofApp::keyPressed(int key)```, Que comienza al apretar "c" lo que significa que vacia todo, osea que elimina la serpiente, al apretar "a"
se agregan nodos a la serpiente, aL apretar "r" puede ir eliminando nodo por nodo y por ultimo "s" que toma captura de la pantalla.

### Actividad 2

 #### Observaciones
> ¿Que es una lista enlazada? = es una estructura de datos donde los elementos no están uno al lado del otro en memoria., en cambio cada elemento guarda un dato y un puntero al siguiente elemento. Cada nodo guarda la dirección del siguiente nodo por lo que esto es lo que permite recorrer la lista.
> En el codigo ```class Node``` contiene un nodo de la lista y cada nodo contiene: posición (x,y) y puntero al siguiente nodo. En ```glm::vec2 position``` contiene un vector 2D y la posición en pantalla. Y cuadno se crea un nodo si esta solo no apunta a nadie y si hay uno siguiente apunta hacia ese hasta que se acaba y el ultimo no apunta a nadie.
> En el codigo ```class LinkedList``` contiene el primer nodo de la lista, el ultimo nodo y guarda todos los nodos que hay en la lista, el constructor lo crea y el destructor elimina todos los nodos.
> En el codigo ```void push_back(glm::vec2 pos)``` agrega un nodo al final y lo guarda en el heap.
> En el codigo ```void pop_back()``` Elimina el ultimo nodo de la lista, si solo hay un nodo se elimina ese, si hay varios elimina el ultimo y la lista queda con el ultimo siendo el punultimo anteriormente.
> En el codigo ```void clear()``` Recorre toda la lista y va eliminando un nodo dentro de un ciclo hasta que no quede ninguno.


## Bitácora de aplicación 

### Actividad 3


## Bitácora de reflexión

### Actividad 4

