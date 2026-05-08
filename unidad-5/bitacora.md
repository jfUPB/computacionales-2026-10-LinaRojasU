# Unidad 5
## Bitácora de proceso de aprendizaje
### Actividad 1

#### Parte 1
¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.
> El encapsulamiento es ocultar los datos internos de una clase y permitir que se acceda a ellos de forma controlada.

Ejemplo.
> Si tengo una clase CuentaBancaria, no sería buena idea que cualquiera pudiera cambiar el saldo directamente.

¿Por qué es útil?
> Porque evita errores, protege la información y hace que el programa sea más ordenado.


¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.
> La herencia es cuando una clase nueva toma características de otra clase.

Ejemplo.
> Si tengo una clase Vehiculo, puedo crear Carro y Moto como clases que heredan de Vehiculo, así no se tiene que repetir cosas como velocidad, color o moverse() en cada clase.

¿Por qué deberia usarse?
> Porque permite reutilizar código y organizar mejor el programa.


¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.
> El polimorfismo significa que una misma instrucción puede comportarse de forma distinta según el objeto real.

Ejemplo.
> Si tengo una lista de figuras y todas tienen el método Dibujar(), entonces puedo llamar Dibujar() a todas, pero cada figura dibuja algo distinto.

¿Qué significa que un código sea polimórfico?
> Que trabaja con un tipo general, pero al ejecutarse usa el comportamiento específico del objeto.


#### Parte 2
Encapsulamiento:
Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.

<img width="255" height="39" alt="image" src="https://github.com/user-attachments/assets/78aa86b6-2d3e-400a-be12-3174b2f9230b" />

> Esto es encapsulamiento porque el campo nombre no se puede cambiar directamente desde fuera de la clase.

¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?
> Porque así se controla mejor el acceso; nombre queda protegido, Nombre sirve como puerta de acceso controlada.

¿Qué problema se evita?
> Se evita que cualquier parte del programa cambie el nombre de forma incorrecta.


Herencia:
¿Cómo se evidencia la herencia en la clase Circulo?

<img width="333" height="31" alt="image" src="https://github.com/user-attachments/assets/dac033aa-13e6-4a32-9e40-6a6e40436db0" />

> Eso significa que Circulo hereda de Figura.

Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?
> También almacena lo que viene de Figura, como nombre.


Polimorfismo:
Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta; solo quiero que intentes razonar cómo podría ser.

> <img width="377" height="139" alt="image" src="https://github.com/user-attachments/assets/c764e4c8-0e2c-4ba5-8ff3-928433b3923d" />

> Aunque fig es de tipo Figura, en realidad puede contener un Circulo o un Rectangulo. Entonces, cuando se llama a fig.Dibujar(), el programa ejecuta el método correcto según el objeto real.

Mi hipótesis sería esta:

> El programa guarda qué tipo real tiene cada objeto, cuando llega la llamada Dibujar(), revisa ese tipo, luego ejecuta la versión correspondiente: si es Circulo, llama a Circulo.Dibujar() o si es Rectangulo, llama a Rectangulo.Dibujar().


#### Parte 3
Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?
> Cuando se crea un Rectangulo, ese objeto tiene todo junto: el nombre que viene de Figura, la base, la altura

¿Cómo lo imagino en memoria?
> Yo me lo imagino como un bloque único de memoria que contiene primero la parte heredada y luego la parte propia de la clase hija.


El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.
> Mi hipótesis es que cada objeto guarda una especie de referencia interna que le dice al programa qué versión del método debe ejecutar. Entonces, aunque la variable sea de tipo Figura, en tiempo de ejecución el programa revisa el objeto real y llama al método correcto, eso explicaría por qué Dibujar() cambia según el tipo del objeto.


La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?
> Yo creo que esto se revisa cuando se escribe y compila el código, no cuando el programa ya está corriendo. O sea: si intentas usar un miembro private desde afuera, el compilador te marca error, y no te deja ejecutar el programa.
> Y piesno esto ya que el problema es de reglas del lenguaje, no de comportamiento en pantalla.


