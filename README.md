# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?

        Al no tener método main ni interfaz de usuario, el proyecto se centra en aislar la unidad lógica más pequeña y hacer pruebas. Al tener estas pruebas automatizadas, se puede modificar el código de la calculadora en el futuro o añadir nuevas operaciones, lo que supone un ahorro de recursos para la empresa.

        Podría usarse para integrarse posteriormente como una librería en un sistema de información más complejo, como una app movil de calculadora.

2. Revisa las pruebas de la suma y comenta lo que te parezca de interés

        El desarrollo separa el código fuente del código de pruebas en carpetas distintas, utilizando JUnit 5.

        El test sumarPositivosMal() está hecho para que falle a propósito. Esto sirve para confirmar que el sistema detecta los errores.

3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.

        Entradas: a (dividendo, int), b (divisor,int).
        Salida: Resultado int u OperacionNoValidaException

        1. Clases de Equivalencia:

        Dividendo (a):

        CE1: Números positivos.

        CE2: Negativos.

        CE3: El 0.

        Divisor (b):

        CE4: Positivos (Válido).

        CE5: Negativos (Válido).

        CE6: El 0 (No válido).
        

        2. Valores limite:
        
        Límites del Dividendo (a): Probaremos un numero positivo y uno negativo, además de probar el 0 para comprobar que el programa lo tolera.

        Límites del Divisor (b):

                Límite inferior válido: -1

                Valor crítico (inválido): 0

                Límite superior válido: 1


        3. Conjetura de errores:
        
        Comprobamos que cuando el divisor es 0, da error.


| Caso de Prueba | Valores (a, b) | Salida Esperada |
| :--- | :--- | :--- |
| CP1 | 4, 2 | 2 |
| CP2 | 4, -2 | -2 |
| CP3 | -4, 2 | -2 |
| CP4 | -4, -2 | 2 |
| CP5 | 0, 2 | 0 |
| CP6 | 0, -2 | 0 |
| CP7 | 4, 0 | OperacionNoValidaException |
| CP8 | -4, 0 | OperacionNoValidaException |
| CP9 | 0, 0 | OperacionNoValidaException |
        

```java
    @Test
    void testDividirValidos() {
        // Agrupamos los casos del CP1 al CP6 
        assertAll("Divisiones con resultado válido",
            () -> assertEquals(2, Calculadora.dividir(4, 2), "CP1"),
            () -> assertEquals(-2, Calculadora.dividir(4, -2), "CP2"),
            () -> assertEquals(-2, Calculadora.dividir(-4, 2), "CP3"),
            () -> assertEquals(2, Calculadora.dividir(-4, -2), "CP4"),
            () -> assertEquals(0, Calculadora.dividir(0, 2), "CP5"),
            () -> assertEquals(0, Calculadora.dividir(0, -2), "CP6")
        );
    }

    @Test
    void testDividirPorCero() {
        // Agrupamos los casos de error del CP7 al CP9
        assertAll("Divisiones por cero (Excepciones)",
            () -> assertThrows(OperacionNoValidaException.class, () -> Calculadora.dividir(4, 0), "CP7"),
            () -> assertThrows(OperacionNoValidaException.class, () -> Calculadora.dividir(-4, 0), "CP8"),
            () -> assertThrows(OperacionNoValidaException.class, () -> Calculadora.dividir(0, 0), "CP9")
        );
    }
    }```


