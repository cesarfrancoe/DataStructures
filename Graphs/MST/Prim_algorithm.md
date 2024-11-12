## **Algoritmo de Prim**

El **algoritmo de Prim** es un algoritmo de grafo utilizado para encontrar el **árbol de expansión mínimo** (MST, por sus siglas en inglés) de un grafo ponderado y conectado. El objetivo del algoritmo es conectar todos los vértices del grafo con el menor costo posible, utilizando un subconjunto de las aristas del grafo.

Este algoritmo es muy útil en problemas de redes, como la planificación de redes de distribución (agua, electricidad, telecomunicaciones), donde se requiere conectar todos los nodos de manera eficiente en términos de costos.

### **Descripción del Algoritmo:**

1. **Inicialización**:
   - Comienza con un vértice arbitrario y lo marca como parte del MST.
   - Todos los vértices restantes están inicialmente en un conjunto no visitado.

2. **Selección de la Arista de Menor Peso**:
   - En cada paso, se selecciona la arista de menor peso que conecta un vértice en el MST con uno en el conjunto de vértices no visitados.

3. **Actualización de los Vértices**:
   - El vértice seleccionado se agrega al MST, y se actualizan las aristas de menor peso que conectan el MST con los vértices no visitados.

4. **Repetir**:
   - Este proceso se repite hasta que todos los vértices estén conectados.

### **Explicación:**

https://www.youtube.com/watch?v=6pPSPYUbTlw

### **Simulador:**

https://www.cs.usfca.edu/~galles/visualization/Prim.html

### **Ejemplo en Python con Listas de Adyacencia**:

```python
import heapq

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
        self.adjacency_list[v].append((u, weight))  # For undirected graph

    def prim(self, start):
        mst = []
        visited = set([start])
        edges = [
            (weight, start, v) for v, weight in self.adjacency_list[start]
        ]
        heapq.heapify(edges)

        while edges:
            weight, u, v = heapq.heappop(edges)
            if v not in visited:
                visited.add(v)
                mst.append((u, v, weight))
                for to, weight in self.adjacency_list[v]:
                    if to not in visited:
                        heapq.heappush(edges, (weight, v, to))

        return mst

# Usage
g = Graph()
g.add_edge('A', 'B', 1)
g.add_edge('A', 'C', 4)
g.add_edge('B', 'C', 2)
g.add_edge('B', 'D', 5)
g.add_edge('C', 'D', 3)

mst = g.prim('A')
print("Minimum Spanning Tree:", mst)
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
        adjacencyList.get(v).add(new Pair<>(u, weight));  // For undirected graph
    }

    public List<Pair<String, String>> prim(String start) {
        List<Pair<String, String>> mst = new ArrayList<>();
        Set<String> visited = new HashSet<>();
        PriorityQueue<Pair<Integer, Pair<String, String>>> edges = new PriorityQueue<>(Comparator.comparingInt(Pair::getKey));

        visited.add(start);
        for (var neighbor : adjacencyList.get(start)) {
            edges.add(new Pair<>(neighbor.getValue(), new Pair<>(start, neighbor.getKey())));
        }

        while (!edges.isEmpty()) {
            var edge = edges.poll();
            var weight = edge.getKey();
            var u = edge.getValue().getKey();
            var v = edge.getValue().getValue();

            if (!visited.contains(v)) {
                visited.add(v);
                mst.add(new Pair<>(u, v));
                for (var neighbor : adjacencyList.get(v)) {
                    if (!visited.contains(neighbor.getKey())) {
                        edges.add(new Pair<>(neighbor.getValue(), new Pair<>(v, neighbor.getKey())));
                    }
                }
            }
        }

        return mst;
    }

    public static void main(String[] args) {
        var g = new Graph();
        g.addEdge("A", "B", 1);
        g.addEdge("A", "C", 4);
        g.addEdge("B", "C", 2);
        g.addEdge("B", "D", 5);
        g.addEdge("C", "D", 3);

        var mst = g.prim("A");
        System.out.println("Minimum Spanning Tree: " + mst);
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
import heapq

class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        self.adjacency_matrix = [[float('inf')] * num_vertices for _ in range(num_vertices)]

        for i in range(num_vertices):
            self.adjacency_matrix[i][i] = 0  # Distance to self is 0

    def add_edge(self, u, v, weight):
        self.adjacency_matrix[u][v] = weight
        self.adjacency_matrix[v][u] = weight  # For undirected graph

    def prim(self, start):
        mst = []
        visited = [False] * self.num_vertices
        min_heap = [(0, start)]

        while min_heap:
            weight, u = heapq.heappop(min_heap)

            if visited[u]:
                continue

            visited[u] = True
            if weight != 0:
                mst.append((prev, u, weight))

            for v in range(self.num_vertices):
                if not visited[v] and self.adjacency_matrix[u][v] != float('inf'):
                    heapq.heappush(min_heap, (self.adjacency_matrix[u][v], v))
                    prev = u

        return mst

# Usage
g = Graph(4)
g.add_edge(0, 1, 1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 5)
g.add_edge(2, 3, 3)

mst = g.prim(0)
print("Minimum Spanning Tree:", mst)
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
        adjacencyMatrix[v][u] = weight; // For undirected graph
    }

    public int[][] prim(int start) {
        int[][] mst = new int[numVertices][numVertices];
        boolean[] visited = new boolean[numVertices];
        int[] minEdge = new int[numVertices];
        Arrays.fill(minEdge, Integer.MAX_VALUE);
        minEdge[start] = 0;

        for (int i = 0; i < numVertices; i++) {
            int u = -1;
            for (int j = 0; j < numVertices; j++) {
                if (!visited[j] && (u == -1 || minEdge[j] < minEdge[u])) {
                    u = j;
                }
            }

            visited[u] = true;

            for (int v = 0; v < numVertices; v++) {
                if (adjacencyMatrix[u][v] != Integer.MAX_VALUE && !visited[v] && adjacencyMatrix[u][v] < minEdge[v]) {
                    minEdge[v] = adjacencyMatrix[u][v];
                    mst[u][v] = adjacencyMatrix[u][v];
                    mst[v][u] = adjacencyMatrix[u][v];
                }
            }
        }

        return mst;
    }

    public static void main(String[] args) {
        var g = new Graph(4);
        g.addEdge(0, 1, 1);


        g.addEdge(0, 2, 4);
        g.addEdge(1, 2, 2);
        g.addEdge(1, 3, 5);
        g.addEdge(2, 3, 3);

        int[][] mst = g.prim(0);
        System.out.println("Minimum Spanning Tree:");
        for (int[] row : mst) {
            System.out.println(Arrays.toString(row));
        }
    }
}
```
