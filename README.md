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

### Ejemplo de runnable con lambda

```
//Runnable Traditional example
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        int sum = 0;
        for (int i = 0; i < 10; i++)
            sum += i;
        System.out.println("Traditional: " + sum);
    }
};
new Thread(runnable).start();

//Implement using Lambda
Runnable runnable1 = () -> {
    int sum = 0;
    for (int i = 0; i < 10; i++)
        sum += i;
    System.out.println("Runnable Lambda: " + sum);
};
new Thread(runnable1).start();

//Implement using Thread with lambda
new Thread(() -> {
    int sum = 0;
    for (int i = 0; i < 10; i++)
        sum = sum + i;
    System.out.println("Thread Lambda: " + sum);

}).start();

```

### Ejemplo de Callable con lambda

En este caso nos encontramos con algo muy similar pero usamos el interface Callable. Este interface dispone del método call que es capaz de devolvernos un resultado algo que el método run de un ejecutable no permite.

```java
// Crea un array de 0 a 5000 usando la interfaz InStream y el metodo rangeClosed
public static int[] array = IntStream.rangeClosed(0,5000).toArray();
// Suma los numeros de 0 a 5000, usando un rango
public static int total = IntStream.rangeClosed(0,5000).sum();

public static void main(String[] args) throws InterruptedException, ExecutionException {
    
    // Crea un callable 
    Callable callable1 = () -> {
        int sum=0;
        for (int i=0;i< array.length/2;i++){
            sum = sum + array[i];
        }
        return sum;
    };
    
    // Crea un segundo callable
    Callable callable2 = () -> {
        int sum = 0;
        for (int i=array.length/2; i<array.length;i++){
            sum = sum + array[i];
        }
        return sum;
    };
    
    // Creamos un executor service que ejecutará los callable en un pool
    ExecutorService executorService = Executors.newFixedThreadPool(2);
    List<Callable<Integer>> taskList = Arrays.asList(callable1, callable2);
    
    // Invocamos todos los hilos del pool a la vez
    List<Future<Integer>> results = executorService.invokeAll(taskList);

    int k=0;
    int sum=0;
    for (Future<Integer> result: results){
        sum = sum + result.get();
        System.out.println("Sum of " + ++k + " is: " + result.get());
    }
    System.out.println("Sum from the Callable is: " + sum);
    System.out.println("Correct sum from InStream is: " + total);
    // Cerramos la ejecución del servicio
    executorService.shutdown();
}
```

## Leccion 2 - Interfaces funcionales

Una interfaz funcional es una interfaz que contiene un solo metodo abstracto sin implementar.
Puede contener metodos default y estaticos con implementación, pero solo un método abstracto.

```
// Podemos anotarla como @FunctionalInterface para que el IDE nos verifique que cumple
// con sus cualidades
@FunctionalInterface
public interface IStrategy {
    
    // Método abstracto no implementado
    public String sayHelloTo(String name);
    
    // Método default implementado
    public default String sayHelloWord(){
        return "Hello word";
    }
}
```

**Interfaces funcionales útiles:**
- Consumer
- Supplier
- Function
- Predicate

### Interfaz funcional `Consumer`

- Parte de `java.util.function`
- Representa una funcion que toma un argumento y produce un resultado

Ejemplos:

```
// Consumer con una sola orden
// Toma un solo argumento (x) y produce un resultado
Consumer<String> c = (x) -> System.out.println(x.length() + " the value of x: " + x);
// Con el metodo 'accept' indicamos que ejecute el método
c.accept("Up in the air");

//Consumer with block statement
Consumer<Integer> d = (x) -> {
    System.out.println("x*x = " + x*x);
    System.out.println("x/x = " + x/x);
};
d.accept(10);

```