## **Costo Mínimo**

El costo mínimo en grafos se refiere a la búsqueda de la ruta más corta o menos costosa entre dos vértices, considerando que cada arista puede tener un costo asociado (peso). Este concepto es fundamental en diversas aplicaciones, como la planificación de rutas, la optimización de redes y el análisis de costos en sistemas de transporte.

- [Algoritmo de Dijkstra](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/Dijkstra_algorithm.md)
- [Algoritmo de Bellman-Ford](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/Bellman_Ford_algorithm.md)
- [Algoritmo de Floyd-Warshall](https://github.com/cesarfrancoe/DataStructures/blob/main/Graphs/Floyd_Warshall_algorithm.md)

### **Comparación de Algoritmos de Costo Mínimo**

| **Características**       | **Dijkstra**                                             | **Bellman-Ford**                                        | **Floyd-Warshall**                                      |
|---------------------------|---------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------------|
| **Tipo de grafo**        | Ponderado, no negativo (no se permiten aristas negativas) | Ponderado (puede incluir aristas negativas)            | Ponderado (puede incluir aristas negativas)            |
| **Complejidad temporal** | \( O((V + E) \log V) \) (usando montículo de Fibonacci) | \( O(VE) \)                                            | \( O(V^3) \)                                           |
| **Complejidad espacial** | \( O(V) \) (almacenamiento de distancias y cola de prioridad) | \( O(V) \) (almacenamiento de distancias)             | \( O(V^2) \) (matriz de distancias)                   |
| **Ciclos negativos**     | No soporta ciclos negativos                              | Soporta ciclos negativos (detecta su existencia)      | Soporta ciclos negativos (detecta su existencia)      |
| **Uso típico**           | Rutas más cortas desde un solo origen                   | Rutas más cortas desde un solo origen, incluyendo aristas negativas | Rutas más cortas entre todos los pares de vértices |
| **Ventajas**             | - Eficiente para grafos densos                          | - Puede manejar aristas negativas                       | - Encuentra distancias más cortas entre todos los pares |
| **Desventajas**          | - No puede manejar aristas negativas                     | - Más lento que Dijkstra en grafos densos             | - Más lento en comparación con Dijkstra y Bellman-Ford en grafos grandes |

