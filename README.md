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

### Ejemplo de Callable con lambda

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
  - Consumers especializados `IntConsumer, LongConsumer, DoubleConsumee`
- `BiConsumer<T>`
- `Predicate<T>`
  - Predicates especializados `IntPredicate, LongPredicate, DoublePredicate`
- `BiPredicate<T>`
- `Function`
- `Bifunction`
- `Unary operator`
- `Binary operator`
- `Supplier`
- Métodos por referencia
- Constructores por referencia

#### Interfaz funcional `Consumer<T>`

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

##### Consumidores especializados IntConsumer, LongConsumer, DoubleConsumer

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

#### BiConsumer

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

#### Predicados

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

##### Predicados especializados: IntPredicate, DoublePredicate, LongPredicate

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

##### Predicados y biconsumer

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

#### Bipredicate

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

#### Function

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

#### Bifunction

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

#### Unary operator

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

#### BinaryOperator

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

#### Constructores por referencia

Podemos usar un metodo por referencia para llamar a un constructor. a diferencia es que aquí llamas al “new” en vez de llamar a un método.
Si por ejemplo tenemos la clase instructor, podemos cear una factoria de Instructor llamando por referencia
a su metodo constructor:

```java

// Clase user con un unico constructor
public class User {

   private String name;
   private String password;

   public User() {
   }

   public User(String name) {
       this.name = name;
   }

   public User(String name, String pass) {
       this.name = name;
       this.password = pass;
   }
}

private class ConstructorsByReference {
    public static void main(String[] args) {

        // Creamos una lista de nombres que queremos usar para crear instancias
        List<String> userNames = new ArrayList<>();
        userNames.add("jose");
        userNames.add("luis");
        userNames.add("lucas");
        
        // Generaremos un stream usando el listado de nombres de usuarios
        // Lo importante aquí es observar que estamos llamando al constructor por referencia cuando escribimos User::new.
        Stream<User> userStream = userNames.stream().map(User::new);
    }
}
```

Aquí el compilador elige por iferenencia el constructor que tenga un solo parámetro String porque es el único que aplica.
Podemos hacer lo mismo con un constructor con más parámetros. Además podemos usar una clase "Factoria" usando su constructor
por referencia para obtener instancias

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
