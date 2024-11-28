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

### **Operaciones Comunes con Diccionarios**

Los diccionarios permiten realizar diversas operaciones básicas que se utilizan para manipular los pares clave-valor. Algunas de las operaciones más comunes incluyen:

- **Crear un diccionario**: Crear un diccionario vacío o con pares de clave-valor iniciales.
- **Agregar pares de clave-valor**: Insertar un nuevo par clave-valor en el diccionario.
- **Eliminar pares de clave-valor**: Eliminar un par clave-valor del diccionario.
- **Acceder a valores**: Obtener el valor asociado a una clave específica.
- **Verificar existencia de una clave**: Comprobar si una clave existe en el diccionario.
