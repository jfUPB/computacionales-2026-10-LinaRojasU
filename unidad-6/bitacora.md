# Unidad 6

## Bitácora de proceso de aprendizaje
### Actividad 1
¿Qué observas en la aplicación al presionar las teclas a, r, s, n?
> a: las particulas se acercan al rededor de donde este posicionado el mouse.
> r: las particulas se caen al "piso" de la aplicación alejandose del mouse.
> s: se detienen las particulas y no se mueven.
> n: se "despausan" las particulas y vuelven a moverse libremente.

¿Qué diferencias notas entre los tipos de partículas?
> Hay tres tipos de particulas
> Rojas: tienen varios tamaños pero son las más pequeñas.
> Verdes: tienen varios tamaños pero son mas grandes que las rojas pero más pequeñas que las azuales.
> Azules: tienen varios tamaños pero so más grandes que las rojas y las verdes.

Formula una hipótesis: ¿Cómo crees que el código organiza la comunicación entre las teclas, las partículas y el cambio de comportamiento?
> Mi hipótetisis es que el sistema está organizado mediante un objeto central (ofApp) que captura las teclas y envía eventos globales a todas las partículas usando un mecanismo de notificación, lo que indica el uso del patrón Observer, ya que las partículas reaccionan automáticamente sin estar acopladas directamente al origen del evento; además, la creación de los distintos tipos de partículas (star, shooting_star, planet) parece delegarse a una estructura que configura sus propiedades iniciales, lo que sugiere el uso de una Factory para evitar crear objetos de forma rígida; finalmente, el cambio de comportamiento de las partículas según la tecla presionada (atraer, repeler, detenerse o movimiento normal) indica que cada partícula cambia internamente su lógica mediante estados intercambiables, lo que corresponde al patrón State, permitiendo modificar su comportamiento sin recurrir a múltiples condicionales dentro de una sola clase.

### Actividad 2
#### Investigación del patrón Observer

1. Coloca un breakpoint dentro de Subject::notify. Cuando se dispare al presionar una tecla, observa en el depurador el vector observers: ¿Cuántos elementos tiene? ¿Qué tipo de objetos son? ¿A qué direcciones de memoria apuntan?
   > Elección del punto de inspección: se colocó un breakpoint dentro del método Subject::notify, específicamente en el bucle for que recorre el vector observers, ya que este punto es clave para observar cómo el sujeto comunica eventos a todos los observadores registrados.

<img width="1552" height="251" alt="image" src="https://github.com/user-attachments/assets/a6ee908c-fc91-46c9-9e85-5e86a6a4fab3" />

   > Explicación: en el depurador se observa que el vector observers contiene múltiples elementos (aproximadamente 115, correspondientes a todas las partículas creadas). Cada elemento es un puntero (Observer*) que apunta a objetos de tipo Particle, y cada uno tiene una dirección de memoria distinta.

   > Justificación: esto demuestra que el sujeto mantiene una colección de referencias a todos los observadores, lo que permite enviar notificaciones a múltiples objetos sin conocer sus detalles internos, evidenciando el desacoplamiento característico del patrón Observer.


2. Ahora coloca un breakpoint en Particle::onNotify. ¿Cuál es la dirección de memoria del objeto this que recibe la llamada? ¿Puedes encontrar esa misma dirección en el vector observers que observaste antes? ¿Qué concluyes sobre cómo el Subject sabe a quién notificar?
   > Elección del punto de inspección: se colocó un breakpoint en el método Particle::onNotify, ya que es el punto donde cada observador recibe la notificación enviada por el sujeto.

<img width="1559" height="361" alt="image" src="https://github.com/user-attachments/assets/c06124ec-6325-41bc-b228-ad57770680db" />

   > Explicación: en el depurador se observa la dirección de memoria del objeto actual (this). Al compararla con las direcciones almacenadas en el vector observers, se puede verificar que coincide con una de ellas.

   > Justificación: esto confirma que el sujeto no crea nuevos objetos ni llama métodos arbitrariamente, sino que utiliza las referencias almacenadas en su lista de observadores para notificar directamente a cada uno, demostrando cómo el patrón Observer gestiona la comunicación mediante referencias existentes.


#### Investigación del patrón State
3. Coloca un breakpoint en Particle::setState. Observa en memoria el puntero state antes y después de la asignación: ¿Qué dirección tenía? ¿Qué dirección tiene ahora? ¿qué le pasó al objeto de estado anterior?
   > Elección del punto de inspección: se colocó un breakpoint en el método Particle::setState, ya que este es el punto donde se realiza el cambio de estado de una partícula.

Antes: 
<img width="1448" height="156" alt="image" src="https://github.com/user-attachments/assets/f0d45c56-cfe7-4cca-915d-b6a78865b48c" />

Despues: 
<img width="1435" height="150" alt="image" src="https://github.com/user-attachments/assets/3968e69e-8433-4660-88e8-9ca81a50ccd9" />

   > Explicación: antes de la asignación, el puntero state apunta a una dirección de memoria correspondiente al estado actual (por ejemplo, NormalState). Después de la asignación, apunta a una nueva dirección (por ejemplo, AttractState). El estado anterior es eliminado mediante delete, liberando la memoria.

   > Justificación: esto demuestra que el objeto cambia dinámicamente su estado interno reemplazando una instancia por otra, lo que permite modificar su comportamiento en tiempo de ejecución sin cambiar su estructura, evidenciando el funcionamiento del patrón State.

   