### Actividad 2
Idea general de la aplicación.
> Este programa simula fuegos artificiales.
> Funciona así: cuando se hace clic en el mouse, aparece una partícula que sube desde abajo. Esa partícula va perdiendo estabilidad hasta que explota. Cuando explota, aparecen varias partículas nuevas con formas distintas: círculo, cuadrado, estrella.
> Todas las partículas se van actualizando y dibujando en pantalla y cuando una partícula termina su tiempo de vida, se elimina de memoria.


### Actividad 3
¿Cómo se ve un objeto en la memoria?
> En C++, un objeto no es solo “algo con métodos”.
> En memoria, un objeto es un bloque que contiene: sus datos miembros, y, si la clase tiene métodos virtuales, un dato oculto que permite el polimorfismo.
> Ese dato oculto es el que termina apuntando a la vtable.


Antes de ejecutar el experimento: ¿Qué esperas ver en memoria (hipótesis)? Ejecuta el código, abre el depurador y captura el objeto ofApp en memoria. ¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?
> Yo esperaría ver que el objeto ofApp está guardado como un bloque de memoria que contiene: un puntero oculto a la vtable, el miembro particles, y cualquier otro dato de la clase.
> Como ofApp hereda de ofBaseApp, y ofBaseApp tiene métodos virtuales, es normal que el objeto tenga ese puntero oculto al inicio.

Usa de nuevo el depurador para capturar un objeto de tipo CircularExplosion. Es posible que debas hacer modificaciones mínimas en el código para poder capturarlo más fácilmente. Abre las ventanas Auto o Locals y Memory 1 en el depurador. Trata de encontrar en memoria todas las partes que componen al objeto CircularExplosion. Recuerda tener a mano toda la jerarquía de clases para identificar cada parte en memoria. ¿Qué puedes observar? ¿Qué puedes concluir?
> El breakpoint va dentro de setup() o update(), porque ahí el objeto ya existe y está corriendo.
> Dentro de una función miembro, se puede ver this.
> En el depurado r se observa: this, particles, en Memory 1 la dirección de this.

¿Que se observa?
> Si se abre Memory 1 con la dirección de this, verás que al inicio aparece algo que no son tus variables visibles directamente: ese es el puntero oculto a la vtable.

Conclusión.
> Que el objeto ofApp vive mientras la aplicación está corriendo, y que su memoria contiene tanto datos visibles como información interna para soportar los métodos virtuales.


### Actividad 4
#### Programa 1
Ejecuta este código. Luego, descomenta las líneas comentadas y vuelve a compilar. ¿Qué sucede? ¿Por qué? ¿Qué puedes concluir?
> Sin descomentar las lineas se ejecuta bien porque solo estás accediendo a publicVar, que es público.
> Y descomentadno las lineas el compilador da error, porque privateVar solo se puede usar dentro de la clase AccessControl y protectedVar solo se puede usar dentro de la clase o en clases que hereden de ella
Desde main, que está fuera de la clase, no se tiene permiso para tocarlos.

#### Programa 2
Compila el programa. ¿Qué pasa?
> Da error, porque secret1 es private y no se puede acceder desde main. Ya que aunque el objeto sí existe en memoria, el lenguaje no te deja usar ese campo directamente fuera de la clase.

#### Prgrama 3
Compila y ejecuta. ¿Qué puedes concluir?
> Sí, normalmente compila, pero en muchos casos puede imprimir algo como: 42, 3.14, A

En tus palabras, ¿qué es el encapsulamiento? ¿Por qué es importante? ¿Es una protección en tiempo de compilación o en tiempo de ejecución?
> El encapsulamiento es esconder los detalles internos de una clase, permitir acceso solo por medios controlados.

¿Por qué es importante?
> Porque evita errores accidentales, protege el estado interno del objeto, hace el código más fácil de mantener y permite cambiar la implementación interna sin romper el resto del programa.

