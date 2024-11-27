## **Conjuntos**

### **Introducción**

Un **conjunto** es una colección de elementos no ordenados y **sin elementos repetidos**. Los conjuntos son fundamentales en la teoría de conjuntos, un área de la matemática que se utiliza para estudiar colecciones de objetos. En la programación, los conjuntos se utilizan para representar colecciones de elementos únicos, eliminar duplicados, realizar operaciones de unión, intersección y diferencia, entre otras tareas.

### Características de los Conjuntos:
- **No permiten duplicados**: Un conjunto no puede contener el mismo elemento más de una vez. Si se intenta agregar un elemento que ya está presente, el conjunto no cambiará.
- **Orden no garantizado**: Los elementos dentro de un conjunto no tienen un orden específico.
- **Operaciones de Conjunto**: Los conjuntos soportan operaciones típicas de teoría de conjuntos, como:
  - **Unión**: Combina los elementos de dos conjuntos.
  - **Intersección**: Obtiene los elementos comunes entre dos conjuntos.
  - **Diferencia**: Obtiene los elementos que están en un conjunto pero no en otro.
  - **Subconjunto**: Verifica si un conjunto es un subconjunto de otro.
  - **Simetría**: Encuentra los elementos que están en uno de los conjuntos, pero no en ambos.

### Tipos de Conjuntos en Programación:

En la mayoría de los lenguajes de programación, los conjuntos pueden implementarse de diferentes maneras. Algunos de los tipos comunes de conjuntos incluyen:

1. **Conjuntos en Python**: En Python, los conjuntos están implementados como el tipo `set`.
2. **Conjuntos en Java**: En Java, los conjuntos pueden ser implementados utilizando la interfaz `Set` y las clases como `HashSet`, `TreeSet`, etc.

### **Operaciones Básicas con Conjuntos**:

- **Crear un conjunto**: Un conjunto vacío o uno con elementos iniciales.
- **Agregar elementos**: Insertar nuevos elementos en el conjunto.
- **Eliminar elementos**: Quitar elementos específicos.
- **Verificar pertenencia**: Comprobar si un elemento pertenece al conjunto.

### **Ejemplo en Python**:

```python
# Crear un conjunto
conjunto_a = {1, 2, 3, 4, 5}

# Agregar un elemento
conjunto_a.add(6)

# Eliminar un elemento
conjunto_a.remove(2)

# Verificar si un elemento está en el conjunto
print(3 in conjunto_a)  # True

# Operación de unión
conjunto_b = {4, 5, 6, 7}
union_conjuntos = conjunto_a | conjunto_b  # {1, 3, 4, 5, 6, 7}

# Operación de intersección
interseccion_conjuntos = conjunto_a & conjunto_b  # {4, 5, 6}

# Operación de diferencia
diferencia_conjuntos = conjunto_a - conjunto_b  # {1, 3}
```

### **Ejemplo en Java**:

```java
import java.util.HashSet;
import java.util.Set;

public class ConjuntoEjemplo {
    public static void main(String[] args) {
        // Crear un conjunto
        Set<Integer> conjuntoA = new HashSet<>();
        conjuntoA.add(1);
        conjuntoA.add(2);
        conjuntoA.add(3);
        conjuntoA.add(4);
        conjuntoA.add(5);

        // Agregar un elemento
        conjuntoA.add(6);

        // Eliminar un elemento
        conjuntoA.remove(2);

        // Verificar si un elemento está en el conjunto
        System.out.println(conjuntoA.contains(3));  // true

        // Operación de unión
        Set<Integer> conjuntoB = new HashSet<>();
        conjuntoB.add(4);
        conjuntoB.add(5);
        conjuntoB.add(6);
        conjuntoB.add(7);
        Set<Integer> unionConjuntos = new HashSet<>(conjuntoA);
        unionConjuntos.addAll(conjuntoB);  // {1, 3, 4, 5, 6, 7}

        // Operación de intersección
        Set<Integer> interseccionConjuntos = new HashSet<>(conjuntoA);
        interseccionConjuntos.retainAll(conjuntoB);  // {4, 5, 6}

        // Operación de diferencia
        Set<Integer> diferenciaConjuntos = new HashSet<>(conjuntoA);
        diferenciaConjuntos.removeAll(conjuntoB);  // {1, 3}
    }
}
```
Aquí tienes el subtema **Operaciones con Conjuntos** para el tema **Conjuntos y Diccionarios**:

---

### **Operaciones con Conjuntos**

Los **conjuntos** permiten una variedad de operaciones que se utilizan para manipular y comparar colecciones de elementos. Estas operaciones son fundamentales en la teoría de conjuntos y son ampliamente utilizadas en programación para resolver problemas relacionados con la agregación, la comparación y la manipulación de datos.

