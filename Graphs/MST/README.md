## **Árboles de Expansión Mínimos**

Los **árboles de expansión mínimos** son árboles que conectan todos los vértices de un grafo ponderado con el menor costo total posible. Este concepto es fundamental en aplicaciones como la planificación de redes de comunicaciones, redes eléctricas, y rutas de transporte, donde se busca conectar todos los puntos de manera eficiente en términos de costos.

Un **árbol de expansión mínimo** (MST, por sus siglas en inglés) es un subconjunto de las aristas de un grafo conectado y ponderado que conecta todos los vértices sin formar ciclos y cuyo peso total es el mínimo posible.

### Algoritmos para encontrar árboles de expansión mínimos

- **[Algoritmo de Prim](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/MST/Prim_algorithm.md)**
- **[Algoritmo de Boruvka](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/MST/Boruvka_algorithm.md)**
- **[Algoritmo de Kruskal](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/MST/Kruskal_algorithm.md)**

### **Comparación de Algoritmos de Árboles de Expansión Mínimos**

| **Características**         | **Prim**                                                | **Boruvka**                                              | **Kruskal**                                              |
|-----------------------------|--------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------|
| **Tipo de grafo**           | Conectado y ponderado                                  | Conectado y ponderado                                    | Conectado y ponderado                                    |
| **Estrategia**              | Crecimiento de un árbol a partir de un vértice inicial | Unión de componentes conexos en cada iteración           | Selección de aristas de menor peso para formar el árbol |
| **Complejidad temporal**    | \( O(E \log V) \) (usando una cola de prioridad)        | \( O(E \log V) \)                                        | \( O(E \log V) \) (usando un algoritmo de búsqueda en conjuntos) |
| **Complejidad espacial**    | \( O(V + E) \) (almacenamiento del grafo y distancias) | \( O(V + E) \)                                           | \( O(V + E) \)                                           |
| **Forma de iteración**      | Itera sobre los vértices                             | Itera sobre las aristas, creando componentes conexos     | Itera sobre las aristas, utilizando una estructura de unión-find |
| **Ventajas**                | - Funciona bien con grafos densos                      | - Eficiente para grafos dispersos                         | - Conceptualmente simple y eficiente en grafos dispersos |
| **Desventajas**             | - No es eficiente en grafos dispersos                   | - Puede ser más lento en grafos densos                    | - Necesita ordenar todas las aristas antes de comenzar   |

