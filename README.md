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

### Ejemplo de Expresiones Lambda sin parametros

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

### Ejemplo de Expresiones Lambda con parametros

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

### Ejemplo de runnable con Expresiones Lambda

```java

private class CallableExample {
    
    public static void main(String[] args) {

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

    }
} 
```

### Ejemplo de Callable con Expresiones Lambda

En este caso nos encontramos con algo muy similar pero usamos el interface Callable. Este interface dispone del método call que es capaz de devolvernos un resultado algo que el método run de un ejecutable no permite.

```java

private class CallableExample {
    
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
        }}
```

### Scopes en Expresiones Lambda

- El cuerpo de la expresión tiene el mismo scope que un bloque anidado
- No se puede declarar un parámetro o variable local en la función lambda que tenga el mismo nombre que una 
variable local
- No se puede modificar la variable local dentro de la expresión lambda
- No hay restriccion por nivel de clase o variable instantánea

#### Effectively Final

En lambda podemos usar una variable local pero no se puede modificar la variable aunque no sea declarada
`final`. A esto se llama `effectively Final`.

Por ejemplo:

```java
int k = 10;
List<Instructor> inst = Instructors.getAll();

instructors.forEach(instructor -> {
    System.out.println(instructor + k++); // ERROR al tratar de modificar k
});
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
- [`Consumer<T>`](#consumer)
  - [Consumers especializados `IntConsumer, LongConsumer, DoubleConsumer`](#consumer_especializados)
- [`BiConsumer<T>`](#biconsumer)
- [`Predicate<T>`](#predicate)
  - [Predicates especializados `IntPredicate, LongPredicate, DoublePredicate`](#predicate_especializados)
  - [Predicates y biconsumers](#predicates-y-biconsumer)
- [`BiPredicate<T>`](#bipredicate)
- [`Function`](#function)
- [`Bifunction`](#bifunction)
- [`Unary operator`](#unary_operator)
- [`Binary operator`](#binary_operator)
- [`Supplier`](#supplier)
- [Métodos por referencia](#metodos_por_referencia)
- [Constructores por referencia](#constructores_por_referencia)

Un resumen general seria

|  Nombre               | Argumentos                        | Respuesta                                         | Método de ejecución                   | 
|-----------------------|-----------------------------------|---------------------------------------------------|---------------------------------------|
|  **Consumer**         | Un argumento de cualquier tipo    | No                                                | `.accept(Object a)`                   |
|  IntConsumer          | Un Integer                        | No                                                | `.accept(Integer a)`                  |
|  LongConsumer         | Un Long                           | No                                                | `.accept(Long a)`                     |
|  DoubleConsumer       | Un Double                         | No                                                | `.accept(Double a)`                   |
|  **Biconsumer**       | Dos argumentos de cualquier tipo  | No                                                | `.accept(Object a, Object b)`         |
|  **Predicate**        | Un argumento de cualquier tipo    | Booleano (`true` / `false`)                       | `.test(Object a)`                     |
|  IntPredicate         | Un Integer                        | Booleano (`true` / `false`)                       | `.test(Integer a)`                    |
|  LongPredicate        | Un Long                           | Booleano (`true` / `false`)                       | `.test(Long a)`                       |
|  DoublePredicate      | Un Double                         | Booleano (`true` / `false`)                       | `.test(Double a)`                     |
|  **BiPredicate**      | Dos argumentos de cualquier tipo  | Booleano (`true` / `false`)                       | `.test(Object a, Object b)`           |
|  **Function**         | Un argumento de cualquier tipo    | Un resultado de cualquier tipo                    | `.apply(Object a)`                    |
|  **Bifunction**       | Dos argumentos de cualquier tipo  | Un resultado de cualquier tipo                    | `.apply(Object a, Object b)`          |
|  **UnaryOperator**    | Un argumento de cualquier tipo    | Un resultado del mismo tipo que el argumento      | `.apply(Object a, Object b)`          |
|  IntUnaryOperator     | Un Integer                        | Un Integer                                        | `.apply(Integer a)`                   |
|  LongUnaryOperator    | Un Long                           | Un Long                                           | `.apply(Long a)`                      |    
|  DoubleUnaryOperator  | Un Double                         | Un Double                                         | `.apply(Double a)`                    |
|  **BinaryOperator**   | Dos argumentos del mismo tipo     | Un resultado del mismo tipo que los argumentos    | `.apply(Object a, Object b)`          |
|  IntBinaryOperator    | Dos Integer                       | Un Integer                                        | `.apply(Integer a, Integer b)`        |
|  LongBinaryOperator   | Dos Long                          | Un Long                                           | `.apply(Long a, Long b)`              |
|  DoubleBinaryOperator | Dos Double                        | Un Double                                         | `.apply(Double a, Double b)`          |
|  **Supplier**         | Ninguno                           | Un resultado de cualquier tipo                    | El definido en el cuerpo del lambda   |

#### Interfaz funcional `Consumer<T>`<a name="consumer"></a>

- Parte de `java.util.function`
- Representa una función que toma **un** argumento y no devuelve un resultado
- Con el método 'accept' indicamos que ejecute la función

```java
private class ConsumerExample {
    public static void main(String[] args) {
    
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

    }
}
```

##### Consumidores especializados IntConsumer, LongConsumer, DoubleConsumer<a name="consumer_especializados"></a>

Java dispone de consumidores especializados, que determinan el tipo de argumento que se le puede pasar en el método
que crea el consumidor

```java
private class SpecialConsumerExample {
    public static void main(String[] args) {

        IntConsumer intConsumer = (a) -> System.out.println(a*10);
        intConsumer.accept(10);
        
        LongConsumer longConsumer = (a) -> System.out.println(a * 10L);
        longConsumer.accept(10L);
        
        DoubleConsumer doubleConsumer = (a) -> System.out.println(a * 10);
        doubleConsumer.accept(10.50);

    }
}
```

#### BiConsumer<a name="biconsumer"></a>

- Parte de `java.util.function`
- Representa una función que toma **dos** argumentos y no devuelve un resultado
- Con el método 'accept' indicamos que ejecute la función

```java
private class BiConsumerExample {
    public static void main(String[] args) {
        
        // Usa dos parametros
        BiConsumer<Integer,Integer> biConsumer = (x,y) -> System.out.println("x: " + x + " y: " + y);
        biConsumer.accept(2,4);

    }
}
```

#### Predicados<a name="predicate"></a>

Son funciones con un solo argumento que devuelven `true` o `false` a traves de un metodo `test`
El predicado dispone de metodos que permiten incluir más condiciones, o realizar negaciones

```java
public class PredicateExample {
    public static void main(String[] args) {
 
        // BASICO
        // if number is >10 return true other false
        Predicate<Integer> p1 = (i) -> i>10;
        System.out.println(p1.test(100));
    
        // COMBINACION DE PREDICADOS
        // i>10 && number is even number (i%2 ==0)
        Predicate<Integer> p2 = (i) -> i%2==0;
        System.out.println(p1.and(p2).test(20));
    
        // i>10 || number is even number (i%2==0)
        System.out.println(p1.or(p2).test(4));
    
        // MANIPULACION DEL PREDICADO CON NEGACIONES
        //i>10 && i%2 !=0
        System.out.println(p1.and(p2.negate()).test(33));
    }
}
```

Un ejemplo de uso: con una clase `Instructor`, podemos usar los predicados para realizar un filtrado
por condiciones

```java
public class PredicateExample2 {
    public static void main(String[] args) {

        //all instructor who teaches online
        Predicate<Instructor> p1 = (i) -> i.isOnlineCourses()==true;
        //instructor experience is >10 years
        Predicate<Instructor> p2 = (i) -> i.getYearsOfExperience() >10;

        // Imprime solo los instructores que cumplan el predicado 1
        List<Instructor> instructors = Instructors.getAll();
        instructors.forEach(instructor -> {
            if (p1.test(instructor)){
                System.out.println(instructor);
            }
        });

        // Imprime solo los instructores que cumplan ambos predicados
        System.out.println("---------------------");
        instructors.forEach(instructor ->  {
            if(p1.and(p2).test(instructor)){
                System.out.println(instructor);
            }
        });

    }
}
```

##### Predicados especializados: IntPredicate, DoublePredicate, LongPredicate<a name="predicate_especializados"></a>

Existen predicados especializados para los tipos Int, Double o Long, que condiciona el tipo de
parametro que se puede pasar al método booleano que define.


```java
public class PredicateExample3 {
    public static void main(String[] args) {
        
        IntPredicate p1 = (i) -> i>100;
        System.out.println(p1.test(100));

        LongPredicate p2 = (i) -> i>100L;
        System.out.println(p2.test(1111111111111111111L));

        DoublePredicate p3 = (i) -> i<100.25;
        DoublePredicate p4 = (i) -> i>100.10;
        System.out.println(p3.and(p4).test(100.15));

    }
}