¿Es protección en tiempo de compilación o en tiempo de ejecución?
> Principalmente es una protección de tiempo de compilación. Porque el compilador revisa si estás intentando acceder a algo privado o protegido, si lo haces mal, te da error antes de ejecutar el programa.

¿Y en tiempo de ejecución?
> En tiempo de ejecución la memoria sigue existiendo, claro. Pero el lenguaje ya no te está protegiendo si tú decides hacer trucos como reinterpret_cast.

### Actividad 5 

## Bitácora de aplicación 

ofApp.h 
```
#pragma once
#include "ofMain.h"
#include <vector>

// -------------------------------------------------
// Clase base abstracta: Particle
// -------------------------------------------------
class Particle {
public:
	virtual ~Particle() { }
	virtual void update(float dt) = 0;
	virtual void draw() = 0;
	virtual bool isDead() const = 0;
	virtual bool shouldExplode() const { return false; }
	virtual glm::vec2 getPosition() const { return glm::vec2(0, 0); }
	virtual ofColor getColor() const { return ofColor(255); }
};

// -------------------------------------------------
// RisingParticle: Partícula que nace en la parte inferior y sube
// -------------------------------------------------
class RisingParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float lifetime;
	float age;
	bool exploded;

public:
	RisingParticle(const glm::vec2 & pos, const glm::vec2 & vel,
		const ofColor & col, float life)
		: position(pos)
		, velocity(vel)
		, color(col)
		, lifetime(life)
		, age(0)
		, exploded(false) { }

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		velocity.y += 9.8f * dt * 8;
		float explosionThreshold = ofGetHeight() * 0.15f + ofRandom(-30, 30);
		if (position.y <= explosionThreshold || age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 10);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

class ZigZagParticle : public Particle {
	glm::vec2 position;
	glm::vec2 velocity;
	float time;
	ofColor color;

public:
	ZigZagParticle(glm::vec2 pos)
		: position(pos)
		, time(0) {
		velocity = glm::vec2(0, -150);
		color.setHsb(ofRandom(255), 200, 255);
	}

	void update(float dt) override {
		time += dt;
		position.y += velocity.y * dt;
		position.x += sin(time * 10) * 50 * dt; // zigzag
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 5);
	}

	bool isDead() const override {
		return position.y < 0;
	}
};

class HeartParticle : public Particle {
private:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float age;
	float lifetime;

public:
	HeartParticle(const glm::vec2 & pos)
		: position(pos)
		, age(0)
		, lifetime(2.0f) {

		velocity = glm::vec2(ofRandom(-100, 100), ofRandom(-200, -50));
		color.setHsb(ofRandom(255), 200, 255);
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;

		// gravedad
		velocity.y += 200 * dt;

		// desvanecimiento
		color.a = ofMap(age, 0, lifetime, 255, 0, true);
	}

	void draw() override {
		ofPushMatrix();
		ofTranslate(position);

		float scale = 0.3f;
		ofScale(scale, scale);

		ofSetColor(color);

		ofPath heart;
		heart.setFilled(true);
		heart.setFillColor(color);

		heart.moveTo(0, -30);
		heart.bezierTo(-35, -60, -80, -10, 0, 35);
		heart.bezierTo(80, -10, 35, -60, 0, -30);
		heart.close();

		heart.draw();

		ofPopMatrix();
	}

	bool isDead() const override {
		return age >= lifetime;
	}
};

// -------------------------------------------------
// Clase base para explosiones: ExplosionParticle
// -------------------------------------------------
class ExplosionParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float age;
	float lifetime;
	float size;

public:
	ExplosionParticle(const glm::vec2 & pos, const glm::vec2 & vel,
		const ofColor & col, float life, float sz)
		: position(pos)
		, velocity(vel)
		, color(col)
		, age(0)
		, lifetime(life)
		, size(sz) { }

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		float alpha = ofMap(age, 0, lifetime, 255, 0, true);
		color.a = alpha;
	}

	bool isDead() const override { return age >= lifetime; }
};

// -------------------------------------------------
// CircularExplosion: Explosión en patrón circular
// -------------------------------------------------
class CircularExplosion : public ExplosionParticle {
public:
	CircularExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(80, 200);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, size);
	}
};

// -------------------------------------------------
// RandomExplosion: Explosión con direcciones aleatorias
// -------------------------------------------------
class RandomExplosion : public ExplosionParticle {
public:
	RandomExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(16, 32)) {
		velocity = glm::vec2(ofRandom(-200, 200), ofRandom(-200, 200));
	}

	void draw() override {
		ofSetColor(color);
		ofDrawRectangle(position.x, position.y, size, size);
	}
};

// -------------------------------------------------
// StarExplosion: Explosión en forma de estrella
// -------------------------------------------------
class StarExplosion : public ExplosionParticle {
public:
	StarExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.3f, ofRandom(20, 40)) {
		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(90, 180);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void draw() override {
		ofSetColor(color);
		int rays = 5;
		float outerRadius = size;
		float innerRadius = size * 0.5f;
		ofPushMatrix();
		ofTranslate(position);
		for (int i = 0; i < rays; i++) {
			float theta = ofMap(i, 0, rays, 0, TWO_PI);
			float xOuter = cos(theta) * outerRadius;
			float yOuter = sin(theta) * outerRadius;
			float xInner = cos(theta + PI / rays) * innerRadius;
			float yInner = sin(theta + PI / rays) * innerRadius;
			ofDrawLine(0, 0, xOuter, yOuter);
			ofDrawLine(xOuter, yOuter, xInner, yInner);
		}
		ofPopMatrix();
	}
};

class SpiralExplosion : public ExplosionParticle {
public:
	SpiralExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, 10) {

		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(50, 150);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void update(float dt) override {
		ExplosionParticle::update(dt);
		// movimiento en espiral
		velocity = glm::rotate(velocity, 0.05f);
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, size);
	}
};

// -------------------------------------------------
// ofApp: Manejo de la escena y eventos
// -------------------------------------------------
class ofApp : public ofBaseApp {
public:
	void setup();
	void update();
	void draw();
	void mousePressed(int x, int y, int button);
	void keyPressed(int key);

	std::vector<Particle *> particles;
	~ofApp();

private:
	void createRisingParticle();
};
```

