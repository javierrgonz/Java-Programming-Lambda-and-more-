# Java-Programming-Lambda-and-more-
Java Programming, Lambda and more (Java 13, 12, 11, 10, 9,8) course

WEB: https://www.udemy.com/course/java-latest-programming-from-zero-java13-java12-java11-java10-java9-j8

## Lección 1 Expresiones Lambda

Las expresiones lambda tienen las siguientes partes:
- Parametros
- Cuerpo
- No tienen tipo de retorno
- No tienen nombre

Se usa para implementar **interfaces funcionales**: Son interfaces con SAM (Simple Abstract Method). 
Puede implementar uno o más métodos default, pero deberá tener forzosamente un único método abstracto.

### Ejemplo de interfaces funcionales sin parametros
```java
// Ejemplo de interfaz funcional - HelloWorldInterface
package com.modernjava.lambda;
public interface HelloWorldInterface {
    //abstract method as it does not provide implementation
    public String sayHelloWorld();
}

// Implemetción tradicional de la interfaz funcional - HelloWorldTraditional 
package com.modernjava.lambda;
public class HelloWorldTraditional implements HelloWorldInterface {
    @Override
    public String sayHelloWorld() {
        return "Hello World";
    }
    public static void main(String[] args) {
        HelloWorldTraditional helloWorldTraditional = new HelloWorldTraditional();
        System.out.println(helloWorldTraditional.sayHelloWorld());
    }
}

// Implementación por lambda - Se define el metodo abstracto al mismo momento de usar la interaz 
package com.modernjava.lambda;
public class HelloWorldLambda {
    public static void main(String[] args) {
        // Iimplementing sayHelloWorld Using Lambda in one line
        HelloWorldInterface helloWorldInterface = () -> "Hello World";
        // La llamada a la interfaz devolvera el metodo definido mediante Lambda         
        System.out.println(helloWorldInterface.sayHelloWorld());
    }
}
```

### Ejemplo de interfaces funcionales con parametros
```java
// Interfaz funcional con un parametro
package com.modernjava.lambda;
@FunctionalInterface
public interface IncrementByFiveInterface {
    //abstract method
    public int incrementByFive(int a);
}

// Impllementación por lambda
package com.modernjava.lambda;
public class IncrementByFiveLambda {
    public static void main(String[] args) {
        // Indicamos los parametros que usa dentro de los parentesis, y los podemos usar en su cuerpo
        // 'x' será el int 'a'
        IncrementByFiveInterface incrementByFiveInterface = (x) -> x + 5;
        System.out.println(incrementByFiveInterface.incrementByFive(2));
    }
}

// Interfaz funcional con más de un parámetro
package com.modernjava.lambda;
@FunctionalInterface
public interface ConcatenateInterface {
    //abstract method
    public String sconcat (String a, String b);
}

// Implementacion
package com.modernjava.lambda;
public class ConcetenateLambda {
    public static void main(String[] args) {
        // Los strings que se pasan por parámetro serán 'a' y 'b'
        ConcatenateInterface concatenateInterface = (a,b) -> a + " " + b;
        System.out.println(concatenateInterface.sconcat("Hello", "World"));
    }
}

```
