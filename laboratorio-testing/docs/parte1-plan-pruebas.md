
## Parte 9. Pruebas funcionales

### Objetivo

Verificar que la función de conversión de calificaciones cumpla con los requisitos establecidos para el sistema, incluyendo entradas normales, valores límite y valores inválidos.

### Requisito funcional

El sistema debe convertir calificaciones numéricas entre 0 y 100 a letras, de acuerdo con los siguientes intervalos:

- De 90 a 100: A.
- De 80 a 89: B.
- De 70 a 79: C.
- De 60 a 69: D.
- De 0 a 59: F.

Las calificaciones fuera del intervalo permitido deben producir una excepción.

### Tabla de casos funcionales

| ID | Requisito | Entrada | Resultado esperado | Tipo de caso |
|---|---|---|---|---|
| TC-001 | Convertir nota excelente | 95 | A | Normal |
| TC-002 | Límite inferior de A | 90 | A | Borde |
| TC-003 | Límite superior de B | 89 | B | Borde |
| TC-004 | Nota inválida baja | -1 | Excepción | Inválido |
| TC-005 | Nota inválida alta | 101 | Excepción | Inválido |

### Implementación de las pruebas

Se revisaron las pruebas existentes en el archivo `tests/test_grade_utils.cpp`.

Los casos TC-001, TC-002, TC-003 y TC-004 ya estaban cubiertos por las pruebas implementadas anteriormente.

Se identificó que faltaba comprobar explícitamente el rechazo de una calificación igual a 101.

Por esta razón, se agregó la prueba `GradeAboveMaximumThrowsException`, utilizando `EXPECT_THROW` para comprobar que la función produzca una excepción de tipo `std::invalid_argument`.

### Resultados

Después de agregar la prueba, se compiló nuevamente el proyecto y se ejecutaron los comandos:

```bash
make
./run_tests
ctest --output-on-failure
```

Se ejecutaron 42 pruebas automatizadas y todas fueron exitosas.

Los cinco casos funcionales definidos quedaron cubiertos.

### ¿Por qué se consideran pruebas funcionales?

Porque fueron diseñadas a partir del comportamiento esperado del sistema y de los requisitos de conversión de calificaciones.

Aunque se implementaron mediante pruebas unitarias, su selección responde a requisitos funcionales específicos y no solamente a detalles internos de la implementación.

### Preguntas de reflexión

#### 1. ¿Qué diferencia hay entre una prueba unitaria y una prueba funcional?

Una prueba unitaria comprueba el comportamiento de una función o componente individual. Una prueba funcional verifica que el sistema cumpla con un requisito de comportamiento definido.

#### 2. ¿Por qué una prueba funcional se relaciona con requisitos?

Porque permite comprobar si el comportamiento implementado coincide con las condiciones que debe cumplir el sistema.

#### 3. ¿Qué significa pensar desde la perspectiva del usuario o del sistema?

Significa concentrarse en qué resultados debe producir el programa ante determinadas entradas, independientemente de cómo esté implementado internamente.

#### 4. ¿Por qué la documentación de casos de prueba ayuda al equipo?

Porque permite identificar los requisitos evaluados, las entradas utilizadas y los resultados esperados, facilitando la comprensión, reproducción y mantenimiento de las pruebas.

## Parte 1. Preparación del proyecto

### Objetivo

Preparar el entorno de desarrollo y establecer la estructura de un proyecto en C++ que permita implementar y ejecutar pruebas automatizadas mediante Google Test y CMake.

### Herramientas utilizadas

#### CMake

CMake es una herramienta que permite configurar y organizar la compilación de proyectos de software.

En este laboratorio se utilizó para establecer el estándar C++17, definir los archivos fuente, integrar Google Test y generar el ejecutable encargado de las pruebas.

#### Google Test

Google Test es un framework para implementar pruebas automatizadas en C++.

Permite definir casos de prueba y utilizar instrucciones como `EXPECT_EQ`, `EXPECT_TRUE`, `EXPECT_FALSE` y `ASSERT_NE` para comprobar el comportamiento de las funciones.

#### Automatización de pruebas

Automatizar pruebas consiste en preparar verificaciones que puedan ejecutarse mediante comandos, sin necesidad de comprobar manualmente cada resultado.

Esto permite repetir las verificaciones después de realizar modificaciones en el código.

#### Repetibilidad

Una prueba repetible permite obtener resultados consistentes cuando se ejecuta bajo las mismas condiciones.

Esta característica es importante porque facilita identificar errores y comprobar que las correcciones realizadas funcionan correctamente.

### Estructura creada

Se creó la carpeta `laboratorio-testing` dentro del repositorio del curso.

El proyecto se organizó en las siguientes carpetas:

- `include/`: declaraciones de funciones en archivos de cabecera.
- `src/`: implementación de las funciones en C++.
- `tests/`: pruebas automatizadas mediante Google Test.
- `docs/`: documentación de las actividades y resultados.
- `.github/workflows/`: configuración del workflow de GitHub Actions.

También se creó el archivo `CMakeLists.txt` para configurar la compilación.

### Preguntas de reflexión

#### 1. ¿Por qué conviene separar el código fuente de las pruebas?

Porque facilita la organización y el mantenimiento del proyecto. Además, permite modificar las pruebas sin alterar directamente la implementación de las funciones.

#### 2. ¿Qué ventaja tiene usar CMake en un proyecto de C++?

Permite organizar la compilación y gestionar las dependencias desde un archivo de configuración, evitando tener que ejecutar manualmente comandos extensos para compilar cada archivo.

#### 3. ¿Por qué es útil que las pruebas se puedan ejecutar con un solo comando?

Porque simplifica la verificación del proyecto y permite comprobar rápidamente si las modificaciones introdujeron errores.

#### 4. ¿Qué diferencia hay entre probar manualmente y probar automáticamente?

Las pruebas manuales requieren que una persona ejecute y revise los resultados de cada caso. Las pruebas automatizadas realizan estas comprobaciones mediante código, lo que facilita repetirlas y detectar inconsistencias.
