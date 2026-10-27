## Parte 4. Diferencias entre EXPECT y ASSERT

Se implementaron dos pruebas adicionales en el archivo
tests/test_calculator.cpp para comparar el comportamiento
de EXPECT y ASSERT.

### Prueba con EXPECT

Se implementó MultipleExpectChecks, que realiza tres
comprobaciones de suma mediante EXPECT_EQ.

EXPECT permite continuar ejecutando las siguientes
comprobaciones aunque alguna falle.

### Prueba con ASSERT

Se implementó AssertBeforeDivision, que utiliza ASSERT_NE
para comprobar que el divisor sea diferente de cero.

Inicialmente, con divisor = 2, la prueba se ejecutó
correctamente.

Posteriormente, se modificó el divisor a cero para
provocar un fallo intencional.

Google Test detectó que la condición ASSERT_NE(divisor, 0)
no se cumplía y detuvo la ejecución de esa prueba antes
de realizar la división.

Finalmente, se restauró divisor = 2 y se ejecutaron
nuevamente las pruebas.

### Diferencias observadas

EXPECT registra un fallo, pero permite continuar con
las siguientes instrucciones de la prueba.

ASSERT detiene inmediatamente la prueba cuando la
condición evaluada no se cumple.

ASSERT resulta especialmente útil cuando continuar
podría producir errores adicionales o resultados inválidos.

### Evidencia del fallo

![Fallo intencional con ASSERT](evidencias/03-fallo-assert.png)
