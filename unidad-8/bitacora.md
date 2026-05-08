# Unidad 8

<details>
<summary>Bitácora de proceso de aprendizaje</summary>

  ### Actividad 1
Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?
> Cuando ejecuto el programa y hago clic en la ventana, lo que observo es que la aplicación se congela completamente. El círculo deja de moverse y la ventana no responde durante unos segundos.
Yo esperaba que, al hacer clic, y doble clic se pausa y se vuelve a mover 
Esto sucede porque la función heavyComputation() realiza un cálculo muy pesado y se ejecuta en el hilo principal. Como ese hilo es el mismo que se encarga de dibujar en pantalla, mientras está ocupado haciendo el cálculo, no puede actualizar la interfaz, lo que provoca que todo se congele.

Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?
> Ahora, cuando ejecuto el programa y hago clic, veo que la aplicación ya no se congela. El círculo sigue moviéndose normalmente, lo cual indica que la interfaz sigue funcionando. 

Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?
> Sin embargo, noto que el tamaño del círculo no cambia inmediatamente, sino después de un tiempo.
Esto pasa porque ahora el cálculo pesado se está ejecutando en un hilo separado, es decir, el cambio no es inmediato porque depende de que el hilo secundario termine su trabajo.

En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?
> En mis propias palabras, la concurrencia es cuando un programa maneja varias tareas al mismo tiempo, pero en realidad puede estar alternando entre ellas muy rápido. No necesariamente se ejecutan al mismo instante, pero da la sensación de simultaneidad.
El paralelismo, en cambio, es cuando esas tareas sí se ejecutan realmente al mismo tiempo, usando diferentes núcleos del procesador.

> Es importante porque al trabajar con hilos necesitas saber qué quieres lograr: si se quiere que el programa no se bloquee, se usa concurrencia o si se quiere que el programa sea más rápido, se usa el paralelismo.
Entender esto te ayuda a: diseñar mejor el comportamiento de tu aplicación, evitar errores con datos compartidos, aprovechar mejor el hardware del computador.

  ### Actividad 2
Analiza de nuevo el código de la actividad anterior. ¿En qué partes del código se está protegiendo el acceso a la variable circleSize?
> En el código de la actividad anterior, el acceso a la variable circleSize se protege utilizando las funciones ```lock()``` y ```unlock()```.
> En ```draw()``` Aquí el hilo principal bloquea el acceso antes de leer circleSize para dibujar el círculo y luego libera el mutex.
> En ```heavyComputation()``` Aquí el hilo secundario bloquea el acceso antes de modificar circleSize.

Según lo que te he venido comentando, los hilos te permiten ejecutar tareas en paralelo; sin embargo, piensa qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido. ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?
> Cuando se sincroniza el acceso a un recurso compartido usando mutex, el paralelismo se reduce parcialmente porque los hilos ya no pueden acceder al recurso simultáneamente. Aunque los hilos siguen ejecutándose en paralelo, cuando uno entra a la sección protegida con lock(), los demás deben esperar hasta que el recurso sea liberado con unlock().
> Sí, el rendimiento puede verse afectado porque los mutex introducen tiempos de espera entre hilos.
Si muchos hilos necesitan acceder constantemente al mismo recurso compartido, puede generarse: espera entre hilos, bloqueos temporales, menor aprovechamiento del paralelismo.
Sin embargo, aunque puede disminuir un poco el rendimiento, el mutex es necesario para garantizar que los datos no se corrompan y evitar errores difíciles de detectar.

Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?
> Cuando useLock es verdadero, el programa funciona de forma segura y el valor final de counter normalmente coincide con el valor esperado. En cambio, cuando useLock es falso, el resultado del contador suele ser incorrecto y cambia cada vez que se ejecuta el programa.
Esto ocurre porque varios hilos están modificando la variable counter al mismo tiempo sin sincronización. Entonces algunos incrementos se “pierden” debido a que dos hilos pueden leer y escribir el mismo valor simultáneamente, por eso el contador final termina siendo menor al esperado.

Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.
> La condición de carrera ocurre porque varios hilos intentan modificar la misma variable compartida (counter) al mismo tiempo sin protección.
La instrucción: ```++(*counter);```
no ocurre en un solo paso. Internamente el procesador debe: leer el valor de counter desde memoria, guardarlo en un registro, incrementarlo, escribir el nuevo valor nuevamente en memoria.
El problema aparece cuando dos hilos hacen esto simultáneamente.

