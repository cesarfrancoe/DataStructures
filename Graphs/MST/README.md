## **Árboles de Expansión Mínimos**

Los **árboles de expansión mínimos** son árboles que conectan todos los vértices de un grafo ponderado con el menor costo total posible. Este concepto es fundamental en aplicaciones como la planificación de redes de comunicaciones, redes eléctricas, y rutas de transporte, donde se busca conectar todos los puntos de manera eficiente en términos de costos.

Un **árbol de expansión mínimo** (MST, por sus siglas en inglés) es un subconjunto de las aristas de un grafo conectado y ponderado que conecta todos los vértices sin formar ciclos y cuyo peso total es el mínimo posible.

### Algoritmos para encontrar árboles de expansión mínimos

- **[Algoritmo de Prim](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/Prim_algorithm.md)**
- **[Algoritmo de Boruvka](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/Boruvka_algorithm.md)**
- **[Algoritmo de Kruskal](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/Kruskal_algorithm.md)**
- **[Algoritmo de Edmonds-Karp](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/MST/Edmon_Karp_Algorithm.md)**

### **Comparación de Algoritmos de Árboles de Expansión Mínimos**

| **Características**         | **Prim**                                                | **Boruvka**                                              | **Kruskal**                                              | **Edmonds-Karp**                                          |
|-----------------------------|--------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------|
| **Tipo de grafo**           | Conectado y ponderado                                  | Conectado y ponderado                                    | Conectado y ponderado                                    | Conectado y ponderado                                    |
| **Estrategia**              | Crecimiento de un árbol a partir de un vértice inicial | Unión de componentes conexos en cada iteración           | Selección de aristas de menor peso para formar el árbol | Encontrar el flujo máximo en redes de flujo, utilizado también para encontrar el MST |
| **Complejidad temporal**    | \( O(E \log V) \) (usando montículo de Fibonacci)        | \( O(E \log V) \)                                        | \( O(E \log V) \) (usando un algoritmo de búsqueda en conjuntos) | \( O(VE^2) \) (usando una búsqueda en anchura)          |
| **Complejidad espacial**    | \( O(V + E) \) (almacenamiento del grafo y distancias) | \( O(V + E) \)                                           | \( O(V + E) \)                                           | \( O(V + E) \) (almacenamiento de flujo residual)     |
| **Forma de iteración**      | Itera sobre los vértices                             | Itera sobre las aristas, creando componentes conexos     | Itera sobre las aristas, utilizando una estructura de unión-find | Utiliza una búsqueda en anchura para encontrar el flujo máximo |
| **Ventajas**                | - Funciona bien con grafos densos                      | - Eficiente para grafos dispersos                         | - Conceptualmente simple y eficiente en grafos dispersos | - Eficiente en grafos densos y grandes flujos de red   |
| **Desventajas**             | - No es eficiente en grafos dispersos                   | - Puede ser más lento en grafos densos                    | - Necesita ordenar todas las aristas antes de comenzar   | - Más complejo y con una mayor complejidad temporal comparado con otros algoritmos |