#### **Operaciones Básicas**

1. **Unión**:
   - La **unión** de dos conjuntos consiste en un nuevo conjunto que contiene todos los elementos de ambos conjuntos, sin repetir elementos.
   - **Notación**: \( A \cup B \)

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3}
   conjunto_b = {3, 4, 5}
   union = conjunto_a | conjunto_b  # {1, 2, 3, 4, 5}
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3));
   Set<Integer> conjuntoB = new HashSet<>(Arrays.asList(3, 4, 5));
   Set<Integer> unionConjuntos = new HashSet<>(conjuntoA);
   unionConjuntos.addAll(conjuntoB);  // {1, 2, 3, 4, 5}
   ```

2. **Intersección**:
   - La **intersección** de dos conjuntos consiste en un nuevo conjunto que contiene solo los elementos comunes entre ambos conjuntos.
   - **Notación**: \( A \cap B \)

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3}
   conjunto_b = {3, 4, 5}
   interseccion = conjunto_a & conjunto_b  # {3}
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3));
   Set<Integer> conjuntoB = new HashSet<>(Arrays.asList(3, 4, 5));
   Set<Integer> interseccionConjuntos = new HashSet<>(conjuntoA);
   interseccionConjuntos.retainAll(conjuntoB);  // {3}
   ```

3. **Diferencia**:
   - La **diferencia** de dos conjuntos consiste en un nuevo conjunto que contiene los elementos de un conjunto que no están en el otro conjunto.
   - **Notación**: \( A - B \)

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3}
   conjunto_b = {3, 4, 5}
   diferencia = conjunto_a - conjunto_b  # {1, 2}
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3));
   Set<Integer> conjuntoB = new HashSet<>(Arrays.asList(3, 4, 5));
   Set<Integer> diferenciaConjuntos = new HashSet<>(conjuntoA);
   diferenciaConjuntos.removeAll(conjuntoB);  // {1, 2}
   ```

4. **Diferencia Simétrica**:
   - La **diferencia simétrica** entre dos conjuntos consiste en un nuevo conjunto que contiene los elementos que están en uno de los conjuntos o en el otro, pero no en ambos.
   - **Notación**: \( A \Delta B \)

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3}
   conjunto_b = {3, 4, 5}
   diferencia_simetrica = conjunto_a ^ conjunto_b  # {1, 2, 4, 5}
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3));
   Set<Integer> conjuntoB = new HashSet<>(Arrays.asList(3, 4, 5));
   Set<Integer> diferenciaSimetricaConjuntos = new HashSet<>(conjuntoA);
   diferenciaSimetricaConjuntos.addAll(conjuntoB);
   Set<Integer> interseccion = new HashSet<>(conjuntoA);
   interseccion.retainAll(conjuntoB);
   diferenciaSimetricaConjuntos.removeAll(interseccion);  // {1, 2, 4, 5}
   ```

5. **Subconjunto**:
   - Un conjunto \( A \) es un **subconjunto** de otro conjunto \( B \) si todos los elementos de \( A \) están también en \( B \).
   - **Notación**: \( A \subseteq B \)

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2}
   conjunto_b = {1, 2, 3, 4, 5}
   es_subconjunto = conjunto_a.issubset(conjunto_b)  # True
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2));
   Set<Integer> conjuntoB = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
   boolean esSubconjunto = conjuntoB.containsAll(conjuntoA);  // true
   ```

6. **Superconjunto**:
   - Un conjunto \( A \) es un **superconjunto** de otro conjunto \( B \) si \( B \) es un subconjunto de \( A \).
   - **Notación**: \( A \supseteq B \)

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3, 4, 5}
   conjunto_b = {1, 2}
   es_superconjunto = conjunto_a.issuperset(conjunto_b)  # True
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
   Set<Integer> conjuntoB = new HashSet<>(Arrays.asList(1, 2));
   boolean esSuperconjunto = conjuntoA.containsAll(conjuntoB);  // true
   ```

### **Operaciones Avanzadas**

1. **Copia de un Conjunto**:
   - Crear una copia de un conjunto sin afectar al original.

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3}
   copia_conjunto = conjunto_a.copy()  # {1, 2, 3}
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3));
   Set<Integer> copiaConjunto = new HashSet<>(conjuntoA);  // {1, 2, 3}
   ```

2. **Limpiar un Conjunto**:
   - Eliminar todos los elementos de un conjunto.

   **Ejemplo en Python**:
   ```python
   conjunto_a = {1, 2, 3}
   conjunto_a.clear()  # set()
   ```

   **Ejemplo en Java**:
   ```java
   Set<Integer> conjuntoA = new HashSet<>(Arrays.asList(1, 2, 3));
   conjuntoA.clear();  // set is now empty
   ```

