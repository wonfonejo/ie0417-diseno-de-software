
# Análisis del laboratorio

## Parte 1: Creación básica de hilos

### 1. ¿Los mensajes aparecen siempre en el mismo orden?

No. Durante las cinco ejecuciones se observaron diferentes órdenes de impresión. Además, algunos mensajes aparecieron mezclados entre sí.

### 2. ¿Por qué podría cambiar el orden de impresión?

Porque los hilos se ejecutan concurrentemente y el sistema operativo decide cuándo asignarles tiempo de CPU. Por eso, el orden de ejecución no está garantizado.

### 3. ¿Qué función cumple join()?

La función join() hace que el hilo principal espere a que un hilo termine su ejecución antes de continuar.

### 4. ¿Qué podría pasar si no se llama a join()?

Si un objeto std::thread se destruye mientras todavía representa un hilo al que no se le ha aplicado join() o detach(), el programa termina mediante std::terminate().


## Parte 2: Condición de carrera

### Resultados obtenidos

| Ejecución | Valor esperado | Valor obtenido |
|-----------|----------------|----------------|
| 1 | 4000000 | 1295526 |
| 2 | 4000000 | 1245458 |
| 3 | 4000000 | 1371763 |
| 4 | 4000000 | 1412127 |
| 5 | 4000000 | 1166145 |

### 1. ¿El valor obtenido siempre coincide con el valor esperado?

No. En ninguna de las cinco ejecuciones se obtuvo el valor esperado de 4000000. Los resultados fueron considerablemente menores y variaron entre ejecuciones.

### 2. ¿Por qué se pierden incrementos?

Porque varios hilos modifican simultáneamente la misma variable. Dos hilos pueden leer el mismo valor del contador antes de actualizarlo, provocando que uno de los incrementos sobrescriba al otro.

### 3. ¿La operación contador++ es realmente una sola operación a nivel de CPU?

No necesariamente. Esta operación implica leer el valor actual, incrementarlo y almacenar el resultado. Al no estar sincronizada, otros hilos pueden interferir durante este proceso.

### 4. ¿Qué problema de concurrencia se está observando?

Se observa una condición de carrera, ya que varios hilos acceden y modifican una variable compartida sin mecanismos de sincronización. Esto provoca un comportamiento indefinido y resultados que no son confiables.


## Parte 3: Corrección usando mutex

### Resultados obtenidos

| Ejecución | Valor esperado | Valor obtenido |
|-----------|----------------|----------------|
| 1 | 4000000 | 4000000 |
| 2 | 4000000 | 4000000 |
| 3 | 4000000 | 4000000 |
| 4 | 4000000 | 4000000 |
| 5 | 4000000 | 4000000 |

### 1. ¿Qué cambió con respecto al programa anterior?

Se incorporó un mutex para proteger el acceso a la variable compartida contador. A diferencia de la Parte 2, todas las ejecuciones produjeron el resultado esperado de 4000000.

### 2. ¿Qué hace std::mutex?

Permite controlar el acceso a un recurso compartido, evitando que varios hilos ejecuten simultáneamente una sección crítica protegida por el mismo mutex.

### 3. ¿Qué hace std::lock_guard?

Bloquea automáticamente el mutex al crearse y lo libera cuando sale de su ámbito. Esto evita tener que utilizar manualmente las funciones lock() y unlock().

### 4. ¿Por qué ahora el resultado sí debería ser correcto?

Porque el mutex garantiza que solamente un hilo a la vez pueda incrementar el contador. Esto evita que se pierdan actualizaciones cuando varios hilos intentan modificar la variable compartida.

### 5. ¿Qué desventaja podría tener proteger cada incremento individual con un mutex?

Puede reducir el rendimiento, ya que cada incremento requiere bloquear y desbloquear el mutex. Además, los hilos deben esperar su turno para acceder al contador, lo que limita el paralelismo.



## Parte 4: Benchmark secuencial vs. paralelo

### Resultados obtenidos

| Ejecución | Tiempo secuencial | Tiempo paralelo | Más rápido |
|-----------|-------------------|-----------------|------------|
| 1 | 49 ms | 28 ms | Paralelo |
| 2 | 48 ms | 28 ms | Paralelo |
| 3 | 50 ms | 28 ms | Paralelo |

### 1. ¿El resultado secuencial y el paralelo son iguales?

Sí. En las tres ejecuciones ambos métodos obtuvieron el resultado esperado de 100000000.

### 2. ¿La versión paralela siempre fue más rápida?

En las tres pruebas realizadas, sí. La versión secuencial tardó entre 48 y 50 ms, mientras que la paralela tardó 28 ms en todas las ejecuciones. Sin embargo, esto no significa que la ejecución paralela siempre sea más rápida en cualquier situación.

