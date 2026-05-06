# Unidad 8

<details>
<summary>Bitácora de proceso de aprendizaje</summary>

  ### Actividad 1
Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?
> Cuando ejecuto el programa y hago clic en la ventana, lo que observo es que la aplicación se congela completamente. El círculo deja de moverse y la ventana no responde durante unos segundos.
Yo esperaba que, al hacer clic, y doble clic se pausa y se vuelve a mover 
Esto sucede porque la función heavyComputation() realiza un cálculo muy pesado y se ejecuta en el hilo principal. Como ese hilo es el mismo que se encarga de dibujar en pantalla, mientras está ocupado haciendo el cálculo, no puede actualizar la interfaz, lo que provoca que todo se congele.

Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?

Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?

En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?q

  ### Actividad 2
Analiza de nuevo el código de la actividad anterior. ¿En qué partes del código se está protegiendo el acceso a la variable circleSize?

Según lo que te he venido comentando, los hilos te permiten ejecutar tareas en paralelo; sin embargo, piensa qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido. ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?

Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?

Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.

  ### Actividad 3
Ejecuta el código y observa el resultado.

Analiza el código y estudia detenidamente su funcionamiento. En la fase de aplicación tendrás que retomar este código para resolver un reto.

Experimenta modificando, PERO, no olvides cómo investigamos en este curso:

Realiza cambios pequeños y específicos.
Lanza una hipótesis sobre lo que crees que va a pasar.
Ejecuta el código y observa lo que ocurre.
¿Tu hipótesis era correcta? ¿Por qué crees que ocurre esto?
Te dejo una idea para comenzar a experimentar: ¿Qué ocurre si cambias el número de hilos? ¿Por qué crees que ocurre esto?

  ### Actividad 4
</details>

<details>
<summary>Bitácora de aplicación</summary>

 ### Actividad 5
  
</details>

<details>
<summary>Bitácora de reflexión</summary>
</details>
