## **Algoritmo de Floyd-Warshall**

El algoritmo de Floyd-Warshall es un método utilizado para encontrar las distancias más cortas entre todos los pares de vértices en un grafo ponderado. Este algoritmo es especialmente útil para grafos densos y puede manejar aristas con pesos negativos, siempre que no haya ciclos negativos.

### **Descripción del Algoritmo:**
1. **Inicialización**:
   - Crear una matriz de distancias y establecer la distancia entre cada par de vértices. La distancia de un vértice a sí mismo se establece en 0, y la distancia entre vértices conectados directamente se establece en el peso de la arista. Si no hay conexión directa, se establece como infinito.

2. **Relajación**:
   - Para cada vértice intermedio, actualizar la matriz de distancias revisando si una ruta que pasa por este vértice intermedio es más corta que la ruta directa entre los dos vértices.

3. **Repetir**:
   - Repetir el proceso para cada vértice como posible vértice intermedio.

### **Ejemplo en Python con Listas de Adyacencia**:

```python
class Graph:
    def __init__(self):
        self.adjacency_list = {}

    def add_vertex(self, vertex):
        if vertex not in self.adjacency_list:
            self.adjacency_list[vertex] = []

    def add_edge(self, u, v, weight):
        self.add_vertex(u)
        self.add_vertex(v)
        self.adjacency_list[u].append((v, weight))

    def floyd_warshall(self):
        # Initialize the distance matrix
        distance = {u: {v: float('inf') for v in self.adjacency_list} for u in self.adjacency_list}

        for u in self.adjacency_list:
            distance[u][u] = 0  # Distance to self is 0
            for v, weight in self.adjacency_list[u]:
                distance[u][v] = weight  # Set the initial distances

        # Update distances
        for k in self.adjacency_list:
            for i in self.adjacency_list:
                for j in self.adjacency_list:
                    if distance[i][j] > distance[i][k] + distance[k][j]:
                        distance[i][j] = distance[i][k] + distance[k][j]

        return distance

# Usage
g = Graph()
g.add_edge('A', 'B', 3)
g.add_edge('A', 'C', 8)
g.add_edge('B', 'C', 2)
g.add_edge('B', 'D', 5)
g.add_edge('C', 'D', 1)

distances = g.floyd_warshall()
print("Distance matrix:")
for u in distances:
    print(u, distances[u])
```

### **Ejemplo en Java con Listas de Adyacencia**:

```java
import java.util.*;

class Graph {
    private Map<String, List<Pair<String, Integer>>> adjacencyList;

    public Graph() {
        adjacencyList = new HashMap<>();
    }

    public void addVertex(String vertex) {
        adjacencyList.putIfAbsent(vertex, new ArrayList<>());
    }

    public void addEdge(String u, String v, int weight) {
        addVertex(u);
        addVertex(v);
        adjacencyList.get(u).add(new Pair<>(v, weight));
    }

    public Map<String, Map<String, Integer>> floydWarshall() {
        // Initialize the distance matrix
        var distance = new HashMap<String, Map<String, Integer>>();
        
        for (var u : adjacencyList.keySet()) {
            var distances = new HashMap<String, Integer>();
            for (var v : adjacencyList.keySet()) {
                distances.put(v, Integer.MAX_VALUE);
            }
            distances.put(u, 0); // Distance to self is 0
            
            for (var neighbor : adjacencyList.get(u)) {
                distances.put(neighbor.getKey(), neighbor.getValue()); // Set initial distances
            }
            distance.put(u, distances);
        }

        // Update distances
        for (var k : adjacencyList.keySet()) {
            for (var i : adjacencyList.keySet()) {
                for (var j : adjacencyList.keySet()) {
                    if (distance.get(i).get(j) > distance.get(i).get(k) + distance.get(k).get(j)) {
                        distance.get(i).put(j, distance.get(i).get(k) + distance.get(k).get(j));
                    }
                }
            }
        }

        return distance;
    }

    public static void main(String[] args) {
        var g = new Graph();
        g.addEdge("A", "B", 3);
        g.addEdge("A", "C", 8);
        g.addEdge("B", "C", 2);
        g.addEdge("B", "D", 5);
        g.addEdge("C", "D", 1);

        var distances = g.floydWarshall();
        System.out.println("Distance matrix:");
        for (var u : distances.keySet()) {
            System.out.println(u + " " + distances.get(u));
        }
    }
}

// Helper class for Pair
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
}
```

### **Ejemplo en Python con Matrices de Adyacencia**:

```python
class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        self.adjacency_matrix = [[float('inf')] * num_vertices for _ in range(num_vertices)]

        for i in range(num_vertices):
            self.adjacency_matrix[i][i] = 0  # Distance to self is 0

    def add_edge(self, u, v, weight):
        self.adjacency_matrix[u][v] = weight

    def floyd_warshall(self):
        distance = [[self.adjacency_matrix[i][j] for j in range(self.num_vertices)] for i in range(self.num_vertices)]

        # Update distances
        for k in range(self.num_vertices):
            for i in range(self.num_vertices):
                for j in range(self.num_vertices):
                    if distance[i][j] > distance[i][k] + distance[k][j]:
                        distance[i][j] = distance[i][k] + distance[k][j]

        return distance

# Usage
g = Graph(4)
g.add_edge(0, 1, 3)
g.add_edge(0, 2, 8)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 5)
g.add_edge(2, 3, 1)

distances = g.floyd_warshall()
print("Distance matrix:")
for row in distances:
    print(row)
```

### **Ejemplo en Java con Matrices de Adyacencia**:

```java
class Graph {
    private int[][] adjacencyMatrix;
    private int numVertices;

    public Graph(int numVertices) {
        this.numVertices = numVertices;
        adjacencyMatrix = new int[numVertices][numVertices];

        for (int i = 0; i < numVertices; i++) {
            for (int j = 0; j < numVertices; j++) {
                adjacencyMatrix[i][j] = Integer.MAX_VALUE; // Initialize as infinite
            }
            adjacencyMatrix[i][i] = 0; // Distance to self is 0
        }
    }

    public void addEdge(int u, int v, int weight) {
        adjacencyMatrix[u][v] = weight;
    }

    public int[][] floydWarshall() {
        int[][] distance = new int[numVertices][numVertices];
        
        for (int i = 0; i < numVertices; i++) {
            for (int j = 0; j < numVertices; j++) {
                distance[i][j] = adjacencyMatrix[i][j];
            }
        }

        // Update distances
        for (int k = 0; k < numVertices; k++) {
            for (int i = 0; i < numVertices; i++) {
                for (int j = 0; j < numVertices; j++) {
                    if (distance[i][j] > distance[i][k] + distance[k][j]) {
                        distance[i][j] = distance[i][k] + distance[k][j];
                    }
                }
            }
        }

        return distance;
    }

    public static void main(String[] args) {
        var g = new Graph(4);
        g.addEdge(0, 1, 3);
        g.addEdge(0, 2, 8);
        g.addEdge(1, 2, 2);
        g.addEdge(1, 3, 5);
        g.addEdge(2, 3, 1);

        int[][] distances = g.floydWarshall();
        System.out.println("Distance matrix:");
        for (int[] row : distances) {
            System.out.println(Arrays.toString(row));
        }
    }
}
```