ofApp.cpp
```
#include "ofApp.h"

// --------------------------------------------------------------
void ofApp::setup() {
	ofSetFrameRate(60);
	ofBackground(0);
}

// --------------------------------------------------------------
void ofApp::update() {
	float dt = ofGetLastFrameTime();

	for (int i = 0; i < particles.size(); i++) {
		particles[i]->update(dt);
	}

	for (int i = particles.size() - 1; i >= 0; i--) {
		if (particles[i]->shouldExplode()) {
			int explosionType = (int)ofRandom(4);
			int numParticles = (int)ofRandom(20, 30);
			for (int j = 0; j < numParticles; j++) {
				if (explosionType == 0) {
					particles.push_back(new CircularExplosion(
						particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 1) {
					particles.push_back(new RandomExplosion(
						particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 2) {
					particles.push_back(new StarExplosion(
						particles[i]->getPosition(), particles[i]->getColor()));
				} else {
					particles.push_back(new SpiralExplosion(
						particles[i]->getPosition(),
						particles[i]->getColor()));
				}
			}
			delete particles[i];
			particles.erase(particles.begin() + i);
		} else if (particles[i]->isDead()) {
			delete particles[i];
			particles.erase(particles.begin() + i);
		}
	}
}

// --------------------------------------------------------------
void ofApp::draw() {
	for (int i = 0; i < particles.size(); i++) {
		particles[i]->draw();
	}
}

// --------------------------------------------------------------
void ofApp::createRisingParticle() {
	float minX = ofGetWidth() * 0.35f;
	float maxX = ofGetWidth() * 0.65f;
	float spawnX = ofRandom(minX, maxX);
	glm::vec2 pos(spawnX, ofGetHeight());
	glm::vec2 target(ofGetWidth() / 2.0f + ofRandom(-300, 300),
		ofGetHeight() * 0.10f + ofRandom(-30, 30));
	glm::vec2 direction = glm::normalize(target - pos);
	glm::vec2 vel = direction * ofRandom(250, 350);
	ofColor col;
	col.setHsb(ofRandom(255), 220, 255);
	float lifetime = ofRandom(1.5f, 3.5f);
	particles.push_back(new RisingParticle(pos, vel, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
	createRisingParticle();
}

// --------------------------------------------------------------
void ofApp::keyPressed(int key) {
	if (key == ' ') {
		for (int i = 0; i < 1000; i++) {
			createRisingParticle();
		}
	}
	if (key == 's') {
		ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
	}
}

// --------------------------------------------------------------
ofApp::~ofApp() {
	for (int i = 0; i < particles.size(); i++) {
		delete particles[i];
	}
	particles.clear();
}
```

