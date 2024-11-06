## **Algoritmo de Bellman-Ford**

El algoritmo de Bellman-Ford es otro método utilizado para encontrar la ruta más corta desde un vértice fuente a todos los demás vértices en un grafo. A diferencia del algoritmo de Dijkstra, el algoritmo de Bellman-Ford puede manejar aristas con pesos negativos, aunque no se puede usar en grafos que contengan ciclos negativos.

### **Descripción del Algoritmo:**
1. **Inicialización**:
   - Establecer la distancia del vértice fuente a sí mismo como 0 y a todos los demás vértices como infinito.

2. **Relajación**:
   - Para cada arista en el grafo, actualizar la distancia de los vértices si se encuentra una distancia más corta.

3. **Repetir**:
   - Repetir el proceso de relajación para todos los vértices, lo que se debe hacer \( V-1 \) veces, donde \( V \) es el número de vértices.

4. **Detección de Ciclos Negativos**:
   - Verificar si hay un ciclo negativo en el grafo. Si se puede relajar cualquier arista después de \( V-1 \) iteraciones, el grafo tiene un ciclo negativo.

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

    def bellman_ford(self, start):
        # Initialize distances from start to all vertices as infinite
        distances = {vertex: float('infinity') for vertex in self.adjacency_list}
        distances[start] = 0

        # Relax edges |V| - 1 times
        for _ in range(len(self.adjacency_list) - 1):
            for u in self.adjacency_list:
                for v, weight in self.adjacency_list[u]:
                    if distances[u] + weight < distances[v]:
                        distances[v] = distances[u] + weight

        # Check for negative-weight cycles
        for u in self.adjacency_list:
            for v, weight in self.adjacency_list[u]:
                if distances[u] + weight < distances[v]:
                    print("Graph contains a negative-weight cycle")
                    return None

        return distances

# Usage
g = Graph()
g.add_edge('A', 'B', 1)
g.add_edge('A', 'C', 4)
g.add_edge('B', 'C', -3)
g.add_edge('B', 'D', 2)
g.add_edge('C', 'D', 3)

print("Distances from A:", g.bellman_ford('A'))
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

    public Map<String, Integer> bellmanFord(String start) {
        var distances = new HashMap<String, Integer>();
        for (var vertex : adjacencyList.keySet()) {
            distances.put(vertex, Integer.MAX_VALUE);
        }
        distances.put(start, 0);

        // Relax edges |V| - 1 times
        for (int i = 0; i < adjacencyList.size() - 1; i++) {
            for (var u : adjacencyList.keySet()) {
                for (var neighbor : adjacencyList.get(u)) {
                    var v = neighbor.getKey();
                    var weight = neighbor.getValue();
                    if (distances.get(u) != Integer.MAX_VALUE && distances.get(u) + weight < distances.get(v)) {
                        distances.put(v, distances.get(u) + weight);
                    }
                }
            }
        }

        // Check for negative-weight cycles
        for (var u : adjacencyList.keySet()) {
            for (var neighbor : adjacencyList.get(u)) {
                var v = neighbor.getKey();
                var weight = neighbor.getValue();
                if (distances.get(u) != Integer.MAX_VALUE && distances.get(u) + weight < distances.get(v)) {
                    System.out.println("Graph contains a negative-weight cycle");
                    return null;
                }
            }
        }

        return distances;
    }

    public static void main(String[] args) {
        var g = new Graph();
        g.addEdge("A", "B", 1);
        g.addEdge("A", "C", 4);
        g.addEdge("B", "C", -3);
        g.addEdge("B", "D", 2);
        g.addEdge("C", "D", 3);

        System.out.println("Distances from A: " + g.bellmanFord("A"));
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

    def bellman_ford(self, start):
        # Initialize distances from start to all vertices as infinite
        distances = [float('inf')] * self.num_vertices
        distances[start] = 0

        # Relax edges |V| - 1 times
        for _ in range(self.num_vertices - 1):
            for u in range(self.num_vertices):
                for v in range(self.num_vertices):
                    if self.adjacency_matrix[u][v] != float('inf'):
                        if distances[u] + self.adjacency_matrix[u][v] < distances[v]:
                            distances[v] = distances[u] + self.adjacency_matrix[u][v]

        # Check for negative-weight cycles
        for u in range(self.num_vertices):
            for v in range(self.num_vertices):
                if self.adjacency_matrix[u][v] != float('inf'):
                    if distances[u] + self.adjacency_matrix[u][v] < distances[v]:
                        print("Graph contains a negative-weight cycle")
                        return None

        return distances

# Usage
g = Graph(4)
g.add_edge(0, 1, 1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, -3)
g.add_edge(1, 3, 2)
g.add_edge(2, 3, 3)

print("Distances from vertex 0:", g.bellman_ford(0))
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

    public int[] bellmanFord(int start) {
        var distances = new int[numVertices];
        Arrays.fill(distances, Integer.MAX_VALUE);
        distances[start] = 0;

        // Relax edges |V| - 1 times
        for (int i = 0; i < numVertices - 1; i++) {
            for (int u = 0; u < numVertices; u++) {
                for (int v = 0; v < numVertices; v++) {
                    if (adjacencyMatrix[u][v] != Integer.MAX_VALUE) {
                        if (distances[u] != Integer.MAX_VALUE && distances[u] + adjacencyMatrix[u][v] < distances[v]) {
                            distances[v] = distances[u] + adjacencyMatrix[u][v];
                        }
                    }
                }
            }
        }

        // Check for negative-weight cycles
        for (int u = 0; u < numVertices; u++) {
            for (int v = 0; v < numVertices; v++) {


                if (adjacencyMatrix[u][v] != Integer.MAX_VALUE) {
                    if (distances[u] != Integer.MAX_VALUE && distances[u] + adjacencyMatrix[u][v] < distances[v]) {
                        System.out.println("Graph contains a negative-weight cycle");
                        return null;
                    }
                }
            }
        }

        return distances;
    }

    public static void main(String[] args) {
        var g = new Graph(4);
        g.addEdge(0, 1, 1);
        g.addEdge(0, 2, 4);
        g.addEdge(1, 2, -3);
        g.addEdge(1, 3, 2);
        g.addEdge(2, 3, 3);

        System.out.println("Distances from vertex 0: " + Arrays.toString(g.bellmanFord(0)));
    }
}
```