```

##### Predicados y biconsumer<a name="predicates-y-biconsumer"></a>

Un ejemplo de implementación de predicados y biconsumers: 

```java
public class PredicateAndBiConsumerExample {
    public static void main(String[] args) {

        List<Instructor> instructors = Instructors.getAll();

        // Definimos los predicados como las condiciones para filtrar los instructores
        Predicate<Instructor> p1 = (i) -> i.isOnlineCourses() == true;
        Predicate<Instructor> p2 = (i) -> i.getYearsOfExperience() > 10;

        // El biconsumer recibirá dos parámetros para imprimir una serie de valores
        BiConsumer<String, List<String>> biConsumer = (name, courses) ->
                System.out.println("name is: " + name + " courses : " + courses);
    
        // Finalmente, recorremos el listado de instructores, y en caso de que se cumpla
        // las condiciones de los predicados, usa el biconsumer para imprimir los valores
        // del instructor
        instructors.forEach(instructor -> {
            if(p1.and(p2).test(instructor))
                biConsumer.accept(instructor.getName(), instructor.getCourses());
        });
    }
}
```

#### Bipredicate<a name="bipredicate"></a>

De forma similar al Biconsumer, un Bipredicate se trata de un método que acepta dos parámetros y devuelve
un booleano `true` o `false` como respuesta.

```java
public class BiPredicateExample {
    public static void main(String[] args) {
        
        List<Instructor> instructors = Instructors.getAll();
        
        // BIPREDICADO
        // En este caso, acepta un booleano y un integer, y la condicion es una
        // combinación de comprobaciones sobre ambos parámetros
        BiPredicate<Boolean, Integer> p3 = 
            (online, experience) -> online == true && experience > 10;

        // Definimos un BICONSUMER que imprime los nombres y cursos
        BiConsumer<String, List<String>> biConsumer = (name, courses) ->
                System.out.println("name is: " + name + " courses : " + courses);
    
        // Recorremos el listado de instructores, y si cumplen la condicion del
        // bipredicate, ejecutan el biconsumer 
        instructors.forEach(instructor -> {
            if(p3.test(instructor.isOnlineCourses(), instructor.getYearsOfExperience()))
                biConsumer.accept(instructor.getName(), instructor.getCourses());
        });
    }
}

