# Unidad 6

<details>
<summary> ## Bitácora de proceso de aprendizaje</summary>
   
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

</details>

## Bitácora de aplicación 
### Fase 1

ofApp.h
```
#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
    virtual ~Observer() = default;
    virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
    void addObserver(Observer * observer);
    void removeObserver(Observer * observer);

protected:
    void notify(const std::string & event);

private:
    std::vector<Observer *> observers;
};

class Particle;

class State {
public:
    virtual ~State() = default;
    virtual void update(Particle * particle) = 0;
    virtual void onEnter(Particle * particle) { }
    virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
    Particle();
    ~Particle() override;

    Particle(const Particle &) = delete;
    Particle & operator=(const Particle &) = delete;

    void update();
    void draw();
    void onNotify(const std::string & event) override;

    void setState(State * newState);

    ofVec2f position;
    ofVec2f velocity;
    float size;
    ofColor color;

private:
    void keepInsideWindow();
    State * state;
};

class NormalState : public State {
public:
    void update(Particle * particle) override;
    void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
    void update(Particle * particle) override;
};

class RepelState : public State {
public:
    void update(Particle * particle) override;
};

class StopState : public State {
public:
    void update(Particle * particle) override;
};

class SpiralState : public State {
public:
    void update(Particle * particle) override;
};

class ParticleFactory {
public:
    static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
    ~ofApp() override;
    void setup() override;
    void update() override;
    void draw() override;
    void keyPressed(int key) override;

private:
    std::vector<Particle *> particles;
};
```

ofApp.cpp
```
#include "ofApp.h"
#include <algorithm>

void Subject::addObserver(Observer * observer) {
    if (!observer) return;
    if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
        observers.push_back(observer);
    }
}

void Subject::removeObserver(Observer * observer) {
    if (!observer) return;
    observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string & event) {
    for (Observer * observer : observers) {
        observer->onNotify(event);
    }
}

Particle::Particle() : state(nullptr) {
    position = ofVec2f(ofRandomWidth(), ofRandomHeight());
    velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
    size = ofRandom(2.0f, 5.0f);
    color = ofColor(255);

    state = new NormalState();
    state->onEnter(this);
}

Particle::~Particle() {
    if (state) {
        state->onExit(this);
        delete state;
        state = nullptr;
    }
}

void Particle::setState(State * newState) {
    if (state) {
        state->onExit(this);
        delete state;
    }
    state = newState;
    if (state) {
        state->onEnter(this);
    }
}

void Particle::update() {
    if (state) {
        state->update(this);
    }
    keepInsideWindow();
}

void Particle::draw() {
    ofPushStyle();
    ofSetColor(color);
    ofDrawCircle(position, size);
    ofPopStyle();
}

void Particle::onNotify(const std::string & event) {
    if (event == "attract") setState(new AttractState());
    else if (event == "repel") setState(new RepelState());
    else if (event == "stop") setState(new StopState());
    else if (event == "normal") setState(new NormalState());
    else if (event == "spiral") setState(new SpiralState());
}

void Particle::keepInsideWindow() {
    float W = ofGetWidth();
    float H = ofGetHeight();

    if (position.x < 0 || position.x > W) velocity.x *= -1;
    if (position.y < 0 || position.y > H) velocity.y *= -1;
}

void NormalState::onEnter(Particle * particle) {
    particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}

void NormalState::update(Particle * particle) {
    particle->position += particle->velocity;
}

void AttractState::update(Particle * particle) {
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    ofVec2f dir = mouse - particle->position;
    dir.normalize();
    particle->velocity += dir * 0.05f;
    particle->position += particle->velocity;
}

void RepelState::update(Particle * particle) {
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    ofVec2f dir = particle->position - mouse;
    dir.normalize();
    particle->velocity += dir * 0.05f;
    particle->position += particle->velocity;
}

void StopState::update(Particle * particle) {
    particle->velocity *= 0.9f;
    particle->position += particle->velocity;
}

void SpiralState::update(Particle * particle) {
    float angle = ofGetElapsedTimef();
    particle->velocity.x = cos(angle) * 2.0f;
    particle->velocity.y = sin(angle) * 2.0f;
    particle->position += particle->velocity;
}

Particle * ParticleFactory::createParticle(const std::string & type) {
    Particle * p = new Particle();

    if (type == "comet") {
        p->size = 6.0f;
        p->color = ofColor(255, 255, 0);
        p->velocity *= 2.5f;
    }

    return p;
}

ofApp::~ofApp() {
    for (auto p : particles) { removeObserver(p); delete p; }
}

void ofApp::setup() {
    ofBackground(0);

    for (int i = 0; i < 50; i++) {
        Particle * p = ParticleFactory::createParticle("comet");
        particles.push_back(p);
        addObserver(p);
    }
}

void ofApp::update() {
    for (auto p : particles) p->update();
}

void ofApp::draw() {
    for (auto p : particles) p->draw();
}

void ofApp::keyPressed(int key) {
    if (key == 'p') notify("spiral");
}
```