### 3. ¿Por qué dividir el vector en bloques permite paralelizar el trabajo?

Porque cada hilo puede calcular independientemente la suma de una sección del vector. Después de finalizar los hilos, se combinan las sumas parciales para obtener el resultado total.

### 4. ¿Qué costos adicionales tiene la versión paralela?

La creación y administración de los hilos, su sincronización y la combinación de resultados parciales. Estos procesos consumen recursos adicionales.

### 5. ¿Qué podría pasar si el vector fuera muy pequeño?

La versión paralela podría resultar más lenta, ya que el costo de crear y administrar los hilos podría ser mayor que el tiempo ahorrado al distribuir el trabajo.


### 3. ¿Cuántos núcleos tiene la computadora donde se ejecutó el programa?

La computadora utilizada tiene 6 núcleos físicos y 12 procesadores lógicos, según los resultados obtenidos mediante PowerShell.



### Conclusión

Los resultados muestran que aumentar la cantidad de hilos puede mejorar el rendimiento hasta cierto punto. Las configuraciones de 4 y 8 hilos obtuvieron los mejores tiempos, con 30 ms, mientras que la configuración de 16 hilos tardó 31 ms. Aunque la computadora dispone de 6 núcleos físicos y 12 procesadores lógicos, utilizar más hilos no produjo una mejora continua. Esto demuestra que el rendimiento también depende de factores como la administración de los hilos y el acceso a memoria.


## Parte 5: Cantidad de hilos vs. rendimiento

### Resultados obtenidos

| Cantidad de hilos | Tiempo obtenido |
|-------------------|-----------------|
| 1 | 54 ms |
| 2 | 41 ms |
| 4 | 30 ms |
| 8 | 30 ms |
| 16 | 31 ms |

### 1. ¿Cuál cantidad de hilos produjo el mejor tiempo?

Las configuraciones de 4 y 8 hilos obtuvieron el mejor tiempo de ejecución, con 30 ms en ambos casos.

### 2. ¿El tiempo mejoró siempre al aumentar los hilos?

No. El tiempo disminuyó al pasar de 1 a 4 hilos, pero se mantuvo igual con 8 hilos y aumentó ligeramente al utilizar 16 hilos. Esto demuestra que aumentar la cantidad de hilos no garantiza una mejora continua del rendimiento.

### 3. ¿Cuántos núcleos tiene la computadora donde se ejecutó el programa?

La computadora utilizada tiene 6 núcleos físicos y 12 procesadores lógicos, según los resultados obtenidos mediante PowerShell.

### 4. ¿Qué ocurre cuando se usan más hilos que núcleos disponibles?

Cuando se utilizan más hilos que procesadores lógicos disponibles, el sistema operativo debe alternar su ejecución entre los procesadores. Esto puede generar costos adicionales de administración y reducir las mejoras de rendimiento.

### 5. ¿Qué relación tiene esto con el context switching?

El context switching es el proceso mediante el cual el sistema operativo cambia la ejecución de un hilo a otro. Cuando hay más hilos listos para ejecutarse que procesadores disponibles, pueden producirse más cambios de contexto, lo que consume tiempo y recursos.

### 6. ¿Por qué la versión con 16 hilos podría no ser la mejor?

Porque la computadora dispone de 12 procesadores lógicos y ejecutar 16 hilos puede generar costos adicionales de planificación y cambios de contexto. Además, factores como el acceso a memoria y la administración de los hilos pueden limitar el rendimiento. En las pruebas, esta configuración tardó 31 ms, mientras que con 4 y 8 hilos se obtuvieron 30 ms.

### Conclusión

Los resultados muestran que aumentar la cantidad de hilos puede mejorar el rendimiento, pero solamente hasta cierto punto. El tiempo disminuyó de 54 ms con un hilo a 30 ms con cuatro hilos, lo que representa una mejora considerable. Sin embargo, utilizar 8 hilos no produjo una mejora adicional y con 16 hilos el tiempo aumentó ligeramente.

Aunque la computadora cuenta con 6 núcleos físicos y 12 procesadores lógicos, los mejores resultados se obtuvieron utilizando 4 y 8 hilos. Esto demuestra que el rendimiento no depende únicamente de la cantidad de hilos, sino también de los costos de administración y las características de la tarea.

## Parte 6: Ejemplo simple de deadlock

### Resultados obtenidos

Al ejecutar el programa, ambos hilos intentaron acceder a los dos recursos compartidos. Sin embargo, ninguno logró obtener ambos recursos y el programa quedó bloqueado. Fue necesario interrumpir manualmente su ejecución.

