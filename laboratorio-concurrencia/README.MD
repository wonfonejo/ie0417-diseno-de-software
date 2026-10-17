
# Laboratorio de programación concurrente y paralela en C++

## Estudiante

Nombre: Julián Martín Brenes Zúñiga

Carné: C31329

Curso: IE0417 - Diseño de Software para Ingeniería

## Descripción

Este laboratorio explora conceptos básicos de programación concurrente y paralela utilizando C++.

Se desarrollan seis ejercicios para observar la creación de hilos, las condiciones de carrera, los mecanismos de sincronización mediante mutex, la comparación de rendimiento entre ejecución secuencial y paralela, y los problemas de deadlock.

## Requisitos

- Compilador g++ compatible con C++17.
- Sistema operativo Windows con PowerShell.
- Soporte para hilos mediante std::thread.
- Git para el control de versiones.

## Estructura del proyecto

- src/: contiene los programas desarrollados.
- resultados/analisis.md: contiene las tablas, observaciones y respuestas del laboratorio.
- README.md: documentación e instrucciones de ejecución.

## Compilación y ejecución

Los siguientes comandos deben ejecutarse desde la carpeta laboratorio-concurrencia.

### Parte 1: Creación básica de hilos

Compilación:

```powershell
g++ -std=c++17 -Wall -Wextra -pthread src/parte1_threads.cpp -o parte1.exe
```

Ejecución:

```powershell
.\parte1.exe
```

### Parte 2: Condición de carrera

Compilación:

```powershell
g++ -std=c++17 -Wall -Wextra -pthread src/parte2_race_condition.cpp -o parte2.exe
```

Ejecución:

```powershell
.\parte2.exe
```

### Parte 3: Corrección usando mutex

Compilación:

```powershell
g++ -std=c++17 -Wall -Wextra -pthread src/parte3_mutex.cpp -o parte3.exe
```

Ejecución:

```powershell
.\parte3.exe
```

### Parte 4: Benchmark secuencial vs. paralelo

Compilación:

```powershell
g++ -std=c++17 -O2 -Wall -Wextra -pthread src/parte4_benchmark.cpp -o parte4.exe
```

Ejecución:

```powershell
.\parte4.exe
```

### Parte 5: Cantidad de hilos vs. rendimiento

Compilación:

```powershell
g++ -std=c++17 -O2 -Wall -Wextra -pthread src/parte5_hilos_vs_rendimiento.cpp -o parte5.exe
```

Ejecución:

```powershell
.\parte5.exe
```

### Parte 6: Ejemplo de deadlock

Compilación:

```powershell
g++ -std=c++17 -Wall -Wextra -pthread src/parte6_deadlock.cpp -o parte6.exe
```

Ejecución:

```powershell
.\parte6.exe
```

Nota: Este programa está diseñado para producir un deadlock. Se debe detener manualmente utilizando Ctrl + C.

### Parte 6: Corrección del deadlock

Compilación:

```powershell
g++ -std=c++17 -Wall -Wextra -pthread src/parte6_deadlock_corregido.cpp -o parte6_corregido.exe
```

Ejecución:

```powershell
.\parte6_corregido.exe
```

## Resultados

Los resultados experimentales y las respuestas a las preguntas de análisis se encuentran en resultados/analisis.md.

En las pruebas de rendimiento, la ejecución paralela obtuvo mejores tiempos que la secuencial. Además, se observó que aumentar la cantidad de hilos no siempre produce mejoras adicionales.

## Conclusiones

El laboratorio permitió comprender el funcionamiento básico de los hilos en C++ y la importancia de sincronizar correctamente el acceso a recursos compartidos.

Se observaron condiciones de carrera que produjeron resultados incorrectos, las cuales fueron corregidas mediante mutex. También se comprobó que el uso de múltiples hilos puede mejorar el rendimiento, aunque su efectividad depende de las características de la tarea y los recursos disponibles.

Finalmente, se reprodujo un deadlock y se corrigió utilizando std::scoped_lock.
