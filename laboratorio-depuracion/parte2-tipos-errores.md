
# Parte 2: Tipos de errores

## Ejercicio 1: Error de sintaxis

### Error observado

Al intentar compilar el programa original, el compilador mostró el siguiente mensaje:

```text
error: expected ';' before 'return'
```

### Causa del error

El error se encontraba en la línea 5, donde faltaba un punto y coma al finalizar la instrucción de impresión.

### Comando de compilación

```bash
g++ -g -o error_sintaxis codigo/01_error_sintaxis.cpp
```

### Corrección realizada

Se agregó el punto y coma faltante:

```cpp
std::cout << "Hola mundo" << std::endl;
```

### Resultado final

Después de corregir el código, el programa compiló correctamente y produjo la siguiente salida:

```text
Hola mundo
```

## Preguntas de reflexión

### 1. ¿Este error fue detectado antes o durante la ejecución?

Fue detectado antes de la ejecución, durante el proceso de compilación.

### 2. ¿Qué herramienta detectó el error?

El compilador g++, que identificó la ausencia del punto y coma y mostró la ubicación del problema.

### 3. ¿Por qué este tipo de error suele ser más fácil de corregir que un error lógico?

Porque el compilador normalmente indica dónde se encuentra el problema y proporciona un mensaje que ayuda a identificarlo. En cambio, un error lógico puede permitir que el programa compile y se ejecute, pero produzca resultados incorrectos.


## Ejercicio 2: Error lógico

### Código original

La función original calculaba la suma de las notas, pero no realizaba la división necesaria para obtener el promedio.

```cpp
double calcular_promedio(const std::vector<int>& notas) {
    int suma = 0;

    for (int nota : notas) {
        suma += nota;
    }

    return suma;
}
```

### Compilación y ejecución

Comando de compilación:

```bash
g++ -g -o error_logico codigo/02_error_logico.cpp
```

Comando de ejecución:

```bash
./error_logico
```

### Resultado observado

El programa compiló correctamente, pero produjo el siguiente resultado:

```text
Promedio: 270
```

El promedio esperado era:

(80 + 90 + 100) / 3 = 90

### Causa del error

La función calcular_promedio sumaba correctamente los elementos del vector, pero retornaba directamente la suma sin dividirla entre la cantidad de notas.

### Corrección realizada

Se reemplazó la instrucción de retorno por:

```cpp
return static_cast<double>(suma) / notas.size();
```

Esta modificación permite calcular el promedio mediante una división con resultado decimal.

### Resultado final

Después de corregir el código y ejecutarlo nuevamente, se obtuvo:

```text
Promedio: 90
```

### Preguntas de reflexión

#### 1. ¿Por qué el compilador no detectó este error?

Porque el código era sintácticamente válido y no presentaba operaciones prohibidas. El compilador no puede determinar que la intención del programa era calcular un promedio y no una suma.

#### 2. ¿Por qué este error se considera lógico?

Porque el programa compila y se ejecuta correctamente, pero produce un resultado diferente al esperado debido a un error en el procedimiento de cálculo.

#### 3. ¿Qué estrategia usó para encontrarlo?

Se comparó el resultado obtenido con el promedio calculado manualmente. Después se revisó la función para identificar que faltaba dividir la suma entre la cantidad de elementos.

#### 4. ¿Qué pruebas adicionales podría hacer?

Se podrían probar vectores con distintas cantidades de notas, valores iguales y resultados decimales para verificar que el promedio se calcule correctamente en diferentes situaciones.

