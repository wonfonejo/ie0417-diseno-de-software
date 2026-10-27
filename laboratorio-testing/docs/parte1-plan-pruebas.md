
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
