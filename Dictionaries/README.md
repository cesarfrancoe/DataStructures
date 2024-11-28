## **Diccionarios (Dictionaries)**

### **Introducción**

Un **diccionario** es una estructura de datos que permite almacenar elementos en forma de pares de **clave-valor (key-value)**. A diferencia de los conjuntos, que almacenan elementos únicos sin asociarlos entre sí, los diccionarios permiten asociar un valor con una clave única, lo que facilita la búsqueda, inserción y eliminación de elementos de manera eficiente.

Los diccionarios son fundamentales en muchos algoritmos y aplicaciones de programación. Se utilizan ampliamente en tareas que requieren una rápida búsqueda y recuperación de datos, como bases de datos, tablas de símbolos, procesamiento de textos, y almacenamiento de configuraciones o preferencias en aplicaciones.

### Características de los Diccionarios:
- **Claves únicas**: Cada clave dentro del diccionario debe ser única. No puede haber claves duplicadas.
- **Acceso rápido a los valores**: El acceso a los valores asociados con una clave es muy eficiente, lo que hace que los diccionarios sean ideales para situaciones donde se necesita hacer búsquedas rápidas.
- **No tienen un orden específico**: Aunque algunas implementaciones de diccionarios (como los diccionarios ordenados) mantienen un orden, en general, los diccionarios no garantizan que los elementos estén ordenados.

### Tipos de Diccionarios en Programación:

1. **Diccionarios en Python: `dict`**

   En Python, los diccionarios se implementan como el tipo `dict`, lo que permite almacenar pares de clave-valor. Son muy flexibles y fáciles de usar.

   **Ejemplo en Python**:
   ```python
   # Create a dictionary
   dictionary = {'key1': 'value1', 'key2': 'value2'}

   # Add a new key-value pair
   dictionary['key3'] = 'value3'

   # Remove a key-value pair
   del dictionary['key2']

   # Access a value using a key
   print(dictionary['key1'])  # 'value1'

   # Check if a key exists
   print('key3' in dictionary)  # True

   # Get all values
   print(dictionary.values())  # dict_values(['value1', 'value3'])
   ```

   En este ejemplo:
   - Se crea un diccionario con claves `key1` y `key2`, cada una asociada a un valor.
   - Se agrega un nuevo par clave-valor con `key3` y su respectivo valor.
   - Se elimina el par con `key2`.
   - Se accede a un valor utilizando su clave (`key1`).
   - Se verifica si `key3` está presente en el diccionario con `in`.
   - Se obtiene una lista de todos los valores almacenados en el diccionario.

2. **Diccionarios en Java: `HashMap`**

   En Java, los diccionarios pueden implementarse utilizando la clase `HashMap`, que almacena pares clave-valor. `HashMap` proporciona un acceso eficiente y no garantiza el orden de los elementos.

   **Ejemplo en Java**:
   ```java
   import java.util.HashMap;

   public class DictionaryExample {
       public static void main(String[] args) {
           // Create a dictionary
           HashMap<String, String> dictionary = new HashMap<>();
           dictionary.put("key1", "value1");
           dictionary.put("key2", "value2");
   
           // Add a new key-value pair
           dictionary.put("key3", "value3");
   
           // Remove a key-value pair
           dictionary.remove("key2");
   
           // Access a value using a key
           System.out.println(dictionary.get("key1"));  // 'value1'
   
           // Check if a key exists
           System.out.println(dictionary.containsKey("key3"));  // true
   
           // Get all values
           System.out.println(dictionary.values());  // [value1, value3]
       }
   }
   ```

   En este ejemplo:
   - Se crea un diccionario de tipo `HashMap` con claves `key1` y `key2`, asociadas a los valores `value1` y `value2`.
   - Se agrega un nuevo par clave-valor con `key3` y `value3`.
   - Se elimina el par con `key2`.
   - Se accede al valor de `key1` con `get()`.
   - Se verifica si `key3` está presente en el diccionario con `containsKey()`.
   - Se obtiene una colección con todos los valores almacenados con `values()`.

---

### **Operaciones Comunes con Diccionarios**

Los diccionarios permiten realizar diversas operaciones básicas que se utilizan para manipular los pares clave-valor. A continuación, se muestran ejemplos de las operaciones más comunes:

#### **1. Crear un Diccionario**

- **En Python**: 
  Puedes crear un diccionario vacío o inicializarlo con pares clave-valor.
  
  **Ejemplo en Python**:
  ```python
  # Crear un diccionario vacío
  dictionary = {}

  # Crear un diccionario con pares clave-valor
  dictionary = {'key1': 'value1', 'key2': 'value2'}
  print(dictionary)  # {'key1': 'value1', 'key2': 'value2'}
  ```

- **En Java**: 
  En Java, puedes crear un `HashMap` vacío o inicializarlo con pares clave-valor.

  **Ejemplo en Java**:
  ```java
  import java.util.HashMap;

  public class CreateDictionary {
      public static void main(String[] args) {
          // Crear un diccionario vacío
          HashMap<String, String> dictionary = new HashMap<>();
          
          // Crear un diccionario con pares clave-valor
          dictionary.put("key1", "value1");
          dictionary.put("key2", "value2");
          
          System.out.println(dictionary);  // {key1=value1, key2=value2}
      }
  }
  ```