```

#### Function<a name="function"></a>

Parte de java.util.function. Representa una función que usa un argumento y devuelve un resultado.
Dispone de un método `apply` que ejecuta la función.

Dispone de dos metodos auxiliares para la composiciónd de funciones complejas:
- `andThen`: crea una función nueva que combina dos funciones, ejecutando primero la que llama al método andThen y 
después la segunda. Por ejemplo, `functionA.andThen(functionB)` ejecuta primero la `functionA` y después la `functionB`
- `compose`: actua al revés, ejecutará primero la que se pasa por parámetro. En el ejemplo anterior, ejecuta la 
`functionB` después de la `functionA` 

```java
public class FunctionExample {
    public static void main(String[] args) {

        // FUNCTION
        // En este caso, recoge un Integer 'n' y devuelve un Double
        //        in       out
        //         |        |
        Function<Integer, Double> sqrt = n -> Math.sqrt(n);

        // Ejecutamos la función con el método `apply`
        System.out.println("Square root of 64: " + sqrt.apply(64));
        System.out.println("Square root of 81: " + sqrt.apply(81));

        // FUNCTION
        // Aquí recoge un String y devuelve un String en minusculas
        //        in      out
        //         |       |
        Function<String,String> lowercaseFunction = s1 -> s1.toLowerCase();
        System.out.println(lowercaseFunction.apply("PROGRAMMING"));
        
        // COMBINACIÓN DE FUNCTIONS
        // Podemos combinar funciones usando los métodos de el objeto `Function`.
        // Por ejemplo disponemos del metodo `andThen` que e        
        Function<String, String> concatFunction = (s) -> s.concat(" In Java");
        System.out.println(lowercaseFunction.andThen(concatFunction).apply("PROGRAMMING"));
        System.out.println(lowercaseFunction.compose(concatFunction).apply("PROGRAMMING"));

    }
}
```

Un ejemplo de una `function` compleja:

```java
public class FunctionExample2 {
    public static void main(String[] args) {

        // Predicate will return true if instructor has online courses
        Predicate<Instructor> p1 = (i) -> i.isOnlineCourses()==true;
    
        // Esta function recibe un listado de instructors y devuelve un mapa de los
        // que cumplen la condición del predicado definida arriba
        //               in                  out
        //                |                   |
        Function<List<Instructor>, Map<String,Integer>> mapFunction = 
            // Con el parámetro de entrada realizamos una operación
            (instructors -> {
                Map<String,Integer> map = new HashMap<>();
                instructors.forEach(instructor -> {
                    if(p1.test(instructor)) {
                        map.put(instructor.getName(), instructor.getYearsOfExperience());
                    }
                });
                return map;
        });
    
        // Ejecución de la function con apply
        System.out.println(mapFunction.apply(Instructors.getAll()));
    }
}
```

#### Bifunction<a name="bifunction"></a>

En este caso, la función recibe dos argumentos y devuelve una respuesta

```java
public class BiFunctionExample {
    public static void main(String[] args) {
    
        Predicate<Instructor> p1 = (i) -> i.isOnlineCourses() == true;
    
        // BIFUNCTION
        // Recibe dos parámetros y devuelve un resultado después de hacer una operación
        //              in                  in                  out 
        //               |                   |                   |
        BiFunction<List<Instructor>, Predicate<Instructor>, Map<String,Integer>> mapBiFunction =
            // Con los dos parámetros realizamos una compribación y rellenamos el mapa de salida
            ((instructors, instructorPredicate) -> {
                Map<String, Integer> map = new HashMap<>();
                instructors.forEach(instructor -> {
                    if(instructorPredicate.test(instructor)){
                        map.put(instructor.getName(), instructor.getYearsOfExperience());
                    }
                });
                return map;
            });
        System.out.println(mapBiFunction.apply(Instructors.getAll(), p1));
    }
}
```

#### Unary operator<a name="unary_operator"></a>

El `unary operator` extiende de Function, y es una función que recibe un argumento y devuelve un resultado del mismo
tipo del parámetro de entrada.
Suele usarse para encadenar operaciones.

Existen distintos tipos especializados: IntUnaryOperator, LongUnaryOperator, DoubleUnaryOperator

```java
public class UnaryOperatorExample {

    public static void main(String[] args) {

        // UnaryOperator con un tipo Integer. Solo hay que informar del tipo de entrada
        UnaryOperator<Integer> unary = i -> i * 10;
        System.out.println(unary.apply(100));

        // Function equivalente al UnaryOperation anterior. 
        // Informa del tipo de entrada in y out
        Function<Integer, Integer> function = i -> i*10;
        System.out.println(function.apply(100));

        // UnaryOperation especializados: IntUnaryOperator
        // No hace falta informar del tipo de entrada ni de salida
        IntUnaryOperator intUnaryOperator = i -> i *10;
        System.out.println(intUnaryOperator.applyAsInt(100));

        // UnaryOperation especializados: LongUnaryOperator
        LongUnaryOperator longUnaryOperator = i -> i*10;
        System.out.println(longUnaryOperator.applyAsLong(10000000000000000l));

        // UnaryOperation especializados: DoubleUnaryOperator
        DoubleUnaryOperator doubleUnaryOperator = i -> i*10;
        System.out.println(doubleUnaryOperator.applyAsDouble(2000000.20000000));
    }
}
```

Un ejemplo de encadenado de UnaryOperators:

```java
public class Java8UnaryOperator3 {

