# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?

        Realizar pruebas unitarias sobre un componente del sistema (en este caso, la lógica de una calculadora). Al no tener método main ni interfaz de usuario, el proyecto se centra en aislar los métodos matemáticos. El objetivo es comprobar que la unidad lógica más pequeña (los métodos matemáticos) funciona correctamente de forma independiente.

        Podría usarse para integrarse posteriormente como una librería en un sistema de información más complejo, como una app movil de calculadora.

2. Revisa las pruebas de la suma y comenta lo que te parezca de interés

       En la línea Calculadora calculadora = new Calculadora(); no es necesario crear el objeto, ya que los métodos de la calculadora están definidos como estáticos. Por tanto, se pueden invocar directamente usando Calculadora.sumar().

       Además, el método sumarPositivosMal() está hecho a propósito para que falle al esperar un 4 en lugar de un 5. Esto sirve para verificar que el sistema de pruebas detecta correctamente los errores.


3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.

        Entradas: a (int), b (int).
        Salida: Resultado int u OperacionNoValidaException

        Dividendo válido: Cualquier número entero.
        Divisor válido: Cualquier número entero distinto de cero.

        Divisor no válido: El número 0.

        Valores límite:
        Límite inferior válido: -1
        Valor crítico (inválido): 0
        Límite superior válido: 1

        Pruebas aleatorias
        
        PA1: a = 4, b = 2
        PA2: a = -1, b = -1


| Caso de Prueba | Clase / Origen | Prefijo | Valores (a, b) | Salida Esperada |
| :--- | :--- | :--- | :--- | :--- |
|CP1| Aleatoria (Positivo / Positivo) | CEdv | 4, 2 | 2 |
|CP2| Límite < 0 (Positivo / Negativo) | CEdv | 3, -1 | -3 |
|CP3| Aleatoria (Negativo / Negativo) | CEdv | -1, -1 | 1 |
|CP4| Clase No Válida (Divisor Cero) | CEdi | 14, 0 | OperacionNoValidaException |
        

```java
    @Test
    @DisplayName("División con divisores válidos")
    void dividirCajaNegraTest() {
        assertAll("División Válida",
                () -> assertEquals(2, Calculadora.dividir(4, 2), "CP1: Aleatoria (Positivo / Positivo)"),
                () -> assertEquals(-3, Calculadora.dividir(3, -1), "CP2: Límite < 0 (Positivo / Negativo)"),
                () -> assertEquals(1, Calculadora.dividir(-1, -1), "CP3: Aleatoria (Negativo / Negativo)")
        );
    }

    @Test
    @DisplayName("División por cero")
    void dividirPorZeroExceptionTest() {
        var ex = assertThrows(OperacionNoValidaException.class, 
                () -> Calculadora.dividir(14, 0), "CP4: Divisor = 0 lanza excepción");
                
        assertEquals(OperacionNoValidaException.MSG, ex.getMessage());
    }```


