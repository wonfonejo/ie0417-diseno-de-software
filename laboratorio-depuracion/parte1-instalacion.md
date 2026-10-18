
# Parte 1: Instalación y verificación del ambiente

## 1. Entorno utilizado

El laboratorio se desarrolla utilizando Ubuntu mediante WSL2 (Windows Subsystem for Linux), con las siguientes herramientas:

| Herramienta | Versión |
|-------------|---------|
| Sistema operativo | Ubuntu (WSL2) |
| g++ | 15.2.0 |
| GDB | 17.1 |
| Valgrind | 3.26.0 |

## 2. Verificación de las herramientas

Se verificó la instalación utilizando los siguientes comandos:

```bash
g++ --version
gdb --version
valgrind --version
```

Los tres comandos mostraron correctamente las versiones instaladas, confirmando que las herramientas están disponibles.

## 3. Compilación y ejecución del programa de prueba

Se creó el archivo `codigo/prueba.cpp` con el siguiente contenido:

```cpp
#include <iostream>

int main() {
    std::cout << "Ambiente listo para depuración" << std::endl;
    return 0;
}
```

### Compilación

```bash
g++ -g -o prueba codigo/prueba.cpp
```

La compilación finalizó correctamente, sin mostrar errores.

### Ejecución

```bash
./prueba
```

Resultado obtenido:

```text
Ambiente listo para depuración
```

El programa se ejecutó correctamente, confirmando que el entorno está preparado para comenzar las actividades de depuración.

## 4. Función de las herramientas

- g++: compilador que transforma el código fuente de C++ en programas ejecutables.
- GDB: depurador que permite detener la ejecución, inspeccionar variables y analizar el comportamiento del programa.
- Valgrind: conjunto de herramientas de análisis que permite detectar problemas como pérdidas de memoria y accesos inválidos.

## 5. Preguntas de reflexión

### 1. ¿Para qué sirve g++?

Sirve para compilar programas escritos en C++, convirtiendo el código fuente en archivos ejecutables.

### 2. ¿Para qué sirve gdb?

Permite depurar programas, ejecutar instrucciones paso a paso, establecer puntos de interrupción e inspeccionar variables para identificar errores.

### 3. ¿Para qué sirve valgrind?

Permite analizar el comportamiento de los programas, especialmente su uso de memoria, para detectar errores como pérdidas de memoria y accesos inválidos.

### 4. ¿Por qué se recomienda compilar con -g al depurar?

Porque esta opción incorpora información de depuración en el ejecutable, lo que permite relacionar las instrucciones del programa con las líneas del código fuente y examinar sus variables mediante GDB.

### 5. ¿Qué diferencia hay entre compilar un programa y depurarlo?

Compilar consiste en transformar el código fuente en un programa ejecutable y detectar ciertos errores del código. Depurar consiste en analizar el comportamiento del programa para identificar y corregir problemas que pueden aparecer durante su ejecución.