    public static void main(String[] args) {

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Definimos los UnaryOperators
        UnaryOperator<Integer> uo = x -> x * 2;
        UnaryOperator<Integer> uo2 = x -> x + 1;

        // Para cada elemento de la lista, aplicamos primero el uo y luego el uo2  
        for (T t : list) {
            result.add(uo.andThen(uo2).apply(t));
        }
    }
}
```

#### BinaryOperator<a name="binary_operator"></a>

Es una interfaz funcional que toma dos parametros y devuelve un único valor. 
**Los parametros de entrada y la salida deben ser del mismo tipo**
Se usa mucho para opeaciones matematicas que devuelven parámetros del mismo tipo que la entrada

Dispone de especialidades **IntBinaryOperator**, **LongBinaryOperator** y **DoubleBinaryOperator**

```java
public class BinaryOperatorExample {
    public static void main(String[] args) {

        // Define BinaryOperator con un Integer. En este caso toma dos Integer
        // a,b y devuelve la suma de ambos
        BinaryOperator<Integer> binaryOperator = (a,b) -> a + b;
        System.out.println(binaryOperator.apply(2,4));

        // Definimos un comparator que compare a con b y devuelva uno de ellos segun
        // una condicion establecida mediante un BinaryOperator
        Comparator<Integer> comparator = (a,b) -> a.compareTo(b);
        // Definimos un binaryoperator integer predefinido por java, que coja el 
        // comparator y le establezca la condición 'maxBy', es decir, devuelveme el
        // maximo de estos 
        BinaryOperator<Integer> maxBi = BinaryOperator.maxBy(comparator);
        // Ejecutamos el binaryOperator
        System.out.println(maxBi.apply(7,8));

        BinaryOperator<Integer> minBy = BinaryOperator.minBy(comparator);
        System.out.println(minBy.apply(7,8));

        IntBinaryOperator intBi = (a,b) -> a*b;
        System.out.println(intBi.applyAsInt(2,4));

        LongBinaryOperator longBi = (a,b) -> a*b;
        System.out.println(longBi.applyAsLong(20000000l, 22222222222222222l));

        DoubleBinaryOperator doubleBi = (a,b) -> a*b;
        System.out.println(doubleBi.applyAsDouble(2222.22222, 22222222222222.22222));
    }
}
```

#### Supplier<a name="supplier"></a>

Intefaz funcional que proporciona un valor de cualquier tipo. 
Podria entenderse como una factoría de valores de un tipo concreto.

```java
public class SupplierExample {
    public static void main(String[] args) {
    
        // Método que devuelve un integer aleatorio
        Supplier<Integer> supplier = () -> (int) (Math.random() * 1000);
        System.out.println(supplier.get());
        System.out.println(supplier.get());
    }
}
```

#### Métodos por referencia<a name="metodos_por_referencia"></a>

Es un atajo en notación lambda que permite llamar a un método
Existen 3 tipos:

- `Class::staticMethod` - Referencia a un método estatico
- `object::instanceMthod` - Referencia a un método de instancia
- `Class::new` - Referencia a un constructor

No se puede convertir:
- `(a) -> System.out.println(a*10)` 

```java
public class MethodReferenceExample {
    public static void main(String[] args) {

        // Ejemplo con predicate
        Predicate<Instructor> p1 = instructor -> instructor.isOnlineCourses();
        Predicate<Instructor> p2 = Instructor::isOnlineCourses;

        // Ejemplo con funciones
        Function<Integer, Double> sqrt= a -> Math.sqrt(a);
        Function<Integer, Double> sqrt1 = Math::sqrt;

        Function<String, String> lowercaseFunction = s -> s.toLowerCase();
        Function<String, String> lowercaseFunction1 = String::toLowerCase;
   }
}
```

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

#### Constructores por referencia<a name="constructores_por_referencia"></a>

Solo puede usarse en el contexto de una `interfaz funcional`, es decir, no podemos crear 
una instancia de una clase de esta forma:

    `Instructor inst = Instructor::new`

No obstante, podemos instanciar un objeto como este, pero la interfaz debe ser una interfaz
funcional:

    `InstructorFactory insFac = Instructor::new`

Para usar la referencia por constructor, debes definir una interfaz funcional con un metodo
abstracto cuyo tipo devuelto es el mismo que el del objeto que queremos usar el constructor
por referencia

```java
public class ConstructorReferenceExample {
    public static void main(String[] args) {
        
        // Creamos la factoria pasando el metodo constructor por refrencia
        InstructorFactory instructorFactory = Instructor::new;

        // Instanciamos el objeto con la factoria
        Instructor instructor = instructorFactory.getInstructor("Mike", 10, "Software Developer"
        , "M", true, Arrays.asList("Java Programming", "C++ Programming", "Python Programming"));

        System.out.println(instructor);
    }
}
```

El compilador elige por iferenencia el constructor que tenga un solo parámetro String porque es el único que aplica.
Podemos hacer lo mismo con un constructor con más parámetros. 

```java
// Clase instructor con un constructor con multiples parámetros
public class Instructor {
    String name;
    int yearsOfExperience;
    String title;
    String gender;
    boolean onlineCourses;
    List<String> courses;

    public Instructor(String name, int yearsOfExperience, String title, String gender, boolean onlineCourses, List<String> courses) {
        this.name = name;
        this.yearsOfExperience = yearsOfExperience;
        this.title = title;
        this.gender = gender;
        this.onlineCourses = onlineCourses;
        this.courses = courses;
    }
}

// Interface InstructorFactory con metodo getInstructor
public interface InstructorFactory {
    Instructor getInstructor(String name, int yearsOfExperience, String title,
                             String gender, boolean onlineCourse, List<String> courses);
}