- Evidencia 1 — Herencia en memoria
Elección del punto de inspección: ```particles[i]->update(dt);```
¿Por qué aquí?: Porque en ese momento ya existe un objeto real (ej: HeartParticle) dentro del vector y está siendo tratado como Particle*. Es el mejor punto para ver cómo está construido en memoria con herencia.

<img width="1564" height="958" alt="image" src="https://github.com/user-attachments/assets/ae167be9-6ce3-4cc0-9875-4ec6c674c1cf" />

Explicación: En el depurador se observa que SpiralExplosion contiene la parte heredada de ExplosionParticle y la de Particle dentro de una sola instancia. La herencia no crea objetos separados, sino un solo objeto con una organización interna por niveles.

Justificación: Esto muestra que la herencia se implementa dentro de una misma región de memoria, donde la clase derivada incorpora la información de sus clases base.

- Evidencia 2 — La _vtable de tu nuevo tipo
Elección del punto de inspección:  ```particles[i]->update(dt);```
¿Por qué aquí?: Porque en este punto el objeto ya está completamente construido y listo para ejecutar métodos virtuales. Esto permite inspeccionar su _vptr, que apunta a la _vtable, y analizar cómo el sistema decide qué función ejecutar en tiempo de ejecución.

SpiralExplosion:
<img width="1564" height="958" alt="image" src="https://github.com/user-attachments/assets/ae167be9-6ce3-4cc0-9875-4ec6c674c1cf" />

CircularExplosion:
<img width="1861" height="860" alt="image" src="https://github.com/user-attachments/assets/4ed80eb9-8b58-459e-9c64-8662daa20fdf" />

Explicación: Al comparar la vtable de SpiralExplosion con la de CircularExplosion, se observa que la estructura de la tabla es la misma, pero algunas direcciones cambian. Eso ocurre porque cada clase derivada puede sobrescribir métodos virtuales con su propia implementación.

Justificación: Esto muestra que el polimorfismo en C++ se apoya en la vtable: la tabla conserva el orden de los métodos virtuales, pero cada clase apunta a sus propias funciones cuando las modifica.

- Evidencia 3 — Polimorfismo en tiempo de ejecución
Elección del punto de inspección: ```particles[i]->draw();```
¿Por qué aquí?: Porque esta es la línea donde ocurre directamente el polimorfismo. Aunque el tipo del puntero es Particle*, aquí el programa decide en tiempo de ejecución qué método draw() ejecutar dependiendo del tipo real del objeto.

<img width="1549" height="736" alt="image" src="https://github.com/user-attachments/assets/c0fa1be6-0f9a-470e-b289-ce77e5913827" />

Explicación: Aunque la variable es de tipo Particle*, el programa ejecuta la versión del método correspondiente al tipo real del objeto. Al hacer Step Into desde particles[i]->update(dt), el depurador entra en el método de la clase derivada correcta.

Justificación: Esto demuestra despacho dinámico: la llamada se resuelve en tiempo de ejecución usando el tipo real del objeto y no solo el tipo del puntero.

