# Taller 8 - CustomersService y Excepciones

En este taller se trabajará la creación de excepciones y la implementación de un nuevo servicio.

## Indice

1. [Preguntas teóricas](#preguntas-teóricas)
2. [Enunciado](#enunciado)
3. [Calificación](#calificación)
4. [¿Qué sigue?](#¿qué-sigue?)

## Preguntas teóricas

Marque la respuesta correcta a las siguientes preguntas. Estas preguntas no afectan la calificación del taller, pero le ayudarán a reforzar los conceptos vistos en clase:

1. ¿Qué es una excepción en Java?
    -  Un error en tiempo de ejecución.
    -  Un error en tiempo de compilación.
    -  Un objeto que representa un evento inesperado en tiempo de ejecución.
    -  Un objeto que representa un evento inesperado en tiempo de compilación.
2. ¿Cómo se categorizan las excepciones en Java según su origen?
   - Excepciones de java y excepciones definidas por el usuario (built-in exceptions & User-Defined exceptions).
   - Excepciones y errores.
   - Excepciones de tiempo de ejecución y excepciones de tiempo de compilación.
   - Ninguna de las anteriores.
3. ¿Qué es un checked exception?
   - Una excepción que se verifica en tiempo de compilación y es mostrada por el ide.
   - Una excepción que se verifica en tiempo de ejecución.
   - Una excepción que se lanza en tiempo de compilación.
   - Una excepción que se lanza en tiempo de ejecución.
4. ¿Qué es un unchecked exception?
   - Una excepción que se verifica en tiempo de compilación y es mostrada por el ide.
   - Una excepción que se verifica y lanza en tiempo de ejecución.
   - Una excepción que se lanza en tiempo de compilación.
   - Ninguna de las anteriores.
5. La palabra clave `throws` se usa para lanzar una excepción en un método. Esta afirmación es:
   - Verdadera
   - Falsa
6. La forma correcta de usar la palabra clave `throw` en un método es:
   - throw new Exception("My exception");
   - throws new Exception();
   - throw Exception("My exception");
   - Ninguna de las anteriores.
7. Siempre que se lanza una excepción, es necesario añadir la palabra clave `throws` en la firma del método. Esta afirmación es:
   - Verdadera
   - Falsa

Suponga que tiene las siguientes clases:
```java

public class MyException extends Exception {
    
    public MyException(String message) {
        super(message);
    }
}


public class MyClass {
    
    int [] arr;
    
    public MyClass() {
        
        arr = new int[5];
        
        arr[0] = 1;
        arr[1] = 2;
        arr[2] = 3;
        arr[3] = 4;
        arr[4] = 5;
    }
    
    public int divide(int a, int b) {
        return a / b;
    }
    
    public int getLastElement() {
        return arr[arr.length];
    }
    
    public void throwException() throws MyException {
        throw new MyException("My exception");
    }
}

public class Main {
    
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        System.out.println(myClass.divide(5, 0));
        System.out.println(myClass.getLastElement());
        myClass.throwException();
    }
}
```
Responda las preguntas 8 a 9 sobre el código anterior:
8. ¿Qué excepción se lanza en el método `divide` al momento de ejecutar el método `main`?
   -  ArithmeticException
   -  ArrayIndexOutOfBoundsException
   -  IndexOutOfBoundsException
   -  NullPointerException
9. El método `getLastElement` lanza una excepción verificada (checked exception). Esta afirmación es:
   - Verdadera
   - Falsa
10. ¿Qué se debe agregar en el método `main` para que el código no termine abruptamente al lanzar alguna excepción?
    - Un bloque try-catch en el método `main`.
    - Un bloque try-finally
    - Un bloque try-catch-finally en el método `throwException` de la clase `MyClass`.
    - Ninguna de las anteriores

[Volver al índice](#indice)

## Enunciado

**Este taller toma como base el proyecto de la aplicación de música que se ha venido desarrollando en los talleres anteriores.**

Se debe permitir a los clientes de la aplicación de música seguir a sus artistas favoritos y crear listas de reproducción con sus canciones favoritas. Para esto, el programa debe permitir realizar las siguientes operaciones:

1. Seguir a un artista: Un cliente puede seguir a un artista. Si el usuario digita un id de artista que no existe, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"El artista con id ${id} no existe"_.</br></br>
2. Dejar de seguir a un artista: Un cliente puede dejar de seguir a un artista. El sistema debe mostrar los artistas a quien sigue y el usuario debe digitar el id del artista que desea dejar de seguir. Si el usuario digita un id de artista que no existe, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"El artista con id ${id} no existe en la lista de artistas del usuario"_. </br></br>
3. Agregar una lista de reproducción: Un cliente puede agregar una lista de reproducción. Si el nombre de la lista de reproducción es null, está vacío o contiene solo espacios en blanco, se debe lanzar una excepción de java (IllegalArgumentException) con el mensaje _"El nombre de la lista de reproducción no puede estar vacío o ser null"_.</br></br>
4. Eliminar una lista de reproducción: Un cliente puede eliminar una lista de reproducción. Si la lista de reproducción no existe, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"La playlist con id ${id} no existe en la lista del usuario"_.</br></br>
5. Agregar una canción a una lista de reproducción: Un cliente puede agregar una canción existente a una lista de reproducción del cliente. Si la lista de reproducción no existe, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"La playlist con id ${id} no existe en el usuario"_. En caso de que la canción no exista, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"La canción con id ${id} no existe"_.</br></br>
6. Eliminar una canción de una lista de reproducción: Un cliente puede eliminar una canción de una lista de reproducción del cliente. Si la lista de reproducción no existe, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"La playlist con id ${id} no existe en el usuario"_. En caso de que la canción no exista, se debe lanzar una excepción personalizada `NotFoundException` cuyo mensaje sea: _"La canción con id ${id} no existe en la lista de reproducción"_.</br></br>
7. Obtener la información de todas las listas de reproducción del cliente: Un cliente puede obtener la información de todas las listas de reproducción que ha creado. </br></br>
8. Obtener la información de todas las canciones de una lista de reproducción del cliente: Un cliente puede obtener la información de todas las canciones de una lista de reproducción que ha creado.</br></br>
9. Loggearse en la aplicación: Un cliente debe loggearse en la aplicación para poder realizar las operaciones anteriores. Si el cliente no se loggea correctamente, no debe mostrar el menú de opciones.</br></br>
10. Salir de la aplicación: Un cliente debe salir de la aplicación para finalizar la sesión. </br></br>

Para interactuar con el cliente, se recomienda seguir la estructura usada en el taller anterior, es decir, tener una vista que muestre las opciones al cliente y que llame a los métodos del controlador correspondiente.

Va a existir un nuevo paquete llamado `exception` que contendrá las excepciones personalizadas que se lanzarán en la aplicación.

Además, debe modificar el proyecto para que se cumplan las siguientes reglas de negocio:

1. Al momento de **eliminar un artista** se debe buscar el artista con el `id` proporcionado y eliminarlo de la lista de artistas. Si el artista no existe, debe lanzar una excepción `NotFoundException` y debe contener el mensaje: _"El artista con id <id> no existe"_. Si el `id` del artista proporcionado es `null`, está vacío o contiene solo espacios en blanco, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje _"El id del artista no puede estar vacío o ser null"_. **Si el artista es eliminado con éxito, se deben eliminar las canciones del artista y a su vez, eliminar las canciones de las listas de reproducción**.</br></br>
2. Al momento de **agregar un artista** se debe validar que el nombre proporcionado no sea nulo, esté vacío o contenga solo espacios en blanco. Si el nombre del artista no cumple con la validación, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje _"El nombre del artista no puede estar vacío o ser null"_. También debe validar que si el artista ya existe en la lista de artistas, debe lanzar una excepción personalizada llamada `AlreadyExistException` y debe contener el mensaje: _"El artista con nombre ${name} ya existe"_.</br></br>
3. Al momento de **agregar un cliente** se debe validar que el nombre de usuario, la contraseña, el nombre y el apellido no sean nulos, estén vacíos o contengan solo espacios en blanco. Si alguno de estos campos no cumple con la validación, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje "Los campos no pueden estar vacíos o ser null". También debe validar que: 
   - Si el nombre de usuario ya existe en la lista de clientes, debe lanzar una excepción personalizada llamada `AlreadyExistException` y debe contener el mensaje: _"El cliente con nombre de usuario ${username} ya existe_".
   - El nombre de usuario debe tener entre 8 y 10 caracteres y debe contener solo letras y números. De lo contrario, debe lanzar una excepción con el mensaje: _"El nombre de usuario debe tener entre 8 y 10 caracteres y debe contener solo letras y números"_.
   - La contraseña debe tener al menos 8 caracteres, una letra mayúscula, una letra minúscula, un número y un carácter especial entre los siguientes: _# ? ! @ $ % ^ & * -_.
   - La edad debe ser mayor a 14 años. De lo contrario, debe lanzar una excepción con el mensaje: "La edad debe ser mayor a 14 años".</br>

   **Si cumple con todas las condiciones, debe crear un objeto de la clase `Customer` con los datos proporcionados y agregarlo a la lista de clientes**.</br></br>
4. Al momento de **eliminar un cliente** se debe buscar el cliente con el `id` proporcionado y eliminarlo de la lista de clientes. Si el cliente no existe, debe lanzar una excepción `NotFoundException` y debe contener el mensaje: _"El cliente con id <id> no existe"_. Si el `id` del cliente proporcionado es `null`, está vacío o contiene solo espacios en blanco, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje "_El id del cliente no puede estar vacío o ser null"_.
**Si el cliente es eliminado con éxito, se deben eliminar sus listas de reproducción**. </br></br>
5. Al momento de **agregar una canción** se debe validar que el nombre, el género, y el álbum no sean nulos, estén vacíos o contengan solo espacios en blanco. Si alguno de estos campos no cumple con la validación, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje _"Los campos no pueden estar vacíos o ser null"_. Por otro lado, si la duración es menor a 0, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje _"La duración de la canción no puede ser menor a 0"_.</br></br>
6. Al momento de **eliminar una canción** se debe buscar la canción con el `id` proporcionado y eliminarla de la lista de canciones. Si la canción no existe, debe lanzar una excepción `NotFoundException` y debe contener el mensaje: _"La canción con id <id> no existe"_. Si el `id` de la canción proporcionado es `null`, está vacío o contiene solo espacios en blanco, debe lanzar una excepción de java `IllegalArgumentException` con el mensaje "_El id de la canción no puede estar vacío o ser null"_. **Si la canción es eliminada con éxito, se deben eliminar la canción de las listas de reproducción**.</br></br>

[Volver al índice](#indice)

## Calificación

El programa debe compilar y ejecutar sin errores. Se debe cumplir con los siguientes requerimientos:

1. Las clases deben estar en los paquetes correctos (servicios, controllers, vistas, modelos y excepciones).(0.5)
2. La clase `Main` y las clases del paquete `views` son las únicas que pueden interactuar con el usuario (hacer print y usar scanner).(0.5)
3. Los controladores deben llamar a los métodos de los servicios correspondientes.(0.5)
4. Los servicios deben llamar a los métodos de las clases del paquete `models` correspondientes.(0.5)
5. El programa debe permitir al cliente loggearse en la aplicación.(0.5)
6. El programa debe capturar las excepciones que se lanzan en los controladores y mostrar los mensajes de error correspondientes de acuerdo a las reglas del negocio.(1.0)
7. El programa debe permitir seguir a un artista, dejar de seguir a un artista, agregar una lista de reproducción, eliminar una lista de reproducción, agregar una canción a una lista de reproducción y eliminar una canción de una lista de reproducción.(1.5)

**Este taller hace parte de su proyecto. Los posteriores talleres no se calificarán hasta que se haya completado este.
Si todo está correcto, sumará 1.0 a su proyecto final.
Este taller debe ser entregado durante la semana 12**

## ¿Qué sigue?

En el proyecto la carga de datos es manual. En el siguiente taller, se trabajará en la carga de datos desde un archivo de texto y serialización de objetos. Además, se trabajará en la persistencia de datos en texto y binario.

## Recursos en línea

- [Excepciones en Java](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html) [Artículo]
- [Excepciones personalizadas en Java](https://www.baeldung.com/java-new-custom-exception) [Artículo]
- [Excepciones en Java](https://www.geeksforgeeks.org/exceptions-in-java/) [Artículo]
- [Java: Introducción a excepciones](https://www.youtube.com/watch?v=kGzwPunAOxk&) [Video]
- [Java: throw y throws, usos y diferencias](https://www.youtube.com/watch?v=-xC0o6JQaoE) [Video]