### Fase 2
#### Evidencia 1: Tu nueva partícula en la Factory
Breakponit: Breakpoint en ```createParticle``` en el ```if (type == "comet")```
<img width="1564" height="528" alt="image" src="https://github.com/user-attachments/assets/024da3f7-1851-4726-945e-a2dc7405cd61" />

Explicación: Se observa que el tipo es "comet" y el objeto tiene: size = 6.0, color amarillo, velocidad aumentada
Justificación: Demuestra que la Factory controla la creación y configuración.

#### Evidencia 2: Tu nuevo estado en la _vtable
Breakponit: Breakpoint en ```SpiralState::update```
<img width="1506" height="490" alt="image" src="https://github.com/user-attachments/assets/b9910628-e5b8-463e-9393-71187feea3f8" />

<img width="1565" height="479" alt="image" src="https://github.com/user-attachments/assets/2824e4bd-4672-44a9-8091-d9a0d0db00c4" />

Explicación: La vtable cambia porque ahora apunta a ```SpiralState::update``` en lugar de ```NormalState::update```
Justificación: Demuestra polimorfismo dinámico → base del patrón State

#### Evidencia 3: La cadena Observer → State completa
Breakponit: Breakpoints en: keyPressed, notify, onNotify, setState
keyPressed; <img width="1567" height="420" alt="image" src="https://github.com/user-attachments/assets/ee87578a-2e75-48c3-a5f2-d966df008ca0" />

notify; <img width="1561" height="500" alt="image" src="https://github.com/user-attachments/assets/e8ea8b92-7d6b-4be0-8984-222f4d99f058" />

onNotify; <img width="1561" height="531" alt="image" src="https://github.com/user-attachments/assets/f9bba69e-6854-448a-b367-d9d6527b8043" />

setState; <img width="1564" height="428" alt="image" src="https://github.com/user-attachments/assets/19dd285c-922e-4905-b347-949f6bb2bece" />
<img width="1464" height="429" alt="image" src="https://github.com/user-attachments/assets/73316e7f-eedd-4aea-ac4f-a01d36a43253" />

Explicación: Evento ```"spiral"``` fluye por toda la cadena y cambia el puntero ```state```
Justificación: Demuestra integración Observer + State

#### Evidencia 4: Decisión de diseño justificada
Breakponit: Crear ```SpiralState``` desde cero (no heredar de otro estado)
<img width="1558" height="641" alt="image" src="https://github.com/user-attachments/assets/0e3bd7ff-9db3-422c-b24d-f1ff7ed2cd1f" />
<img width="1542" height="652" alt="image" src="https://github.com/user-attachments/assets/8b7cbf74-0ea5-419b-b200-13fb294a2e5c" />

Explicación: Comportamiento independiente (usa trigonometría)
Justificación: Evita acoplamiento innecesario y facilita extensión futura

## Bitácora de reflexión