- Evidencia 4 — Encapsulamiento en el contexto de herencia
Elección del punto de inspección: ```void update(float dt)```
¿Por qué aquí?: Porque dentro de este método se tiene acceso directo a los atributos privados del objeto mediante this. Es el lugar ideal para ver qué datos están disponibles dentro de la clase y entender cómo el encapsulamiento limita el acceso desde fuera.

<img width="1536" height="746" alt="image" src="https://github.com/user-attachments/assets/e04ed584-5012-4aa9-a333-4f33450b23f6" />

Explicación: En la jerarquía de herencia, los campos protected de la clase base son visibles y utilizables desde la subclase, mientras que los private no pueden ser accedidos directamente desde fuera de su propia clase. En el depurador, esto se refleja en la forma en que se agrupan los miembros del objeto y en qué campos puede usar el código según su contexto.

Justificación: Esto demuestra que el encapsulamiento sigue siendo una regla de acceso del lenguaje, incluso dentro de una jerarquía de herencia.

Evidencias para RAE 2 — Pruebas y depuración
- Evidencia 5 — Ciclo de vida completo de tu partícula
Elección del punto de inspección: ```particles.push_back(new RisingParticle(...));  particles[i]->update(dt);  delete particles[i];```
¿Por que aqui?: Porque aquí se crea el objeto y entra al sistema, Porque aquí el objeto está en uso y cambiando su estado, Porque aquí se libera la memoria del objeto.

Creación:
<img width="1557" height="826" alt="image" src="https://github.com/user-attachments/assets/0a0f99a5-996d-4c96-a3f0-744094c4ffa3" />

Vida:
<img width="1558" height="810" alt="image" src="https://github.com/user-attachments/assets/0df81314-9c4c-4268-83a1-614b23e79383" />

Muerte:
<img width="1564" height="789" alt="image" src="https://github.com/user-attachments/assets/87e2a70b-6a7b-410d-820c-423d18ca82c2" />

Explicación: La partícula se crea y entra al vector como un puntero dinámico, luego se actualiza mientras vive y finalmente se elimina cuando isDead() indica que terminó su tiempo de vida. El depurador permite ver claramente cada etapa del ciclo.

Justificación: Esto demuestra el ciclo completo de vida del objeto: creación, uso y destrucción.

- Evidencia 6 — Sin fugas de memoria
Elección del punto de inspección: ```delete particles[i];
particles.erase(particles.begin() + i);```
¿Por que aqui?: Porque estas dos líneas son críticas: una libera la memoria (delete) y la otra elimina el puntero del contenedor (erase). Es el punto clave donde se evita una fuga de memoria

Antes: 
<img width="1546" height="726" alt="image" src="https://github.com/user-attachments/assets/24fb5ce5-31f3-4b8a-a345-82d90379f190" />

Despues: 
<img width="1552" height="709" alt="image" src="https://github.com/user-attachments/assets/da2c896a-4c6e-4fd1-9f3f-dea6207b2533" />

Explicación: La memoria se libera con delete y la referencia se retira del vector con erase. Después de esa operación, el objeto ya no aparece en la colección, lo que evita fugas de memoria y accesos a memoria liberada.

Justificación: Esto demuestra que el objeto no queda “vivo” en memoria después de morir y que el vector no conserva referencias inválidas.

- Evidencia 7 — Prueba de condición límite
Elección del punto de inspección: ```particles.push_back(...)```
¿Por que aqui?: Porque este punto permite observar qué ocurre cuando se agregan muchas partículas rápidamente. Es ideal para evaluar el comportamiento del sistema bajo carga extrema.

<img width="1554" height="753" alt="image" src="https://github.com/user-attachments/assets/3e50b541-1072-46c3-a3a1-415f91c96cfa" />

Explicación: La prueba se diseñó para verificar que la aplicación funciona correctamente cuando no hay partículas activas. Al detenerse la ejecución al inicio de update(), se observa que particles.size() es 0, por lo que los bucles se omiten sin producir errores.

Justificación: Esto confirma que la implementación maneja correctamente el caso límite de un vector vacío y no intenta acceder a elementos inexistentes.

## Bitácora de reflexión
