# Java-Programming-Lambda-and-more-
Java Programming, Lambda and more (Java 13, 12, 11, 10, 9,8) course

WEB: https://www.udemy.com/course/java-latest-programming-from-zero-java13-java12-java11-java10-java9-j8

- - -

- [Java-Programming-Lambda-and-more-](#java-programming-lambda-and-more-)
- [JAVA 8](#java-8)
  * [Lección 1 Expresiones Lambda](#lecci-n-1-expresiones-lambda)
    + [Ejemplo de Expresiones Lambda sin parametros](#ejemplo-de-expresiones-lambda-sin-parametros)
    + [Ejemplo de Expresiones Lambda con parametros](#ejemplo-de-expresiones-lambda-con-parametros)
    + [Ejemplo de runnable con Expresiones Lambda](#ejemplo-de-runnable-con-expresiones-lambda)
    + [Ejemplo de Callable con Expresiones Lambda](#ejemplo-de-callable-con-expresiones-lambda)
    + [Scopes en Expresiones Lambda](#scopes-en-expresiones-lambda)
      - [Effectively Final](#effectively-final)
  * [Lección 2 - Interfaces funcionales](#lecci-n-2---interfaces-funcionales)
    + [Interfaces funcionales útiles:](#interfaces-funcionales--tiles-)
      - [Interfaz funcional `Consumer<T>`<a name="consumer"></a>](#interfaz-funcional--consumer-t---a-name--consumer----a-)
        * [Consumidores especializados IntConsumer, LongConsumer, DoubleConsumer<a name="consumer_especializados"></a>](#consumidores-especializados-intconsumer--longconsumer--doubleconsumer-a-name--consumer-especializados----a-)
      - [BiConsumer<a name="biconsumer"></a>](#biconsumer-a-name--biconsumer----a-)
      - [Predicados<a name="predicate"></a>](#predicados-a-name--predicate----a-)
        * [Predicados especializados: IntPredicate, DoublePredicate, LongPredicate<a name="predicate_especializados"></a>](#predicados-especializados--intpredicate--doublepredicate--longpredicate-a-name--predicate-especializados----a-)
        * [Predicados y biconsumer<a name="predicates-y-biconsumer"></a>](#predicados-y-biconsumer-a-name--predicates-y-biconsumer----a-)
      - [Bipredicate<a name="bipredicate"></a>](#bipredicate-a-name--bipredicate----a-)
      - [Function<a name="function"></a>](#function-a-name--function----a-)
      - [Bifunction<a name="bifunction"></a>](#bifunction-a-name--bifunction----a-)
      - [Unary operator<a name="unary_operator"></a>](#unary-operator-a-name--unary-operator----a-)
      - [BinaryOperator<a name="binary_operator"></a>](#binaryoperator-a-name--binary-operator----a-)
      - [Supplier<a name="supplier"></a>](#supplier-a-name--supplier----a-)
      - [Métodos por referencia<a name="metodos_por_referencia"></a>](#m-todos-por-referencia-a-name--metodos-por-referencia----a-)
      - [Constructores por referencia<a name="constructores_por_referencia"></a>](#constructores-por-referencia-a-name--constructores-por-referencia----a-)
  * [Lección 3 - Stream](#lecci-n-3---stream)
    + [Características](#caracter-sticas)
    + [Resumen](#resumen)
    + [Creación de streams](#creaci-n-de-streams)
    + [Operaciones intermedias en streams](#operaciones-intermedias-en-streams)
      - [Encadenado de operaciones intermedias](#encadenado-de-operaciones-intermedias)
    + [Operaciones finales sobre streams](#operaciones-finales-sobre-streams)
      - [Ejemplo combinando map + filter + reduce](#ejemplo-combinando-map---filter---reduce)
      - [Ordenaciones customizadas con `Comparator` y `sorted`](#ordenaciones-customizadas-con--comparator--y--sorted-)
    + [Numeric Streams](#numeric-streams)
      - [IntStream](#intstream)
      - [Funciones agregadas de NumericStreams](#funciones-agregadas-de-numericstreams)
      - [Boxing / Unboxing](#boxing---unboxing)
      - [mapToObj, mapToLong, mapToDouble](#maptoobj--maptolong--maptodouble)
    + [Collectors](#collectors)
    + [ParallelStream](#parallelstream)
  * [Lección 4 - Optionals](#lecci-n-4---optionals)
    + [Construcción](#construcci-n)
    + [Comprobación de existencia de valor](#comprobaci-n-de-existencia-de-valor)
    + [Métodos de encadenamiento](#m-todos-de-encadenamiento)
    + [Métodos de finalización](#m-todos-de-finalizaci-n)
    + [Uso de `Optional` de forma funcional](#uso-de--optional--de-forma-funcional)
  * [Lección 5 - Default / Static methods](#lecci-n-5---default---static-methods)
    + [Herencia múltiple por implementación de interfaces](#herencia-m-ltiple-por-implementaci-n-de-interfaces)
  * [Lección 6 - New Date/Time libraries](#lecci-n-6---new-date-time-libraries)
    + [LocalDate](#localdate)
    + [LocalTime](#localtime)
    + [LocalDateTime](#localdatetime)
    + [Conversion de LocalDateTime a Date / Time](#conversion-de-localdatetime-a-date---time)
    + [Instant / Duration](#instant---duration)
    + [TimeZones - ZonedDateTime, ZoneId](#timezones---zoneddatetime--zoneid)
    + [Conversiones con anteriores versiones de la API](#conversiones-con-anteriores-versiones-de-la-api)
- [JAVA 9](#java-9)
  * [Leccion 7 - JShell](#leccion-7---jshell)
    + [Expresiones](#expresiones)
    + [Variables](#variables)
    + [Métodos y Clases](#m-todos-y-clases)
    + [Editando Fragmentos](#editando-fragmentos)
  * [Lección 8 - Java Modules](#lecci-n-8---java-modules)
  * [Lección 9 - Factory Methods for Collections](#lecci-n-9---factory-methods-for-collections)
  * [Lección 10 - Mejoras en try-with-resources](#lecci-n-10---mejoras-en-try-with-resources)
- [JAVA 10](#java-10)
  * [Leccion 11 - `var` type](#leccion-11----var--type)
- [JAVA 11](#java-11)
  * [Leccion 12 - `var` with lambda](#leccion-12----var--with-lambda)
  * [Leccion 13 - http client API](#leccion-13---http-client-api)
- [JAVA 12](#java-12)
  * [Leccion 12 - Switch expressions (mejoras)](#leccion-12---switch-expressions--mejoras-)
- [JAVA 13](#java-13)
  * [Lección 13 - Textblocks](#lecci-n-13---textblocks)

- - -

# JAVA 8

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

### Resumen

| Tipo operación             | Nombre                                                                     | Metodo                                                                                         | Obs                                                                                                                                                                                                   |
|----------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Creacion                   | stream                                                                     | `Arrays.aList(1,2,3).stream()`                                                                 | Stream de tipo de datos similares                                                                                                                                                                     |
| Creacion                   | of                                                                         | `Stream.of(1,2,3)`                                                                             | Stream de tipo de datos similares                                                                                                                                                                     |
| Creacion                   | iterate                                                                    | `Stream.iterate(0, i -> i + 2)`                                                                | Secuencial infinito ORDENADO                                                                                                                                                                          |
| Creacion                   | generate                                                                   | `Stream.generate(new Random()::nextInt)`                                                       | Secuencial infinito RANDOM                                                                                                                                                                            |
| Intermedia                 | distinct                                                                   | `...stream().distinct()…`                                                                      | Filtra o recolecta todos los elementos distintos de un string                                                                                                                                         |
| Intermedia                 | count                                                                      | `…stream().count()…`                                                                           | Devuelve el numero de elementos en el stream                                                                                                                                                          |
| Intermedia                 | sort                                                                       | `...stream().sort()…`                                                                          | Ordena el stream basandose en un Comparator                                                                                                                                                           |
| Intermedia                 | sorted                                                                     | `....stream().sorted(Comparator.comparing(Instructor::getName)`                                | Ordena el stream basandose en un Comparator                                                                                                                                                           |
| Intermedia                 | pararell                                                                   | `…stream().parallel()…`                                                                        | Permite ejecutar las operaciones del stream en hilos en paralelo, para que java lance un conjunto de hilos para realizar la tarea                                                                     |
| Intermedia                 | map                                                                        | `...stream().map(x -> x * x)…`                                                                 | Devuelve un stream consistente en los resultados de aplicar la función pasada por parametro sobre los elementos del stream                                                                            |
| Intermedia                 | flatMap                                                                    | `…stream().map(…).flatMap(List::stream)…`                                                      | Devuelve un flujo que consta de los resultados de reemplazar cada elemento de este flujo con el contenido de un flujo mapeado producido al aplicar la función de mapeo proporcionada a cada elemento. |
| Intermedia                 | filter                                                                     | `....stream().filter(n -> n.startswith("J"))…`                                                 | Filtra los resultados basados en el predicado pasado al filtro                                                                                                                                        |
| Intermedia                 | anyMatch                                                                   | `...stream().anyMatch(s -> s.startsWith("J"))`                                                 | Analiza cada objeto del stream y devuelve true si encuentra uno que cumpla el filtro. No recorre todo el stream, si encuentra un objeto que cumpla la condición, devuelve true                        |
| Intermedia                 | allMatch                                                                   | `…stream().allMatch(s -> s.startsWith("J"))`                                                   | Devuelve todos los elementos que cumplan el predicado pasado por parámetro                                                                                                                            |
| Intermedia                 | noneMatch                                                                  | `…stream().noneMatch(s -> s.startsWith("J"))`                                                  | Devuelve todos los elementos que NO cumplan con el predicado pasado por parámetro                                                                                                                     |
| Intermedia                 | findFirst                                                                  | `...stream().findFirst()`                                                                      | Devuelve un Optional conteniendo el primer elemento del stream o un optional vacio si ningun elemento lo cumple                                                                                       |
| Intermedia                 | findAny                                                                    | `...stream().filter(precio -> precio.intValue() < 0).findAny().isPresent()`                    | Indica que si encuentra alguno devuelva un Optional. En este caso SI se recorre todo el stream.                                                                                                       |
| Intermedia                 | limit                                                                      | `...stream().limit(5)…`                                                                        | Devuelve un stream de tamaño no superior al long pasado por parametro                                                                                                                                 |
| Intermedia                 | skip                                                                       | `…stream().skip(5)…`                                                                           | Devuelve un stream obviando los primeros n elementos pasados por parametro                                                                                                                            |
| Final                      | collect                                                                    | `…stream()...collect(Collectors.toList())`                                                     | Devolver el resultado de las operaciones realizadas en el stream usando el tipo indicado por parametro                                                                                                |
| Final                      | forEach                                                                    | `…stream()…forEach(y -> System.out.println(y))`                                                | Itera sobre el stream                                                                                                                                                                                 |
| Final                      | reduce                                                                     | `…stream()…reduce(0,(a,b) -> a +b)`                                                            | Obtiene todos los elementos y los combina en un solo resultado sencillo combinandolos                                                                                                                 |
| Final                      | max                                                                        | `...stream().max(Integer::compareTo)`                                                          | Obtiene el máximo de los valores del stream, segun el Comparator pasado por parámetro                                                                                                                 |
| Final                      | min                                                                        | `…numStream().min(Integer:compareTo)`                                                          | Obtiene el mínimo de los valores del stream, segun el Comparator pasado por parámetro                                                                                                                 |
| NumericStream / intermedia | sum                                                                        | `…numStream().sum()`                                                                           | Devuelve la suma de los elementos del stream                                                                                                                                                          |
| NumericStream / intermedia | max                                                                        | `…numStream().max()`                                                                           | Devuelve el máximo de los elementos del stream                                                                                                                                                        |
| NumericStream / intermedia | min                                                                        | `…numStream().min()`                                                                           | Devuelve el mínimo de los elementos del stream                                                                                                                                                        |
| NumericStream / intermedia | average                                                                    | `…numStream().average()`                                                                       | Devuelve la media de los elementos del stream                                                                                                                                                         |
| NumericStream / intermedia | boxed                                                                      | `…numStream().boxed()...`                                                                      | Convertir un stream de primitivos en un objeto de clase wrapper                                                                                                                                       |
| NumericStream / intermedia | mapToInt                                                                   | `…numStream().mapToInt(Integer::intValue)...`                                                  | Convierte un stream de wrappers en los primitivos correspondientes                                                                                                                                    |
| NumericStream / intermedia | mapToObj                                                                   | `…numStream().mapToObj(a --> Integer.toBinaryString(a))...`                                    | En un Numeric Stream, devuelve un stream de objetos                                                                                                                                                   |
| NumericStream / intermedia | mapToLong                                                                  | `…numStream().mapToLong(num --> (long) num)...`                                                | En un Numeric Stream, devuelve un stream de Longs                                                                                                                                                     |
| NumericStream / intermedia | mapToDouble                                                                | `…numStream().mapToDouble(num --> (double) num)...`                                            | En un Numeric Stream, devuelve un stream de Doubles                                                                                                                                                   |
| Collectors                 | joining()                                                                  | `…stream().collect(Collectors.joining());`                                                     | Concatena los elementos de entrada en una cadena, en el orden en que lo encuentra                                                                                                                     |
| Collectors                 | joining(CharSequence delimiter)                                            | `…stream().collect(Collectors.joining(","));`                                                  | Concatena los elementos de entrada en una cadena separados por el delimitador                                                                                                                         |
| Collectors                 | joining(CharSequence delimiter, CharSequence prefix, CharSequence suffix)  | `…stream().collect(Collectors.joining(",","preffix","suffix"));`                               | Concatena los elementos de entrada en una cadena separados por el delimitador con un prefijo y un sufijo pasados por parametros                                                                       |
| Collectors                 | counting()                                                                 | `…stream().collect(Collectors.counting())`                                                     | Cuenta el numero de elementos en el stream                                                                                                                                                            |
| Collectors                 | mapping()                                                                  | `…stream().collect(Collectors.mapping(Instructor::getName, Collectors.toList()))`              | Coge una función y otro collector y crea un nuevo collector que aplica la funcion y recoge el resultado usando el collector pasado por parámetro                                                      |
| Collectors                 | minBy / maxBy                                                              | `…stream().collect(Collectors.minBy(Comparator.comparing(Instructor::getYearsOfExperience)));` | Recoge un collector que produce el maximo o minimo elemento segun el comparator que se pasa por parametro                                                                                             |
| Collectors                 | summingInt                                                                 | `...stream().collect(Collectors.summingInt(Instructor::getYearsOfExperience));`                | Devuelve un collector que construye la SUMA de los valores integer sobre los que se aplica                                                                                                            |
| Collectors                 | averagingInt                                                               | `...stream().collect(Collectors.averagingInt(Instructor::getYearsOfExperience));`              |  Devuelve un collector que construye la MEDIA de los valores integer sobre los que se aplica                                                                                                          |
| Collectors                 | groupingBy                                                                 | Ver expandido                                                                                  | Proporciona una funcionalidad similar a la clausula GROUP BY de SQL devolviendo un Map<Key, Value>                                                                                                    |
| Collectors                 | partitioningBy                                                             | `...stream().collect(Collectors.partitioningBy(experiencePredicate))`                          | Particionar un stream de objetos basados en un predicado entregado. Devuelve un mapa `Map<Boolean, List<T>>` con los elementos que cumplen y los que no  separados                                    |

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

## Lección 4 - Optionals

Esta clase permite evitar excepciones por NullPointerException. Se trata de unac lase generica que puede
contener cualquier clase de objeto.

### Construcción

```java
// Clase
public final class Optional<T>{}

// Creacion
public static<T> Optional<T> empty();
public static <T> Optional<T> ofNullable(T value);
public static <T> Optional<T> of(T value);

// Ejemplo
String nombre = "Daniel";
Optional<String> oNombre = Optional.of(nombre);
```

### Comprobación de existencia de valor

El método `isPresent` método es el equivalente a `variable == null` y cómo el propio nombre indica nos dice si el objeto
`Optional` contiene un valor o está vacío. Este método se usa principalmente si trabajamos de manera imperativa con
`Optional`. Y el método `get` es el encargado de devolvernos el valor, devolviendo una excepción si no estuviera presente.

```java
// isPresent
Optional<String> stringOptional = Optional.ofNullable("Hello World");
if(stringOptional.isPresent())
System.out.println("stringOptional = " + stringOptional);

// ifPresent para uso con Lambdas
stringOptional.ifPresent(s -> System.out.println("s = " + s));

// Obtencion del valor
public T get();
```

### Métodos de encadenamiento

`Optional` permite encadenar distintas operaciones que devuelvan `Optional` sin tener que comprobar si el valor está presente
después de cada operación

```java
public Optional<T> filter(Function f);
public<U> Optional<U> map(Function f);
public<U> Optional<U> flatMap(Function f);
```

Por ejemplo el metodo `map`, comprueba si el Optional está vacío, si lo está devuelve un `Optional` vacío y si no, 
aplica la función que le hemos pasado por parámetro, pasándole el valor del `Optional`

```java
public<U> Optional<U> map(Function<? super T, ? extends U> mapper) {
    Objects.requireNonNull(mapper);
    if (!isPresent())
        return empty();
    else {
        return Optional.ofNullable(mapper.apply(value));
    }
}
```

### Métodos de finalización

Finalmente estos métodos nos permiten finalizar una serie de operaciones, teniendo tres maneras: 

- **orElse**: devuelve el valor o si no devolverá el valor que le demos. 
- **orElseGet**: devolverá el valor si está presente y si no, invocará la función que le pasemos por parámetro y devolverá el resultado de dicha función. 
- **orElseThrow**: devolverá el valor si está presente y si invocará la función que le pasemos, la cual tiene que devolver una excepción y lanzará dicha excepción. 
Esto nos ayudará a trabajar en conjunción con APIs que todavía usen excepciones.

```java
public T orElse(T other);
public T orElseGet(Function f);
public <X extends Throwable> T orElseThrow(Function f);
```

### Uso de `Optional` de forma funcional

El uso de `Optional` está pensado para usarse de forma funcional, no de forma imperativa.
Si quisieramos chequear los datos de la duración de las canciones de un album usando `Optional`, según bajamos de niveles
de anidamiento la cosa se complica, dejando de ser práctica:

```java
private static Optional<Double> getDurationOfAlbumWithName(String name) {
    Album album;
    Optional<Album> albumOptional = getAlbum(name);
    if (albumOptional.isPresent()) {
        album = albumOptional.get();
        Optional<List<Track>> tracksOptional = getAlbumTracks(album.getName());
        double duration = 0;
        if (tracksOptional.isPresent()) {
            List<Track> tracks = tracksOptional.get();
            for (Track track : tracks) {
                duration += track.getDuration();
            }
            return Optional.of(duration);
        } else {
            return Optional.empty();
        }
    } else {
        return Optional.empty();
    }
}
```

El uso **funcional** de `Optional` y lambdas permite que este codigo se simplifique usando los metodos de encadenamiento y
de finalización, de forma que de no encontrar nada se devuelve un valor concreto

```java
private static double getDurationOfAlbumWithName(String name) {
    return getAlbum(name)
            .flatMap((album) -> getAlbumTracks(album.getName()))
            .map((tracks) -> getTracksDuration(tracks))
            .orElse(0.0);
}
```

## Lección 5 - Default / Static methods

Con Java 8 se incorpora la opción de que las interfaces dispongan de métodos `default` y métodos `static`, implementando 
el cuerpo por defecto del método. En caso de los métodos por `default`, el comportamiento puede ser sobreescrito por las
clases que lo implementen, pero no en los métodos `static`.

```java
// Interfaz con metodo default
public interface InterfaceA {
    default void sumA(int num1, int num2){
        System.out.println("InterfaceA.sumA " + (num1 + num2));
    }
}

// Clase implementando el método 
public class Example implements InterfaceA {
    public static void main(String[] args) {
        ...    
    }

    // Podemos sobreescribir el método default
    @Override
    public int sum(int num1, int num2) {
       return num1 + num2;
    }
}
```

### Herencia múltiple por implementación de interfaces

En caso de herencia múltiple por implementación de interfaces, en caso de que el método exista en las distintias interfaces,

- Si la clase no lo implementa, se ejecuta el metodo de la ultima interfaz que lo implemente.
- Si la clase lo implementa, se ejecuta el de la clase

```java
public interface InterfaceA {
    default void sumA(int num1, int num2){
        System.out.println("InterfaceA.sumA " + (num1 + num2));
    }
}

public interface InterfaceB extends InterfaceA{
    default void sumA(int num1, int num2){
        System.out.println("InterfaceB.sumA " + (num1 + num2));
    }
}

public class MultipleIneritanceExampleA implements InterfaceA, InterfaceB {
    public static void main(String[] args) {
        MultipleIneritanceExampleA multipleIneritanceExample = new MultipleIneritanceExampleA();
        multipleIneritanceExample.sumA(4,8);  // Usa el de InterfazB
    }
}

public class MultipleIneritanceExampleB implements InterfaceA, InterfaceB {
    public static void main(String[] args) {
        MultipleIneritanceExampleB multipleIneritanceExample = new MultipleIneritanceExampleB();
        multipleIneritanceExample.sumA(4,8);  // Usa el de la clase
    }

    // Usará este
    public void sumA (int num1, int num2){
        System.out.println("MultipleIneritanceExample.sumA" + (num1 + num2));
    }
}
```

## Lección 6 - New Date/Time libraries

Se ha incluido una nueva API para el trabajo con fechas en Java, dado que tradicionalmente la API de fechas ha sido bastante
caótica siempre. Principalmente se han incluido dos clases principales:

- **Local**: API simplificada sin complicaciones de manejo de timezones
- **Zoned**: API especializada en trabajo con varias timezones

```java
// Ejemplos básicos
LocalDate localDate = LocalDate.now();
LocalTime localTime = LocalTime.now();
LocalDateTime localDateTime = LocalDateTime.now();
```

### LocalDate

- **Creación**
  - Con fecha actual: `LocalDate localDate = LocalDate.now();`
  - Indicando dia del año: `LocalDate localDate = LocalDate.ofYearDay(2018, 35);`
  - Indicando fecha completa: `LocalDate localDate = LocalDate.of(2018, 05, 23);`
  
- **Obtención de datos**
  - Nombre del Mes: `localDate.getMonth()`
  - Numero de mes: `localDate.localDate.getMonthValue()`
  - Numero de mes (2): `localDate.get(ChronoField.MONTH_OF_YEAR)`
  - Dia de la semana: `localDate.getDayOfWeek()`
  - Dia del año: `localDate.getDayOfYear()`

- **Modificación**:

LocalDate es un objeto **inmutable** por lo que a no ser que le asignemos el valor expresamente no cambiará su valor

  - Sumar dias: `localDate = localDate.plusDays(4);`
  - Sumar meses: `localDate.plusMonths(2));`
  - Sumar años: `localDate.plusYears(2));`
  - Restar días: `localDate.minusDays(10));`
  - Establecer año: `localDate.withYear(2023));`
  - Establecer año (2): `localDate.with(ChronoField.YEAR, 2025));`
  - Establecer fecha con TemporalAdjusters: `localDate.with(TemporalAdjusters.lastDayOfMonth()));`
 
 ### LocalTime
 
 - **Creación**:
 
  - Con fecha actual: `LocalTime localTime = LocalTime.now();`
  - Estableciendo fecha: `localTime = LocalTime.of (15, 18);`
  - Estableciendo fecha (2): `localTime = LocalTime.of(15, 18, 22);`
  - Estableciendo fecha (3): `localTime = LocalTime.of(15,18,23,22222222);`

- **Obtención**:

  - Horas: `localTime.getHour()`
  - Minutos: `localTime.getMinute()`
  - Minutos del presente dia: `localTime.get(ChronoField.MINUTE_OF_DAY))`
  - Segundos: `localTime.getSecond()`
  - Segundos del presente dia: `localTime.get(ChronoField.SECOND_OF_DAY))`
  - NanoSegundos: `localTime.getNano()`

- **Modificación**:

LocalTime es un objeto **inmutable** por lo que a no ser que le asignemos el valor expresamente no cambiará su valor

  - Suma horas: `localTime.plusHours(2));`
  - Suma minutos: `localTime.plusMinutes(22));`
  - Suma segundos: `localTime.plusSeconds(30));`
  - Suma nanosegundos: `localTime.plusNanos(222222));`
  - Resta horas: `localTime.minusHours(2));`
  - Resta horas (2): `localTime.minus(2, ChronoUnit.HOURS));`
  - Establecimiento de hora en medianoche: `localTime.with(LocalTime.MIDNIGHT));`
  - Establecimiento hora del dia: `localTime.with(ChronoField.HOUR_OF_DAY, 4));`

### LocalDateTime

- **Creación**

  - Actual: `LocalDateTime localDateTime = LocalDateTime.now();`
  - Con fecha y hora expresa: `LocalDateTime.of(2022, 1, 12, 12,12,12);`
  - Con fecha y hora expresa (2): `LocalDateTime.of(LocalDate.now(), LocalTime.now());`

- **Obtención**:

  - Hora: `localDateTime.getHour()`
  - Mes: `localDateTime.getMonth()`
  - Minuto: `localDateTime.getMinute()`
  - Segundos: `localDateTime.getSecond()`
  - Mes del año: `localDateTime.get(ChronoField.MONTH_OF_YEAR)`

- **Modificación**:

  - Sumar años: `localDateTime.plusYears(3)`
  - Sumar horas: `localDateTime.plusHours(4)`
  - Sumar minutos: `localDateTime.plusMinutes(60)`
  - Establecimiento de hora: `localDateTime.with(ChronoField.HOUR_OF_DAY,3))`
  - Establecimiento de hora a la medianoche: `localDateTime.with(LocalTime.MIDNIGHT)`

### Conversion de LocalDateTime a Date / Time

- LocalDateTime a LocalDate: `localDateTime.toLocalDate()` 
- LocalDateTime a LocalTime: `localDateTime.toLocalTime()`

### Instant / Duration

Instant se define como el instante en el continuo datetime especificado como el numero de milisegundos
desde el 1/1/1970 hasta ahora

Representa el numero de nanosegundos en la linea de tiempo. Se suele usar para representar tiempo máquina

- `Instant` genera timestamps 
  - **Creacion**: `Instant timestamp = Instant.now()`
  - **Modificacion**: `Instant timestamp1 = Instant.now().plusSeconds(3600);`
  - Puede usarse para generar LocalDateTime: `LocalDateTime.ofInstant(timestamp1, ZoneId.systemDefault());`  

- `Duration` representa intervalos de tiempo: 

  - **Creación**: `Duration duration = Duration.between(timestamp1,timestamp);`
  - **Uso**: `duration.toSeconds()`

### TimeZones - ZonedDateTime, ZoneId

- Obtener las timezones: `ZoneId.getAvailableZoneIds().stream().forEach(System.out::println);`
- Establecer una ZoneDateTime según la timeZone: `ZonedDateTime.now(ZoneId.of("Europe/London")));`
- Conversión a ZoneDateTime:
    ```java
    LocalDateTime localDateTime = LocalDateTime.now();
    ZonedDateTime zonedDateTime = localDateTime.atZone(ZoneId.of("America/New_York"));
    localDateTime.atOffset(ZoneOffset.ofHours(-10));
    ```

### Conversiones con anteriores versiones de la API

- Date a LocalDateTime:
    ```java
    Date date = new Date();
    LocalDateTime localDateTime = date.toInstant().atZone(ZoneId.systemDefault()).toLocalDateTime();
    ```
- java.sql.Date a LocalDate:
    ```java
    java.sql.Date dateSql = new java.sql.Date(System.currentTimeMillis());
    LocalDate localDate = dateSql.toLocalDate();
    ```
 

# JAVA 9
 
## Leccion 7 - JShell

JShell/REPL es una herramienta interactiva para aprender Java y prototipado de código Java. Evalua declaraciones, órdenes
y expresiones según se van introduciendo, y muestra los resultados inmediatamente.
REPL se puede usar para realiza pruebas, test, snippets....
Requiere de al menos Java 9 y la variable de entorno JAVA_HOME definida

`$ jshell`: Inicia el JShell REPL
`jshell> / <comando>`: Ejecuta un comando JShell dado
`jshell> / exit`: Salir de JShell
`jshell> / help`: Ver una lista de comandos de JShell
`jshell> <java_expression>`: Evalúa la expresión Java dada (punto y coma opcional)
`jshell> / vars O / métodos O / tipos`: vea una lista de variables, métodos o clases, respectivamente.
`jshell> / open <archivo>`: lee un archivo como entrada al shell
`jshell> / edit <identifier>`: - edita un fragmento en el editor de conjuntos
`jshell> / set editor <comando>`: establece el comando que se usará para editar fragmentos de código usando / editar
`jshell> / drop <identifier>`: borra un fragmento
`jshell> / reset`: Restablece la JVM y borra todos los fragmentos

Los siguientes paquetes se importan automáticamente cuando se inicia JShell:

```java
import java.io.*
import java.math.*
import java.net.*
import java.nio.file.*
import java.util.*
import java.util.concurrent.*
import java.util.function.*
import java.util.prefs.*
import java.util.regex.*
import java.util.stream.*
```

### Expresiones

Dentro de JShell, puede evaluar expresiones de Java, con o sin punto y coma. Estos pueden ir desde expresiones y declaraciones básicas hasta expresiones más complejas:

```java
jshell> 4+2
jshell> System.out.printf("I am %d years old.\n", 421)
```

Los bucles y los condicionales también están bien:

```java
jshell> for (int i = 0; i<3; i++) {
   ...> System.out.println(i);
   ...> }
```

Es importante tener en cuenta que las expresiones dentro de los bloques deben tener punto y coma.

### Variables

Puedes declarar variables locales dentro de JShell:

```java
jshell> String s = "hi"
jshell> int i = s.length
```

Las variables se pueden redeclar con diferentes tipos; Esto es perfectamente válido en JShell:

```java
jshell> String var = "hi"
jshell> int var = 3
```

Para ver una lista de variables, ingrese `/vars` en el indicador de JShell.

### Métodos y Clases

Puedes definir métodos y clases dentro de JShell:

```java
jshell> void speak() {
   ...> System.out.println("hello");
   ...> }

jshell> class MyClass {
   ...> void doNothing() {}
   ...> }
```

No se requieren modificadores de acceso. Al igual que con otros bloques, se requieren puntos y coma dentro de los cuerpos de los métodos. Tenga en cuenta que, al igual que con las variables, es posible redefinir los métodos y las clases. Para ver una lista de métodos o clases, ingrese /methods o /types en el indicador de JShell, respectivamente.

### Editando Fragmentos

La unidad básica de código utilizada por JShell es el fragmento o la entrada de origen . Cada vez que declara una variable local o define un método o clase local, crea un fragmento de código cuyo nombre es el identificador de la variable / método / clase. En cualquier momento, puede editar un fragmento de código que haya creado con el comando /edit . Por ejemplo, digamos que he creado la clase Foo con una sola bar método:

```java
jshell> class Foo {
   ...> void bar() {
   ...> }
   ...> }
```

Ahora, quiero rellenar el cuerpo de mi método. En lugar de reescribir toda la clase, puedo editarla:

```java
jshell> /edit Foo
```

De forma predeterminada, aparecerá un editor de swing con las funciones más básicas posibles. Sin embargo, puedes cambiar el editor que JShell usa:

```java
jshell> /set editor emacs
jshell> /set editor vi
jshell> /set editor nano
jshell> /set editor -default
```

Tenga en cuenta que si la nueva versión del fragmento de código contiene errores de sintaxis, es posible que no se guarde. Del mismo modo, un fragmento de código solo se crea si la declaración / definición original es sintácticamente correcta; lo siguiente no funciona:

```java
jshell> String st = String 3
//error omitted
jshell> /edit st
|  No such snippet: st
```

Sin embargo, los fragmentos de código pueden compilarse y, por lo tanto, ser editables a pesar de ciertos errores de tiempo de compilación, como los tipos que no coinciden, los siguientes trabajos:

```java
jshell> int i = "hello"
//error omitted
jshell> /edit i
```

Finalmente, los fragmentos de código se pueden eliminar con el comando `/drop` :

```java
jshell> int i = 13
jshell> /drop i
jshell> System.out.println(i)
|  Error:
|  cannot find symbol
|    symbol:   variable i
|  System.out.println(i)
|
```

Para eliminar todos los fragmentos de código, restableciendo así el estado de la JVM, use `\reset` :

```java
jshell> int i = 2
jshell> String s = "hi"
jshell> /reset
|  Resetting state.

jshell> i
|  Error:
|  cannot find symbol
|    symbol:   variable i
|  i
|  ^

jshell> s
|  Error:
|  cannot find symbol
|    symbol:   variable s
|  s
|  ^
```

## Lección 8 - Java Modules

Saber mas: 
- https://www.arquitecturajava.com/java-9-modules/
- https://www.adictosaltrabajo.com/2017/10/30/modularidad-en-java-9-12/
- https://www.adictosaltrabajo.com/2017/11/16/modularidad-en-java-9-22/

Java 9 introdujo una capa de abtracción en lo alto de los paquetes que se llama `Java Platform Module System`
Los módulos de Java proporcionan una mayor encapsulación de las clases contenidas en un paquete y las librerías. 
Esta encapsulación evita que una aplicación u otra librería haga uso y dependa de clases y paquetes de los que no debería 
lo que mejora la compatibilidad con versiones futuras.

Antes del sistema de módulos de Java la librería de tiempo de ejecución consistía en un gran archivo `rt.jar` con un 
tamaño de más de 60 MiB. Este archivo contiene la mayor parte de clases de la plataforma en forma de monolito. 
Para conseguir mayor flexibilidad y ser una plataforma de futuro se decidió modularizar el JDK.

Con el tiempo las dependencias entre los propios paquetes y clases de la API de Java estaba enmarañada, con Java 9 las 
dependencias entre paquetes se ha simplificado en gran medida.

Los beneficios son:

- **Configuración confiable**: el sistema de módulos comprueba si una combinación de módulos satisface todas las dependencias antes de compilar o ejecutar una aplicación.
- **Encapsulación fuerte**: se evitan dependencias sobre detalles internos de implementación.
- **Desarrollo escalable**: se crean límites entre el equipo que desarrolla un módulo y el que lo usa.
- **Optimización**: dado que el sistema de módulos sabe que módulos necesita cada uno solo se consideran los necesarios mejorándose tiempos de inicio y memoria consumida.
- **Seguridad**: la encapsulación y optimización limita la superficie de ataque.

Los comandos para compilar y ejecutar el ejemplo directamente con los comandos javac y java si cambian, ahora se usa en 
vez de classpath la opción module-path y se indica la clase del módulo que contiene el método main del programa

```bash
javac -d build src/helloworld/module-info.java src/helloworld/io/github/picodotdev/blogbitix/java9/helloworld/Main.java
java --module-path build --module helloworld/io.github.picodotdev.blogbitix.java9.helloworld.Main
```

En las nuevas aplicaciones modulares, se crea nuevo archivo `module-info.java` que incorpora
las dependencias modulares entre proyectos: Si por ejemplo tenemos un proyecto `com.modulos.principal` que hace uso de clases en los proyectos
`com.modulos.producer` y `com.modulos.consumer`, este archivo `module-info.java` tendria la estructura:

```java
module com.modulos.principal {}
    requires com.modulos.producer;
    requires com.modulos.consumer;
```

Igualmente, cada modulo generará su `module-info.java`, indicando que clase se exporta:

```java
module com.modulos.producer {
    exports com.modules.producer;
}
```

## Lección 9 - Factory Methods for Collections

En Java 9 se incorporan los Factory Methods para crear listas, sets y map inmodificables
Antes de Java 9 se creaban asi:

```java
List<String> names = new ArrayList(); 
names.add("Syed"); 
names.add("Mike"); 
names.add("Jenny"); 
names = Collections.unmodifiableList(names);
```

Con los `Factory Methods` introducidos en Java 9:

```java        
List<String> names2 = List.of("Syed", "Mike", "Jenny");
Set<String> set = Set.of("Syed", "Mike", "Jenny");
Map<String, String> map = Map.of("Grade1", "Syed", "Grade2", "Mike");
```

## Lección 10 - Mejoras en try-with-resources

El try-with-resources es una orden try que declara uno o más recursos, que son objetos que deben cerrarse después de uqe
el programa se finalice. Con try-with-resources nos aseguramos que cada recurso se cierre al final del statement.
Para ser un recurso, el objeto debe implementar `java.lang.AutoCloseable` o `java.io.Closeable`.

En Java 8 se realizaba declarando el resource fuera del bucle y reasignandolo en la definicion del try:
```java
Reader inputString = new StringReader("Don't cut any corners");
BufferedReader bufferedReader = new BufferedReader(inputString);
try(BufferedReader bufferedReader1=bufferedReader){
    System.out.println("bufferedReader1.readLine() = "
            + bufferedReader1.readLine());
}
```

En Java 9 no hace falta redefinirlo en la cabecera del try:
```java
Reader inputString2 = new StringReader("Hang in there");
BufferedReader bufferedReader2 = new BufferedReader(inputString2);
try(bufferedReader2){
    System.out.println("bufferedReader2.readLine() = "
            + bufferedReader2.readLine());
}
``` 

# JAVA 10

## Leccion 11 - `var` type

Desde Java 10 se puede eliminar la definición de tipo expresa al crear una variable
Para ello:
- La variable local `var` debe ser inicializada en su declaración
- El compilador debe ser capaz de inferir el tipo de variable asi que una variable con `null` no compilará, dado que el compilador
infiere el tipo de la declaración

```java
var name = "Mike"; // Infiere el tipo String
var dateTime = LocalDateTime.now(); // Infiere el tipo LocalDateTime
var numbers; // Al no poder inferir el tipo no compila
```

# JAVA 11

## Leccion 12 - `var` with lambda

A partir de java 11 se permite el uso de `var` en funciones lambda:

```java
(var j, var i) -> i + j;
```

## Leccion 13 - http client API

Java 11 introdujo un nuevo API para http. Por defecto utilizará HTTP/2, aunque la request se rebaja a HTTP/1.1
en caso de que el server no la admita.

La nueva API utiliza streams reactivos para trabajar de forma asíncrona con request y responses.
También se pueden usar para enviar request y recibir responses sincronizadamente.

```java
HttpClient httpClient = HttpClient.newHttpClient();
HttpClient httpClient = HttpClient.newBuilder().build();
```

El nuevo cliente consiste en tres clases principales:
- **HttpClient**: Se usa para enviar una request y recibir la response
- **HttpRequest**: Encapsula los detalles del recurso solicitado, incluyendo la URI
- **HttpResponse**: Encapsula la response del server

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder().uri(URI.create("https://www.ldapsoft.com")).build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
```

De forma similar se pueden realizar llamadas Asíncronas:

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder().uri(URI.create("https://www.ldapsoft.com")).build();
CompletableFuture<Void> response =
        client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
              .thenApply(HttpResponse::body)
              .thenAccept(System.out::println);
response.get();
```

# JAVA 12

## Leccion 12 - Switch expressions (mejoras)

Se introdujeron para mejorar las switch. Los `break` dejan de ser necesarios, hay menos código innecesario
Se permite agrupar selecciones para ejecutar sentencias a la vez:
 
```java
String month="JANUARY";
switch (month){
    case "JANUARY", "FEBURARY", "MARCH" -> System.out.println("FIRST QUARTER");
    case "APRIL", "MAY", "JUNE" -> System.out.println("SECOND QUARTER");
    case "JULY", "AUGUST", "SEPTEMBER"-> System.out.println("THIRD QUARTER");
    case "OCTOBER", "NOVEMBER", "DECEMBER" -> System.out.println("FOURTH QUARTER");
    default -> System.out.println("UNKNOWN QUARTER");
}
``` 

También se permite incluir acciones en los `case`, usando la palabra reservada `yield` para que el `switch` devuelva un resultado,
siendo el equivalente a un `return` de un método:

```java
String month="JANUARY";

// Evaluamos la variable, pudiendo realizar selecciones multiples en los case
String quarter = switch(month){
    case "JANUARY", "FEBURARY", "MARCH" ->{
        var isLeapYear = LocalDate.now().isLeapYear();
        yield (isLeapYear ? "FIRST QUARTER - LEAP YEAR": "FIRST QUARTER");
    }
    case "APRIL", "MAY", "JUNE" -> "SECOND QUARTER"; 
    case "JULY", "AUGUST", "SEPTEMBER" -> "THIRD QUARTER"; 
    case "OCTOBER", "NOVEMBER", "DECEMBER" -> "FOURTH QUARTER"; 
    default -> "UNKNOWN QUARTER"; 
}; 
```
  
# JAVA 13

## Lección 13 - Textblocks

Java 13 introdujo la definición de bloques de textos mediante el uso de las triples comillas dobles:

```java
String st1 = """
             Hello World
             Using 
             text blocks !
             """;
```