### 1. ¿El programa termina normalmente?

No. El programa quedó bloqueado porque ambos hilos esperaban recursos que estaban siendo utilizados por el otro. Fue necesario detenerlo manualmente.

### 2. ¿Qué recurso tomó primero el hilo A?

El hilo A tomó primero el recurso 1, mediante recurso1.lock().

### 3. ¿Qué recurso tomó primero el hilo B?

El hilo B tomó primero el recurso 2, mediante recurso2.lock().

### 4. ¿Por qué ninguno de los dos hilos puede continuar?

Porque el hilo A mantiene bloqueado el recurso 1 mientras espera el recurso 2, y el hilo B mantiene bloqueado el recurso 2 mientras espera el recurso 1. Ninguno puede continuar ni liberar su recurso.

### 5. ¿Qué significa espera circular?

Es una situación en la que dos o más hilos forman una cadena de dependencias, donde cada uno espera un recurso que está siendo retenido por otro hilo de la misma cadena. Esto puede provocar un deadlock.

### 6. ¿Cómo se podría evitar este problema?

Se puede evitar estableciendo un orden consistente para adquirir los recursos o utilizando mecanismos como std::scoped_lock, que permite bloquear varios mutex de forma conjunta evitando este tipo de deadlock.


### Corrección del deadlock usando std::scoped_lock

Al ejecutar la versión corregida, ambos hilos lograron obtener los recursos de forma segura y el programa finalizó normalmente, sin presentar bloqueos.

### ¿Por qué std::scoped_lock ayuda a evitar este deadlock?

std::scoped_lock permite administrar el bloqueo de varios mutex simultáneamente mediante un mecanismo que evita el deadlock. De esta manera, se impide que los hilos queden esperando indefinidamente los recursos retenidos por otros. Además, los mutex se liberan automáticamente cuando el objeto scoped_lock sale de su ámbito.


## Parte 7: Reflexión final

### 1. ¿Cuál fue la diferencia más clara que observó entre ejecución secuencial y ejecución con hilos?

En la ejecución secuencial, las operaciones se realizan una después de otra, mientras que la ejecución con varios hilos permite distribuir el trabajo. En las pruebas realizadas, la suma paralela obtuvo mejores tiempos que la secuencial.

### 2. ¿Qué es una condición de carrera?

Es un problema que ocurre cuando varios hilos acceden a recursos compartidos sin una sincronización adecuada y el resultado depende del orden en que se ejecutan sus operaciones.

### 3. ¿Por qué contador++ puede fallar cuando muchos hilos lo ejecutan al mismo tiempo?

Porque incrementar un contador implica leer su valor, modificarlo y almacenar el resultado. Si varios hilos realizan estas operaciones simultáneamente sin sincronización, pueden perderse incrementos.

### 4. ¿Qué problema resuelve un mutex?

Un mutex permite proteger una sección crítica, evitando que varios hilos accedan simultáneamente a un recurso compartido de forma que produzcan conflictos.

### 5. ¿Qué ventaja tiene std::lock_guard sobre llamar manualmente a lock() y unlock()?

Permite administrar automáticamente el bloqueo y la liberación del mutex, reduciendo el riesgo de olvidar desbloquearlo y facilitando el mantenimiento del código.

### 6. ¿Por qué más hilos no siempre significan mejor rendimiento?

Porque crear y administrar hilos tiene un costo. Además, el rendimiento depende de factores como los núcleos disponibles, el acceso a memoria y la planificación del sistema operativo. En nuestras pruebas, aumentar de 8 a 16 hilos no mejoró el tiempo de ejecución.

### 7. ¿Qué es un deadlock?

Es una situación en la que dos o más hilos quedan bloqueados indefinidamente porque cada uno espera recursos que están siendo retenidos por otros hilos.

### 8. ¿Qué buenas prácticas aplicaría al programar con hilos?

Proteger los recursos compartidos mediante mecanismos de sincronización, utilizar herramientas como lock_guard y scoped_lock, evitar bloqueos innecesarios y seleccionar una cantidad adecuada de hilos según la tarea.

### 9. ¿En qué tipo de programas reales podría ser útil la programación concurrente?

En servidores web que atienden múltiples solicitudes, aplicaciones que realizan operaciones de entrada y salida simultáneamente y programas con interfaces gráficas que deben mantenerse disponibles mientras ejecutan otras tareas.

### 10. ¿En qué tipo de programas reales podría ser útil la programación paralela?

En simulaciones científicas, procesamiento de imágenes, análisis de grandes cantidades de datos y cálculos matemáticos que pueden dividirse en tareas independientes para aprovechar varios núcleos del procesador.
