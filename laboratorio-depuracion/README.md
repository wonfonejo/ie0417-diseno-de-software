
# Laboratorio de depuración con GDB, Valgrind y Sanitizers

## Estudiante

Nombre: Julián Martín Brenes Zúñiga

Carné: C31329

Curso: IE0417 - Diseño de Software para Ingeniería

## Descripción

Este laboratorio tiene como objetivo practicar diferentes técnicas de depuración en C++, utilizando herramientas como GDB, Valgrind, AddressSanitizer, ThreadSanitizer y Helgrind.

Se desarrollaron ejercicios para identificar errores de sintaxis, errores lógicos, problemas de memoria y condiciones de carrera. Cada actividad incluye el análisis de los problemas encontrados, las correcciones realizadas y las evidencias correspondientes.

## Requisitos

- Ubuntu mediante WSL2.
- Compilador g++ compatible con C++17.
- GDB.
- Valgrind.
- Soporte para AddressSanitizer y ThreadSanitizer.
- Git.

## Estructura del proyecto

- codigo/: programas C++ utilizados en los ejercicios.
- evidencias/: capturas de los resultados de las herramientas.
- Archivos Markdown: documentación y análisis de cada parte.

## Índice del laboratorio

### Parte 1: Instalación y verificación del ambiente

[Ver documentación](parte1-instalacion.md)

Verificación del compilador y las herramientas de depuración.

### Parte 2: Tipos de errores

[Ver documentación](parte2-tipos-errores.md)

Identificación y corrección de errores de sintaxis y errores lógicos.

### Parte 3: Introducción a GDB

[Ver documentación](parte3-gdb-basico.md)

Uso de breakpoints, ejecución paso a paso e inspección de variables.

### Parte 4: Step, next y backtrace

[Ver documentación](parte4-gdb-funciones.md)

Análisis de un error de división entre cero mediante GDB.

### Parte 5: Análisis de memoria con Valgrind

[Ver documentación](parte5-valgrind.md)

Detección y corrección de pérdidas de memoria y accesos fuera de los límites de un arreglo.

### Parte 6: AddressSanitizer

[Ver documentación](parte6-asan.md)

Identificación y corrección de un error de acceso a memoria después de liberarla.

### Parte 7: Análisis de hilos

[Ver documentación](parte7-hilos.md)

Detección de condiciones de carrera mediante ThreadSanitizer y Helgrind, y corrección utilizando mutex.

### Parte 8: Mini reto de depuración

[Ver documentación](parte8-reto-y-reflexion.md)

Identificación y corrección de cuatro errores en un mismo programa, utilizando Valgrind y AddressSanitizer.

### Parte 9: Reflexión final

La reflexión final se encuentra en el documento de la Parte 8 e incluye las respuestas a las quince preguntas solicitadas.

## Compilación y ejecución

Los programas se compilan desde una terminal de Ubuntu, ubicada en la carpeta laboratorio-depuracion.

Ejemplo de compilación:

```bash
g++ -g -o prueba codigo/prueba.cpp
```

Ejemplo de ejecución:

```bash
./prueba
```

Para analizar un programa con Valgrind:

```bash
valgrind --leak-check=full ./programa
```

Para utilizar GDB:

```bash
gdb ./programa
```

Para activar AddressSanitizer:

```bash
g++ -g -fsanitize=address -o programa_asan codigo/archivo.cpp
```

Para activar ThreadSanitizer:

```bash
g++ -g -fsanitize=thread -pthread -o programa_tsan codigo/archivo.cpp
```

Los comandos específicos de cada ejercicio se encuentran en sus respectivos archivos Markdown.

## Resultados y conclusiones

Las actividades permitieron comprender la importancia de analizar el comportamiento de los programas, incluso cuando compilan y se ejecutan aparentemente sin errores.

GDB facilitó la inspección de variables y la identificación de errores de ejecución. Valgrind y AddressSanitizer permitieron detectar problemas de memoria, mientras que ThreadSanitizer y Helgrind ayudaron a identificar condiciones de carrera.

Finalmente, se comprobó que las correcciones realizadas eliminaban los errores detectados en las pruebas y producían los resultados esperados.
