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
public class IncrementByFiveLambda {
    public static void main(String[] args) {
        // Indicamos los parametros que usa dentro de los parentesis, y los podemos usar en su cuerpo
        // 'x' será el int 'a'
        IncrementByFiveInterface incrementByFiveInterface = (x) -> x + 5;
        System.out.println(incrementByFiveInterface.incrementByFive(2));
    }
}

// Interfaz funcional con más de un parámetro
@FunctionalInterface
public interface ConcatenateInterface {
    //abstract method
    public String sconcat (String a, String b);
}

// Implementacion
public class ConcetenateLambda {
    public static void main(String[] args) {
        // Los strings que se pasan por parámetro serán 'a' y 'b'
        ConcatenateInterface concatenateInterface = (a,b) -> a + " " + b;
        System.out.println(concatenateInterface.sconcat("Hello", "World"));
    }
}

```

### Ejemplo de runnable con lambda

```java
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

## Lección 2 - Interfaces funcionales

Una interfaz funcional es una interfaz que contiene un solo método abstracto sin implementar.
Puede contener métodos default y estáticos con implementación, pero solo un método abstracto.

```java
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

### Interfaces funcionales útiles:
- `Consumer<T>`
- Métodos por referencia
- `Supplier`
- `Function`
- `Predicate`

#### Interfaz funcional `Consumer<T>`

- Parte de `java.util.function`
- Representa una función que toma un argumento y produce un resultado
- Con el método 'accept' indicamos que ejecute la función

Ejemplos:

```java
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

#### Métodos por referencia

Permite pasar a una interfaz funcional una función que se encuentra en nuestro propio programa.
De esta forma le indicaremos qué queremos que procese (en caso por ejemplo de un consumer)

```java
public class Principal {
 
    public static void main(String[] args) {
     
        // Metodo 1: Instanciar consumer y ejecutar su accept
        Consumer<String> consumidor = (x) -> System.out.println(x);
        consumidor.accept("hola");
        
        // Metodo 2: Pasar a metodo que recibe consumer su función y que la procese 
        procesar((x)->System.out.println(x),"hola2");
        
        // METODOS POR REFERENCIA: De esta forma indicamos qué función
        // queremos que procese, donde la notacion Principal::imprimir
        // indica el metodo 'imprimir' de la clase Principal (recordar que
        // un Consumer es un método 
        procesar(Principal::imprimir,"hola3");
    }
 
    public static <T> void procesar(Consumer<T> expresion, T mensaje) {
        expresion.accept(mensaje);
    }
 
    public static void imprimir(String mensaje) {
        System.out.println("---------");
        System.out.println(mensaje);
        System.out.println("---------");
    }
    
    /* LA CONSOLA SACARÁ:
    > hola
    > hola2
    > ---------
    > hola3
    > ---------
    */
}
```

Lo interesante es que si por ejemplo disponemos de otra clase que disponga de un método que reciba un parámetro y no 
devuelva nada podremos usarla también.

En este caso hemos creado la clase Impresora , podemos utilizar su método imprimir como si fuera una referencia a una 
expresión lambda.

```java
public class Impresora {
    // Método void imprimir que recibe un parámetro -> candidato a Consumer<T>
    public void imprimir (String mensaje) {
        System.out.println("imprimiendo impresora");
        System.out.println(mensaje);
        System.out.println("imprimiendo impresora");
    }
}
 
public class Principal {
 
    public static void main(String[] args) {
        // Instanciamos un objeto Impresora y pasamos por referencia su método
        // 'imprimir', que es tipo void
        Impresora i= new Impresora();
        procesar(i::imprimir,"hola4");
    }
     
    public static <T> void procesar(Consumer<T> expresion, T mensaje) {
        expresion.accept(mensaje);
    }
     
    public static void imprimir(String mensaje) {
        System.out.println("---------");
        System.out.println(mensaje);
        System.out.println("---------");
    }
    
    /* LA CONSOLA SACARÁ:
    > imprimiendo impresora
    > hola3
    > imprimiendo impresora
    */
}
```

