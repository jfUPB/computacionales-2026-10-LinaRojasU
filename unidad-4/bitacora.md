# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 1
```ofApp.h``` se declaran las clases, ```ofApp.cpp``` se definen las clases

 #### Observaciones 
> - Al modificar la variable ```interpolationFactor``` entre mas cerca este del 0 más lentos van a llegar los nodos al movimiento del mouse, y entra más cerca del 1 más rapido van a seguir el mouse.
> - En el codigo de ```void ofApp::setup()``` Se crea el fondo junto con la serpierte que comienza con 20 nodos.
> - En el codigo de ```void ofApp::update()```, Se empieza con ```target``` que empieza en la posición del mouse, el ```interpolationFactor``` controla la velocidad de los nodos hacia el mouse y ```target = pos;``` es que cada nodo sigue el anterior en modo cadena/serpiente.
> - En el codigo de ```void ofApp::draw()```, se empieza con ```ofColor``` que coloca dos colores y se pinta el fondo en degradado con esos dos colores, luego cuando entra al ```if``` se crea la linea que une a los nodos colocandole color a la linea y por ultimo crea en cada nodo un circulo colocandole color y tamaño segun en que posicion fue creado, siendo de grande a pequeño.
> - En el codigo ```void ofApp::keyPressed(int key)```, Que comienza al apretar "c" lo que significa que vacia todo, osea que elimina la serpiente, al apretar "a"
se agregan nodos a la serpiente, aL apretar "r" puede ir eliminando nodo por nodo y por ultimo "s" que toma captura de la pantalla.

### Actividad 2

 #### Observaciones
> - ¿Que es una lista enlazada? = es una estructura de datos donde los elementos no están uno al lado del otro en memoria., en cambio cada elemento guarda un dato y un puntero al siguiente elemento. Cada nodo guarda la dirección del siguiente nodo por lo que esto es lo que permite recorrer la lista.
> - En el codigo ```class Node``` contiene un nodo de la lista y cada nodo contiene: posición (x,y) y puntero al siguiente nodo. En ```glm::vec2 position``` contiene un vector 2D y la posición en pantalla. Y cuadno se crea un nodo si esta solo no apunta a nadie y si hay uno siguiente apunta hacia ese hasta que se acaba y el ultimo no apunta a nadie.
> - En el codigo ```class LinkedList``` contiene el primer nodo de la lista, el ultimo nodo y guarda todos los nodos que hay en la lista, el constructor lo crea y el destructor elimina todos los nodos.
> - En el codigo ```void push_back(glm::vec2 pos)``` agrega un nodo al final y lo guarda en el heap.
> - En el codigo ```void pop_back()``` Elimina el ultimo nodo de la lista, si solo hay un nodo se elimina ese, si hay varios elimina el ultimo y la lista queda con el ultimo siendo el punultimo anteriormente.
> - En el codigo ```void clear()``` Recorre toda la lista y va eliminando un nodo dentro de un ciclo hasta que no quede ninguno.
> - En el codigo ```LinkedList snake;``` Se crea una lista enlazada que termina siento la serpiente y cada nodo representa una parte de la serpiente.
> - En el codigo ```void ofApp::setup()``` Se crean los 20 nodos y todos comienzan en el centro.

## Bitácora de aplicación 

### Actividad 3

 #### Evidencia 1: inserción del primer nodo en una cola vacía (enqueue)
 <img width="1902" height="883" alt="Captura de pantalla 2026-03-13 032410" src="https://github.com/user-attachments/assets/b71f9204-7c81-4889-ad0f-2f86d7276be9" />
 #### Explicación: En la captura se observa que la cola estaba vacía y se insertó el primer nodo. Las variables front y rear apuntan a la misma dirección de memoria, lo que indica que el primer nodo es simultáneamente el inicio y el final de la cola. Además despues (aunque no se ve en la captura), el tamaño (size) se incrementa a 1.
 #### Justificación: Esto demuestra que la estructura maneja correctamente la inserción inicial en una cola vacía, estableciendo adecuadamente los punteros front y rear.
 
 #### Evidencia 2: mantenimiento del orden FIFO al insertar más nodos (enqueue)
<img width="1913" height="853" alt="image" src="https://github.com/user-attachments/assets/40a311dd-8dc3-4846-b289-1e259480f4a2" />
  #### Explicación: En la imagen se observa que el puntero rear->next apunta al nuevo nodo y posteriormente rear se va a actualiza para señalar el último nodo insertado.
  #### Justificación: Esto demuestra que la cola mantiene el orden FIFO, ya que los nuevos elementos siempre se agregan al final sin alterar los nodos anteriores.

 #### Evidencia 3: comportamiento de eliminación y prevención de fugas (dequeue)
 <img width="1901" height="855" alt="image" src="https://github.com/user-attachments/assets/6a1829cb-9915-4a89-bb9d-91141007dec3" />
  #### Explicación: En la captura se observa que el nodo apuntado por front se guarda temporalmente en temp, luego front se actualiza para apuntar al siguiente nodo de la cola.
  #### Justificación: En la captura se observa que el nodo apuntado por front se guarda temporalmente en temp, luego front se actualiza para apuntar al siguiente nodo de la cola.

 #### Evidencia 4: control del tamaño máximo de la cola (maxSize)
 <img width="1914" height="861" alt="image" src="https://github.com/user-attachments/assets/3920099b-8623-4d90-a684-de5b96dd167d" />
  #### Explicación: cuando el tamaño de la cola supera el límite máximo, el programa ejecuta la función dequeue() para eliminar el nodo más antiguo.
  #### Justificación: Esto garantiza que la cola nunca supere el tamaño definido, manteniendo un número controlado de trazos en pantalla.

 #### Evidencia 5: recorrido de la cola sin destruirla (draw)
 <img width="1912" height="909" alt="image" src="https://github.com/user-attachments/assets/eaf1b36a-afdd-4073-ba12-471cd4ec952d" />
  #### Explicación: El puntero current se utiliza para recorrer los nodos de la cola desde front hasta nullptr, permitiendo dibujar cada trazo en pantalla.
  #### Justificación: Esto demuestra que el recorrido de la cola se realiza sin modificar la estructura de datos original.

 #### Evidencia 6: limpieza total de la memoria (clear)
 <img width="1919" height="856" alt="image" src="https://github.com/user-attachments/assets/64af4337-9cb5-448a-9d7d-2adb7682b772" />
  #### Explicación: En la captura se observa que todos los nodos han sido eliminados mediante llamadas repetidas a dequeue().
  #### Justificación: Esto confirma que la función clear() elimina correctamente todos los nodos y restablece el estado de la cola.

## Bitácora de reflexión

### Actividad 4