// Ejemplo de uso de constructor por referencia
public class ConstructorReferenceExample {
    public static void main(String[] args) {
        // Usamos la llamada por referencia a su constructor "new" para el factory
        InstructorFactory instructorFactory = Instructor::new;

        // El factory usará el constructor con el numero de parametros existente para obtener una instancia 
        Instructor instructor = instructorFactory.getInstructor("Mike", 10, "Software Developer"
        , "M", true, Arrays.asList("Java Programming", "C++ Programming", "Python Programming"));
    }
}
```

## Lección 3 - Stream

Un Stream es una secuencia de objetos que soporta varios metodos que pueden ser enlazados
para producir el resultado deseado. Permite procesar colecciones.

Permite filtrar y construir mapas a partir de colecciones.

### Características

- Un stream no es una estructura de datos. Toma los datos de colecciones, arrays o canales in/out
- Stream no cambia la estructura de datos de la que se construye, solo devuelve los resultados tras
la operación sobre la que se construye
- Cada operación intermedia se realiza de forma lazy, y devuelve un stream que puede ser enlazada
para operaciones posteriores
- Se pueden construir operaciones en paralelo sin tener que usar hilos expresamente
- Se diferencia de las colecciones en lo siguiente:

| Collections | Streams |
|---|---|
|Almacena y agrupa informacion| No es una estructura de datos. Coge los de una coleccion y opera con ellos|
|Puedes añadir y borrar elementos|No se pueden añadir ni borrar elementos|
|Se debe iterar externamente|Se iteran internamente|
|Construccion eagerly|Construccion lazy|
|Pueden ser recorridas muchas veces|Solo se recorren una vez|

### Creación de streams

- **of**: Usaremos `Stream.of()` para crear un stream de tipos de datos similares
    ```java
    Arrays.aList(1,2,3).stream();
    // Esto es similar a: 
    Stream<Integer> stream = Stream.of(1,2,3);
    Stream<Integer> stream = Stream.of(new Integer[]{1,2,3});
    ```
- **iterate**: Genera un stream secuencial infinito ORDENADO producido por la aplicación de un UnaryOperator
que será la el elemento inicial de la iteración
    ```java
    // Genera un stream de numeros pares
    Stream.iterate(0, i -> i + 2);
    ```
- **generate**: Genera un stream secuencial infinito DESORDENADO donde cada elemento es generado por el Suplier usado
como parametro
    ```java
    // Generación de un stream de numeros random
    Stream.generate(new Random()::nextInt);
    ```

### Operaciones intermedias en streams

- **Map**: Devuelve un stream consistente en los resultados de aplicar la función pasada por 
parametro sobre los elementos del stream
    ```java
    List numbers = Arrays.asList(2,3,4,5,6)
    // Map calculará el cuadrado de cada numero de la lista que construye el stream
    List square = numbers.stream().map(x -> x * x).collect(Collectors.toList());
    ```
- **distinct()**: filtra o recolecta todos los elementos distintos de un string.
- **count()**: devuelve el numero de elementos en el stream
    ```java
    Long count = Instructors.getAll().stream()
                 .map(Instructor::getCourses)
                 .flatMap(List::stream)
                 .distinct()
                 .count();  
    ```
- **anyMatch**: Similar al filtro. Analiza cada objeto del stream y devuelve true si encuentra uno que 
cumpla el filtro. **No recorre todo el stream**, si encuentra un objeto que cumpla la condición, devuelve true
    ```java
    Boolean existePrecioNeegativo = precios.stream().anyMatch(precio -> precio.intValue() < 0);
    ```
- **allMatch**: devuelve todos los elementos que cumplan el predicado pasado por parámetro
- **noneMatch**: devuelve todos los elementos que NO cumplan con el predicado pasado por parámetro
    ```java
    boolean match = Instructors.getAll().stream()
                    .map(Instructor::getCourses)
                    .flatMap(List::stream)
                    .noneMatch(s -> s.startsWith("J"));
    ```
- **findFist()**: Devuelve un `Optional` conteniendo el primer elemento del stream o un optional
vacio si ningun elemento lo cumple
    ```java
    Optional<Instructor> instructorOptional = Instructors.getAll().stream().findFirst();
    if (instructorOptional.isPresent())
        System.out.println(instructorOptional.get());
    ```
- **findAny()**: Otro filtro. En este caso indica que si encuentra alguno devuelva un `Optional`.
Combinandolo con el método `isPresent()` del Optional, podemos filtrar. En este caso **SI se recorre
todo el stream**, no como en `anyMatch`
    ```java
    public boolean detectarErrorFindAny() {
       return this.precios.stream().filter(precio -> precio.intValue() < 0)
                                   .findAny()
                                   .isPresent();
    }  
    ```
- **Sorted**: Ordena el stream basandose en un Comparator
    ```java
     List names = Arrays.asList("Ana", "Luis", "Paco", "Julia");
     // Ordena alfabeticamente
     List namesByJ = names.stream().sort().collect(Collectors.toList());
     ```
- **PararellStreams**: Permite ejecutar las operaciones del stream en hilos en paralelo, para que
java lance un conjunto de hilos para realizar la tarea:
    ```java
    int total=lista.parallel().map(Principal::duplicar).sum();
    ```
- **Map**: Permite convertir un stream de X en un stream de Y. **No confundir con Collectors.toMap**
    ```java
    // Convertimos un listado de Instructors en un set de Strings con sus nombres
    // en mayúsculas usando map
    Set<String> instructorNames = Instructors
                                  .getAll()
                                  .stream()
                                  .map(Instructor::getName)
                                  .map(String::toUpperCase)
                                  .collect(Collectors.toSet());
    ```
- **FlatMap**: Combinacion de un mapa y una operación de aplanado. Devuelve un flujo que 
    consta de los resultados de reemplazar cada elemento de este flujo con el contenido de un flujo mapeado producido 
    al aplicar la función de mapeo proporcionada a cada elemento.
    Por ejemplo, en este caso, convierte un Stream<List<String>> a un Stream<Object> para simplificar
    el stream inicial
    ```java
    // Obtiene un listado de Strings con los cursos 
    // Con la orden .map(Instructor::getCourses) obtenemos un Stream<List<String>>
    // Después con .flatMap(List::stream) obtenemos un Stream<Object>
    Set<String> instructorsCourses = Instructors.getAll().stream()
                                     .map(Instructor::getCourses)     // Stream<List<String>>
                                     .flatMap(List::stream)           // Stream<Object>           
                                     .collect(Collectors.toSet());  
    ```
- **Filter**: Filtra los resultados basados en el predicado pasado al filtro. Es una operacion `lazy`, que significa que realmente no se está realizando ningún filtrado en 
el elemento, sino que en paralelo se está creando un nuevo stream que contiene los elementos 
   del stream inicial que cumplen con el predicado
   ```java
   List names = Arrays.asList("Ana", "Luis", "Paco", "Julia");
   // Filter filtrará los nombres que empiecen por J
   List namesByJ = names.stream().filter(n -> n.startswith("J")).collect(Collectors.toList());
   ```
- **limit(long n)**: Devuelve un stream de tamaño no superior al long pasado por parametro
    ```java
    List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8);
    List limit5numbers = numbers.stream().limit(5).collect(Collectors.toList());
    ```
- **skip(long n)**: Devuelve un stream obviando los primeros `n` elementos
    ```java
    List skip5numbers = numbers.stream().skip(5).collect(Collectors.toList());
    ```

#### Encadenado de operaciones intermedias

Podemos encadenar operaciones intermedias, como por ejemplo aplicar varios filtros seguidos

```java
public class StreamExample {
    public static void main(String[] args) {
        //creating a map of names and course of instructors who teaches
        //online have more than 10 years of experience

        Predicate<Instructor> p1 = (i) -> i.isOnlineCourses();
        Predicate<Instructor> p2 = (i) -> i.getYearsOfExperience()>10;

        List<Instructor> list = Instructors.getAll();
        list.stream().filter(p1).filter(p2);

        Map<String, List<String>> map = list.stream()
                                .filter(p1)
                                .filter(p2)
                                .peek(s-> System.out.println(s))
                                .collect(Collectors.toMap(Instructor::getName, Instructor::getCourses));

        //System.out.println(map);

    }
}
```

### Operaciones finales sobre streams

- **Collect**: Se usa para devolver el resultado de las operaciones realizadas en el stream. Permite configurar que tipo de 
coleccion queremos devolver, mediante la intefaz `Collectors`
    ```java
    List names = Arrays.asList("Ana", "Luis", "Paco", "Julia");
    // Collect recoge los objetos del stream en este caso a una lista
    List namesByJ = names.stream().sort().collect(Collectors.toList());
    ```
- **forEach**: Itera sobre el stream
    ```java
    List names = Arrays.asList("Ana", "Luis", "Paco", "Julia");
    // Iteramos con forEach
    List namesByJ = names.stream().sorted().forEach(y -> System.out.println(y));
    ```
- **reduce**: Realiza un proceso repetido combinando todos los elementos del stream. Obtiene
todos los elementos y los combina en un solo resultado sencillo por la repetición de operaciones
combinadas como suma, multiplicación y división de elementos. 
Tiene dos partes:
  - La ***identidad***: Es el valor inicial de la operación de reducción, y el valor por defecto del 
  resultado cuando el stream esta vacio
  - La expresión lambda (`BinaryOperator`) es el ***acumulador***, que realiza la operacion sobre los objetos del stream
Tiene dos métodos, y según el que se use puede usar uno o los dos parámetros:
  - `T reduce(identidad, acumulador);`
  - `Optional reduce(acumulador)` 
    ```java
    // Reduce con identidad = 0 y acumulador (a , b) -> a + b que suma los objetos
    List<Integer> numbers = Arrays.asList(1,2,3,4);
    int results = numbers.stream().reduce(0,(a,b) -> a +b);  // 1+2+3+4 = 10
    int results1 = numbers.stream().reduce(1,(a,b) -> a* b); // 2*3*4 = 24

    // Reducer con Optional
    Optional result2 = numbers.stream().reduce((a, b) -> a + b);
    System.out.println("--------");
    if(result2.isPresent())                 // El optional puede contener un objeto o no
        System.out.println(result2.get());
 
    ```
- **max**: Obtiene el máximo de los valores del stream, segun el `Comparator` pasado por parámetro.
Devuelve un `Optional`
    ```java
    List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8);
    Optional result = numbers.stream().max(Integer::compareTo);
    ```
    Esto podría implementarse con un `reduce` y un ternario:
    ```java
    List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8);
    int result2 = numbers.stream().reduce(0,(a,b)-> a>b?a:b);
    Optional result3 = numbers.stream().reduce((a,b)->a>b?a:b);
    ```
- **min**: Similar al anterior, pero obtiene el minimo:
    ```java
    List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8);
    Optional result = numbers.stream().min(Integer::compareTo);
    ```
    De igual forma se puede realizar con un reduce y un ternario:
    ```java
    List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8);
    int result1 = numbers.stream().reduce(0,(a,b) -> a<b?a:b);
    Optional result2 = numbers.stream().reduce((a,b) -> a<b?a:b);
    ```

#### Ejemplo combinando map + filter + reduce

```java
public class StreamMapFilterReduceExample {
    public static void main(String[] args) {
        //total years of experience b/w instructors
        int result = Instructors.getAll().stream()
                       .filter(Instructor::isOnlineCourses)     // Obtiene los que sean true
                       .map(Instructor::getYearsOfExperience)   // Recoge los años de experiencia
                       .reduce(0,Integer::sum);                 // Los suma todos 
    }
}
```

#### Ordenaciones customizadas con `Comparator` y `sorted`

Podemos usar la interfaz `Comparator` para crear comparaciones customizadas.
La interfaz dispone de un metodo `comparing` al que debemos pasar el parámetro por el que
queremos comparar.
Además permite encadenar opciones posteriores, como por ejemplo `.reversed()` si queremos que el
orden sea el inverso, o `thenComparing(...` si queremos realizar más comparaciones
Un ejemplo para obtener una serie de nombres ordenados alfabeticamente seria `.sorted(Comparator.comparing(Instructor::getName))`

```java
public class StreamComparatorExample {
    public static void main(String[] args) {
        //retuning all instructors sorted by their name
        List<Instructor> list = Instructors.getAll().stream()
                                .sorted(Comparator.comparing(Instructor::getName).reversed())
                                .collect(Collectors.toList());

        list.forEach(System.out::println);

    }
}
```

### Numeric Streams

Existen tres tipos de Streams numericos: **IntStream**, **LongStream**, **DoubleStream**

#### IntStream

- **Generación**
  ```java
  IntStream numbers = IntStream.of(1,2,3,4,5); // 1,2,3,4,5  
  IntStream numbers = InsSteam.iterate(0, i -> i + 2).limit(5); // 0,2,4,6,8
  IntStream numbers = InsSteam.generate(() ->
    ThreadLocalRandom.current().nextInt(10)).limit(5); // 5 numeros random
  IntStream numbers = InsSteam.range(1,5); // 1,2,3,4
  IntStream numbers = InsSteam.rangeClosed(1,5); // 1,2,3,4,5
  ```
- **LongStream**
  ```java
  LongStream numbers = LongStream.of(1,2,3,4,5); // 1,2,3,4,5  
  LongStream numbers = LongStream.iterate(0, i -> i + 2).limit(5); // 0,2,4,6,8
  LongStream numbers = LongStream.generate(() ->
    ThreadLocalRandom.current().nextInt(10)).limit(5); // 5 numeros random
  LongStream numbers = LongStream.range(1,5); // 1,2,3,4
  LongStream numbers = LongStream.rangeClosed(1,5); // 1,2,3,4,5  
  ```
- **DoubleStream**
  ```java
  DoubleStream numbers = DoubleStream.of(1.2,2.2,3.3,4.3,5.5); // 1.2,2.2,3.3,4.3,5.5  
  DoubleStream numbers = DoubleStream.iterate(0, i -> i + 2).limit(5); // 0.0,2.0,4.0,6.0,8.0
  DoubleStream numbers = DoubleStream.generate(() ->
    ThreadLocalRandom.current().nextDouble(10.0)).limit(5); // 5 numeros double  random
  DoubleStream numbers = DoubleStream.range(1,5).asDoubleStream(10.0); // 1.0,2.0,3.0,4.0
  DoubleStream numbers = DoubleStream.rangeClosed(1,5).asDoubleStream(10.0); // 1.0,2.0,3.0,4.0,5.0  
  ```

#### Funciones agregadas de NumericStreams

- **sum()**: Devuelve la suma de los elementos en el stream
- **max()**: Devuelve el elemento máximo del stream
- **min()**: Devuelve el elemento mínimo del stream
- **average()**: Debuelve la media de los elementos del stream

#### Boxing / Unboxing

**Boxing**: Convertir un primitivo en un objeto de clase envolvente
```java
// Creamos un stream de int primitivos
IntStream numStream = IntStream.rangeClosed(0,5000); 
// con boxed() devolvemos cada elemento primitivo del stream como el wrapper Integer 
List<Integer> numbers = numStream.boxed().collect(Collectors.toList());
```
**Unboxing**: Convertir un wrapper en un primitivo
```
// Con mapToInt(Integer::intValue) mapeamos cada wrapper a su clase primitiva
IntStream numStream = IntStream.rangeClosed(0,5000); 
int sum1 = numbers.stream().mapToInt(Integer::intValue).sum();
``` 

#### mapToObj, mapToLong, mapToDouble

**mapToObj**: En un Numeric Stream, devuelve un stream de objetos
```java
IntStream.mapToObj(a --> Integer.toBinaryString(a));
```
**mapToLong**: En un Numeric Stream, devuelve un stream de Longs
```java
IntStream.mapToLong(num --> (long) num);
```
**mapToDouble**: En un Numeric Stream, devuelve un stream de Doubles
```java
LongStream.mapToDouble(num --> (double) num);
```

### Collectors

- **joining()**
  - **joining()** concatena los elementos de entrada en una cadena, en el orden en que lo encuentra
  ```java
  Stream.of("E", "F", "G").collect(Collectors.joining()); // EFG
  ```
  - **joining(CharSequence delimiter)** concatena los elementos de entrada en una cadena, en el orden en que lo encuentra 
separados por el delimitador
  ```java
  Stream.of("E", "F", "G").collect(Collectors.joining(",")); // E,F,G
  ```
  - **joining(CharSequence delimiter, CharSequence prefix, CharSequence suffix)** concatena los elementos de entrada en una cadena, en el orden en que lo encuentra 
separados por el delimitador con el prefijo y sufijo indicado
  ```java
  Stream.of("E", "F", "G").collect(Collectors.joining(",","{","}")); // {E,F,G,Z}
  ```

- **counting()**: cuenta el numero de elementos en el stream
  ```java
  Stream.of(1,2,3,4,5,6).collect(Collectors.counting());
  Stream.of(1,2,3,4,5,6).count();
  // Util en operaciones de degradación
  grouping(String::length, counting());
  ```

- **mapping()**: coge una función y otro collector y crea un nuevo collector que aplica la funcion y recoge el resultado
usando el collector pasado por parámetro
  ```java
  Collectors.mapping(Instructor::getName, Collectors.toList());
  // Es equivalente a 
  ...map(Instructor::getName).collect(Collectors.toList());
  // Por ejemplo: Agrupamos los instructors por años de experiencia, y luego mapeamos
  // los nombres, devolviendo un Map<Integer, List<String>> mediante collect
  Map<Integer, List<String>> mapYearsOfExperienceAndNames = Instructors.getAll().stream().collect(
      Collectors.groupingBy(Instructor::getYearsOfExperience,
          Collectors.mapping(Instructor::getName, Collectors.toList())));
  ```

- **minBy / maxBy**: Recoge un collector que produce el maximo o minimo elemento segun
el comparator que se pasa por parametro
  ```java
  // Instructor with minimum years of experience
  Optional<Instructor> instructor = Instructors.getAll().stream()
          .collect(Collectors.minBy(Comparator.comparing(Instructor::getYearsOfExperience)));
  // Equivalente con (min)
  instructor = Instructors.getAll().stream().min(Comparator.comparing(Instructor::getYearsOfExperience));

  // Similar con max
  instructor = Instructors.getAll().stream().collect(Collectors.maxBy(Comparator.comparing(Instructor::getYearsOfExperience)));
  // Equivalente con min
  instructor = Instructors.getAll().stream().max(Comparator.comparing(Instructor::getYearsOfExperience));
  ```

- **summingInt(), averagingInt()**: 
  - **summingIng()**: devuelve un collector que construye la SUMA de los valores integer sobre los que se aplica 
  - **averagingIng()**: devuelve un collector que construye la MEDIA de los valores integer sobre los que se aplica 
  ```java
  // sum of years of experience of all instructor
  int sum = Instructors.getAll().stream().collect(Collectors.summingInt(Instructor::getYearsOfExperience));
  // calculate average of years of experience of all instructors
  double average = Instructors.getAll().stream().collect(Collectors.averagingInt(Instructor::getYearsOfExperience));
  ```
 
- **groupingBy()**: Proporciona una funcionalidad similar a la clausula `GROUP BY` de SQL devolviendo un `Map<Key, Value>`
Existen tres metodos sobrecargados:
  - `groupingBy(classifier)`
    ```java
    List<String> names = List.of("Syed", "Mike", "Jenny", "Gene", "Rajeev");
    // Agrupar por longitud del String
    Map<Integer,  List<String>> result = names.stream().collect(Collectors.groupingBy(String::length));
    // Grouping by experience where > 10 years of experience is classified as Senior and others are junior
    Map<String, List<Instructor>> instructorsByExperience = Instructors.getAll().stream().collect(
        Collectors.groupingBy(instructor -> instructor.getYearsOfExperience()>10 ? "SENIOR": "JUNIOR"));
    ```
  - `groupingBy(classifier, downstream)`
    ```java
     List<String> name = List.of("Sid", "Mike", "Jenny", "Gene", "Rajeev");
     // grouping by length of string and also checking that the names contains e
     // and only return those name which has e in it   
     Map<Integer, List<String>> result = name.stream().collect(
        Collectors.groupingBy(
            String::length, 
            Collectors.filtering(
                s-> s.contains("e"),
                Collectors.toList())));
     // instructor grouping them by Senior(>10) and Junior(<10) and filter them on online courses
     Map<String, List<Instructor>> instructorByExpAndOnline = Instructors.getAll().stream().collect(
        Collectors.groupingBy(
            instructor -> instructor.getYearsOfExperience() >10 ? "SENIOR": "JUNIOR",
            Collectors.filtering(
                s->s.isOnlineCourses(),
                Collectors.toList())));
    ```
  - `groupingBy(classifier, mapfactory, downstream)`
    ```java
    List<String> name = List.of("Sid", "Mike", "Jenny", "Gene", "Rajeev");
    // grouping by length of string and also checking that the names contains e
    // and only return those name which has e in it
    LinkedHashMap<Integer, List<String>> result = name.stream()
        .collect(
            Collectors.groupingBy(
                String::length,             // Classifier
                LinkedHashMap::new,         // MapFactory
                Collectors.filtering(       // DownStream
                    s-> s.contains("e"),
                    Collectors.toList()
        )));
    // instructor grouping them by Senior(>10) and Junior(<10) and filter them
    // on online courses
    LinkedHashMap<String, List<Instructor>> instructorByExpAndOnline = Instructors.getAll().stream()
        .collect(
            Collectors.groupingBy(
                instructor -> instructor.getYearsOfExperience() >10 ? "SENIOR": "JUNIOR",  // Classifier
                LinkedHashMap::new,                 // MapFactory
                Collectors.filtering(               // Downstream
                    s -> s.isOnlineCourses(),
                    Collectors.toList()
        )));
    ```

- **partitioningBy()** se usa para particionar un stream de objetos basados en un 
predicado entregado
```java
// partition instructors in two groups of instructor first is years of experience is > 10 and other is <=10
Predicate<Instructor> experiencePredicate = instructor -> instructor.getYearsOfExperience() > 10;

// Crea dos listados, un con las que cumplen el predicado y otras con las que no
Map<Boolean, List<Instructor>> partitionMap = Instructors.getAll().stream().collect(
    Collectors.partitioningBy(experiencePredicate));

//partition but return is set instead of list
Map<Boolean, Set<Instructor>> partitionSet = Instructors.getAll().stream().collect(
    Collectors.partitioningBy(experiencePredicate, Collectors.toSet()));
```

### ParallelStream

ParallelStream divide los datos de partida en múltiples partes, las procesa en paralelo y combina el resultado
Aumenta el rendimiento en procesadores multicore. Se crearan un numero de hilos segun el numero de procesadores

Hay dos maneras de crearlo:
- Llamando al metodo `parallelStream()` en una colección
- Llamando el metodo `parallel()` en un stream

```java
IntStream.rangeClosed(0,50000).parallel().sum();
```