4. En la unidad anterior estudiaste la _vtable y el despacho dinámico. Ahora conéctalo con el patrón State: coloca breakpoints en NormalState::update y en AttractState::update. Presiona n y luego a. ¿A cuál llega el depurador primero en cada caso? ¿Cómo demuestra esto que el patrón State usa polimorfismo para cambiar el comportamiento en tiempo de ejecución?
   > Elección del punto de inspección: se colocaron breakpoints en los métodos update de NormalState y AttractState para observar cómo cambia el flujo de ejecución según el estado activo.

NormalState: 
<img width="1557" height="358" alt="image" src="https://github.com/user-attachments/assets/87b96f1c-657d-438a-8985-7eaed9d912ca" />

AttractState: 
<img width="1557" height="354" alt="image" src="https://github.com/user-attachments/assets/1cc64e15-a317-4ec3-9420-d6ef3a3be8b2" />

   > Explicación: al presionar la tecla n, el depurador entra en NormalState::update. Luego, al presionar a, el flujo cambia y entra en AttractState::update. Esto ocurre sin modificar la función Particle::update, que simplemente delega la ejecución al estado actual.

   > Justificación: esto evidencia el uso de polimorfismo y despacho dinámico (vtable), ya que el mismo llamado (state->update) ejecuta diferentes implementaciones dependiendo del tipo real del objeto. Esto confirma que el patrón State permite cambiar el comportamiento en tiempo de ejecución mediante polimorfismo.


#### Investigación del patrón Factory
5. Coloca un breakpoint en ParticleFactory::createParticle. Observa el parámetro type y el objeto Particle* que se retorna. Luego, en ofApp::setup, observa el vector particles justo después de las llamadas a la factory. ¿Qué relación tienen las direcciones de los objetos creados con los elementos del vector?
   > Elección del punto de inspección: se colocó un breakpoint en ParticleFactory::createParticle para observar la creación de objetos y otro en ofApp::setup después de agregarlos al vector particles, ya que estos puntos permiten analizar cómo se instancian y almacenan las partículas.

ParticleFactory: 
<img width="1556" height="352" alt="image" src="https://github.com/user-attachments/assets/2111a8bf-45da-4cdf-a86a-d393bb0ec6d6" />

ofApp: 
<img width="1568" height="382" alt="image" src="https://github.com/user-attachments/assets/77d7d36f-2216-4d94-bdeb-cb88eaff0fea" />

   > Explicación: en el método factory se observa el parámetro type (por ejemplo, "star", "planet", etc.) y el puntero Particle* retornado con una dirección de memoria específica. Posteriormente, en ofApp::setup, esas mismas direcciones aparecen almacenadas dentro del vector particles.

   > Justificación: esto demuestra que la factory centraliza la creación de objetos y devuelve instancias configuradas que luego son utilizadas por el sistema principal. El hecho de que las direcciones coincidan confirma que no se crean copias, sino que se gestionan referencias directas, lo que evidencia el uso del patrón Factory para desacoplar la creación de objetos del resto del sistema.
   
### Actividad 3
1. Usando excalidraw, dibuja un diagrama de flujo de mensajes que muestre la cadena completa: keyPressed → notify → onNotify → setState → nueva _vtable activa. Indica en qué punto interviene cada patrón (Observer, State) y dónde la Factory ya cumplió su rol (en el setup).
   > <img width="1536" height="1024" alt="Diagrama de patrones de diseño" src="https://github.com/user-attachments/assets/140e189b-3b58-47a7-af14-1818584f9c17" />


2. En el mismo diagrama, agrega una nota que responda: ¿Qué pasaría si no usaras el patrón Observer y en cambio ofApp::update recorriera todas las partículas y les dijera directamente qué estado tener? ¿Qué cambiaría en el diagrama? ¿Qué problema de diseño crearía eso?
   > Patrón Observer: el patrón Observer es el encargado de gestionar la comunicación entre la entrada del usuario y las partículas. Cuando el usuario presiona una tecla, el método keyPressed en ofApp genera un evento que es enviado a todas las partículas mediante notify. Gracias a este patrón, ofApp no necesita conocer detalles específicos de cada partícula, sino que simplemente notifica a todos los observadores registrados. Cada partícula recibe el evento a través de onNotify, lo que permite una comunicación desacoplada, flexible y escalable. Esto facilita agregar o eliminar partículas sin modificar la lógica de emisión de eventos, manteniendo una arquitectura limpia y modular.
   
   > Patrón State: el patrón State define cómo cambia el comportamiento de cada partícula en función de su estado interno. Cuando una partícula recibe un evento en onNotify, no cambia su lógica mediante condicionales, sino que invoca setState para asignar un nuevo objeto de estado. Este nuevo estado redefine el comportamiento de la partícula, especialmente en el método update, que se ejecuta mediante polimorfismo (vtable). De esta forma, el mismo llamado (state->update) puede producir comportamientos distintos según el estado activo (Normal, Attract, Repel, Stop). Esto permite que el sistema sea extensible y evita estructuras complejas de condicionales, mejorando la mantenibilidad del código.
   
   > Patrón Factory: el patrón Factory interviene en la fase inicial del sistema, específicamente en el método setup de ofApp, donde se crean las partículas. En lugar de instanciar objetos directamente, se utiliza ParticleFactory::createParticle, que encapsula la lógica de creación y configuración de cada tipo de partícula (star, shooting_star, planet). Esto permite centralizar la creación de objetos y facilita la extensión del sistema, ya que nuevos tipos de partículas pueden agregarse sin modificar el código principal. Una vez creadas, las partículas son registradas como observadores, y la Factory ya no interviene en el flujo de ejecución, habiendo cumplido su rol en la arquitectura.

## Bitácora de aplicación 


## Bitácora de reflexión