#### **2. Agregar Pares de Clave-Valor**

- **En Python**: 
  Puedes agregar un nuevo par clave-valor a un diccionario utilizando la notación de corchetes.

  **Ejemplo en Python**:
  ```python
  dictionary = {'key1': 'value1'}
  
  # Agregar un nuevo par clave-valor
  dictionary['key2'] = 'value2'
  print(dictionary)  # {'key1': 'value1', 'key2': 'value2'}
  ```

- **En Java**: 
  Puedes usar el método `put()` de `HashMap` para agregar un nuevo par clave-valor.

  **Ejemplo en Java**:
  ```java
  import java.util.HashMap;

  public class AddPairToDictionary {
      public static void main(String[] args) {
          HashMap<String, String> dictionary = new HashMap<>();
          
          // Agregar un nuevo par clave-valor
          dictionary.put("key1", "value1");
          dictionary.put("key2", "value2");
          
          System.out.println(dictionary);  // {key1=value1, key2=value2}
      }
  }
  ```

#### **3. Eliminar Pares de Clave-Valor**

- **En Python**: 
  Puedes eliminar un par clave-valor usando `del` o el método `pop()`.

  **Ejemplo en Python**:
  ```python
  dictionary = {'key1': 'value1', 'key2': 'value2'}
  
  # Eliminar un par clave-valor utilizando del
  del dictionary['key2']
  
  # O utilizando pop()
  dictionary.pop('key1')
  
  print(dictionary)  # {}
  ```

- **En Java**: 
  En Java, puedes eliminar un par clave-valor utilizando el método `remove()` de `HashMap`.

  **Ejemplo en Java**:
  ```java
  import java.util.HashMap;

  public class RemovePairFromDictionary {
      public static void main(String[] args) {
          HashMap<String, String> dictionary = new HashMap<>();
          dictionary.put("key1", "value1");
          dictionary.put("key2", "value2");
          
          // Eliminar un par clave-valor
          dictionary.remove("key1");
          
          System.out.println(dictionary);  // {key2=value2}
      }
  }
  ```

#### **4. Acceder a Valores usando una Clave**

- **En Python**: 
  Puedes acceder al valor de un diccionario utilizando la clave dentro de corchetes o el método `get()`.

  **Ejemplo en Python**:
  ```python
  dictionary = {'key1': 'value1', 'key2': 'value2'}
  
  # Acceder a un valor usando una clave
  print(dictionary['key1'])  # 'value1'
  
  # Usando get()
  print(dictionary.get('key2'))  # 'value2'
  ```

- **En Java**: 
  En Java, puedes acceder al valor de un `HashMap` utilizando el método `get()`.

  **Ejemplo en Java**:
  ```java
  import java.util.HashMap;

  public class AccessValueFromDictionary {
      public static void main(String[] args) {
          HashMap<String, String> dictionary = new HashMap<>();
          dictionary.put("key1", "value1");
          dictionary.put("key2", "value2");
          
          // Acceder a un valor usando una clave
          System.out.println(dictionary.get("key1"));  // 'value1'
      }
  }
  ```

#### **5. Verificar la Existencia de una Clave**

- **En Python**: 
  Puedes verificar si una clave está presente en un diccionario utilizando el operador `in` o el método `get()`.

  **Ejemplo en Python**:
  ```python
  dictionary = {'key1': 'value1', 'key2': 'value2'}
  
  # Verificar si una clave existe
  print('key1' in dictionary)  # True
  print(dictionary.get('key3'))  # None (si no existe)
  ```

- **En Java**: 
  En Java, puedes verificar la existencia de una clave en un `HashMap` utilizando el método `containsKey()`.

  **Ejemplo en Java**:
  ```java
  import java.util.HashMap;

  public class CheckKeyExistence {
      public static void main(String[] args) {
          HashMap<String, String> dictionary = new HashMap<>();
          dictionary.put("key1", "value1");
          dictionary.put("key2", "value2");
          
          // Verificar si una clave existe
          System.out.println(dictionary.containsKey("key1"));  // true
          System.out.println(dictionary.containsKey("key3"));  // false
      }
  }
  ```

#### **6. Obtener Todos los Valores del Diccionario**

- **En Python**: 
  Puedes obtener todos los valores utilizando el método `values()`.

  **Ejemplo en Python**:
  ```python
  dictionary = {'key1': 'value1', 'key2': 'value2'}
  
  # Obtener todos los valores
  print(dictionary.values())  # dict_values(['value1', 'value2'])
  ```

- **En Java**: 
  En Java, puedes obtener todos los valores usando el método `values()` de `HashMap`.

  **Ejemplo en Java**:
  ```java
  import java.util.HashMap;

  public class GetAllValues {
      public static void main(String[] args) {
          HashMap<String, String> dictionary = new HashMap<>();
          dictionary.put("key1", "value1");
          dictionary.put("key2", "value2");
          
          // Obtener todos los valores
          System.out.println(dictionary.values());  // [value1, value2]
      }
  }
  ```