Ejemplo
> Supongamos que counter vale 10.
El hilo A lee 10
El hilo B también lee 10
El hilo A incrementa y escribe 11
El hilo B incrementa y también escribe 11

El resultado final es 11, cuando debería ser 12.
Uno de los incrementos se perdió porque ambos hilos trabajaron sobre el mismo valor inicial al mismo tiempo.

  ### Actividad 3
Ejecuta el código y observa el resultado.
> Al ejecutar el código, observé que el programa genera una imagen fractal del conjunto de Mandelbrot. Cuando presiono la tecla espacio, el programa comienza el cálculo y después de unos segundos aparece la imagen generada.

</details>

<details>
<summary>Bitácora de aplicación</summary>

 ### Actividad 5
1. Pega la parte clave de tu función modificada que calcula el píxel para el conjunto de Julia. Recuerda utilizar un bloque cpp.
```
int calculateJuliaPixel(int x, int y, glm::vec2 k) {
    float zx = ofMap(x, 0, imgWidth, -2.0, 2.0);
    float zy = ofMap(y, 0, imgHeight, -1.5, 1.5);
    int iterations = 0;

    while ((zx * zx + zy * zy) < 4.0 && iterations < maxIterations) {

        float tempX = zx * zx - zy * zy + k.x;
        zy = 2.0 * zx * zy + k.y;
        zx = tempX;

        iterations++;
    }

    return iterations;
}
```

2. Muestra cómo mapeaste la posición del mouse a la constante k.
   > La posición del mouse se convirtió en la constante compleja k usando ofMap().
   > De esta manera: mover horizontalmente cambia la parte real, mover verticalmente cambia la parte imaginaria
   
```
juliaK.x = ofMap(mouseX, 0, ofGetWidth(), -1.5f, 1.5f);
juliaK.y = ofMap(mouseY, 0, ofGetHeight(), -1.5f, 1.5f);
```

Esto permitió generar diferentes fractales de Julia en tiempo real dependiendo de la posición del mouse.
   
3. Describe brevemente cómo reutilizaste la estructura de hilos de la versión Mandelbrot. ¿Tuviste que cambiar mucho esa parte?
   > La estructura de hilos de Mandelbrot pudo reutilizarse casi completamente.
   > Cada hilo siguió: calculando un grupo de filas, trabajando en paralelo, escribiendo directamente sobre los píxeles correspondientes
   > Lo único que tuve que cambiar fue: reemplazar la función de Mandelbrot por la nueva función de Julia, pasar la constante k actualizada a cada hilo.
   > La lógica de: crear hilos, dividir filas, iniciar hilos, esperar resultados.
   > Se mantuvo prácticamente igual.
   
4. ¿Cómo te aseguraste de que la imagen se recalculara cuando el mouse se movía?
   > Para asegurarme de que la imagen se actualizara: detecté cambios en la posición del mouse, actualicé juliaK, lancé nuevamente, startCalculation()
   > Así, cada vez que el usuario movía el mouse: cambiaba la constante k, los hilos recalculaban el fractal completo, la textura se, actualizaba en pantalla.
   > Esto creó una exploración interactiva del conjunto de Julia.
   
5. Incluye al menos dos capturas de pantalla que muestren diferentes fractales de Julia generados al mover el mouse en tu aplicación.
   Cap1:
   <img width="1019" height="796" alt="image" src="https://github.com/user-attachments/assets/15df69dd-279c-4204-8f5f-4813c23b6c86" />

   Cap2:
   <img width="1022" height="794" alt="image" src="https://github.com/user-attachments/assets/8a90c2c4-1e6f-413b-95e5-72efef343f44" />

   Cap3:
   
7. ¿Encontraste algún desafío particular al implementar la interacción o modificar el cálculo?
   > Uno de los principales desafíos fue entender la diferencia matemática entre Mandelbrot y Julia, especialmente: qué valor inicia en z, cuál valor permanece constante.
   > También fue importante controlar el recálculo continuo porque mover el mouse genera muchas actualizaciones rápidamente.
   > Otro reto fue asegurar que los hilos terminaran correctamente antes de iniciar nuevos cálculos, evitando conflictos o sobrecarga innecesaria.
  
</details>

<details>
<summary>Bitácora de reflexión</summary>
</details>
