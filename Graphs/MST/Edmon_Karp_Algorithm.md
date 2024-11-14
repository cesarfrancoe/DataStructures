## **Algoritmo de Edmonds-Karp**

El **algoritmo de Edmonds-Karp** es una implementación del algoritmo de **Ford-Fulkerson** para encontrar el **flujo máximo** en una red de flujo. Es un algoritmo de búsqueda de caminos aumentantes que utiliza una búsqueda en anchura (BFS) para encontrar el camino más corto en términos de número de aristas desde la fuente hasta el sumidero, y luego ajusta el flujo a lo largo de ese camino.

Este algoritmo es útil en aplicaciones como la optimización de redes de transporte, redes de telecomunicaciones y sistemas de distribución, donde se busca maximizar el flujo de un material, recurso o información a través de una red.

### **Descripción del Algoritmo:**

1. **Inicialización**:
   - El flujo en todas las aristas se establece inicialmente en cero.
   - Se crea una red residual que contiene las capacidades restantes para cada arista.

2. **Búsqueda de un Camino Aumentante**:
   - Se busca un camino desde la fuente hasta el sumidero utilizando una búsqueda en anchura (BFS). Este camino debe tener una capacidad residual positiva.

3. **Ajuste del Flujo**:
   - Una vez que se encuentra un camino aumentante, se calcula el flujo máximo posible a lo largo de ese camino y se actualiza el flujo en las aristas del camino.
   - El flujo residual en las aristas se ajusta, restando el flujo enviado a lo largo del camino encontrado.

4. **Repetir**:
   - El proceso se repite hasta que no se pueda encontrar un camino aumentante más.

### **Ejemplo en Python con Listas de Adyacencia**:

```python
from collections import deque

class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = {}
        for i in range(vertices):
            self.graph[i] = {}

    def add_edge(self, u, v, capacity):
        self.graph[u][v] = capacity
        self.graph[v][u] = 0  # Reverse edge has 0 initial capacity

    def bfs(self, source, sink, parent):
        visited = [False] * self.V
        queue = deque([source])
        visited[source] = True

        while queue:
            u = queue.popleft()

            for v in self.graph[u]:
                if not visited[v] and self.graph[u][v] > 0:
                    queue.append(v)
                    visited[v] = True
                    parent[v] = u
                    if v == sink:
                        return True
        return False

    def edmonds_karp(self, source, sink):
        parent = [-1] * self.V
        max_flow = 0

        while self.bfs(source, sink, parent):
            path_flow = float('Inf')
            s = sink
            while s != source:
                path_flow = min(path_flow, self.graph[parent[s]][s])
                s = parent[s]

            max_flow += path_flow

            v = sink
            while v != source:
                u = parent[v]
                self.graph[u][v] -= path_flow
                self.graph[v][u] += path_flow
                v = parent[v]

        return max_flow

# Usage
g = Graph(6)
g.add_edge(0, 1, 16)
g.add_edge(0, 2, 13)
g.add_edge(1, 2, 10)
g.add_edge(1, 3, 12)
g.add_edge(2, 1, 4)
g.add_edge(2, 4, 14)
g.add_edge(3, 2, 9)
g.add_edge(3, 5, 20)
g.add_edge(4, 3, 7)
g.add_edge(4, 5, 4)

max_flow = g.edmonds_karp(0, 5)
print("Maximum Flow:", max_flow)
```

### **Ejemplo en Java con Listas de Adyacencia**:

```java
import java.util.*;

class Graph {
    private int V;
    private Map<Integer, Map<Integer, Integer>> graph;

    public Graph(int vertices) {
        this.V = vertices;
        this.graph = new HashMap<>();
        for (int i = 0; i < vertices; i++) {
            graph.put(i, new HashMap<>());
        }
    }

    public void addEdge(int u, int v, int capacity) {
        graph.get(u).put(v, capacity);
        graph.get(v).put(u, 0);  // Reverse edge has 0 initial capacity
    }

    public boolean bfs(int source, int sink, int[] parent) {
        boolean[] visited = new boolean[V];
        Arrays.fill(visited, false);
        Queue<Integer> queue = new LinkedList<>();
        queue.add(source);
        visited[source] = true;
        parent[source] = -1;

        while (!queue.isEmpty()) {
            int u = queue.poll();

            for (int v : graph.get(u).keySet()) {
                if (!visited[v] && graph.get(u).get(v) > 0) {
                    queue.add(v);
                    visited[v] = true;
                    parent[v] = u;
                    if (v == sink) {
                        return true;
                    }
                }
            }
        }
        return false;
    }

    public int edmondsKarp(int source, int sink) {
        int[] parent = new int[V];
        int maxFlow = 0;

        while (bfs(source, sink, parent)) {
            int pathFlow = Integer.MAX_VALUE;
            int s = sink;
            while (s != source) {
                pathFlow = Math.min(pathFlow, graph.get(parent[s]).get(s));
                s = parent[s];
            }

            maxFlow += pathFlow;

            int v = sink;
            while (v != source) {
                int u = parent[v];
                graph.get(u).put(v, graph.get(u).get(v) - pathFlow);
                graph.get(v).put(u, graph.get(v).get(u) + pathFlow);
                v = parent[v];
            }
        }

        return maxFlow;
    }

    public static void main(String[] args) {
        Graph g = new Graph(6);
        g.addEdge(0, 1, 16);
        g.addEdge(0, 2, 13);
        g.addEdge(1, 2, 10);
        g.addEdge(1, 3, 12);
        g.addEdge(2, 1, 4);
        g.addEdge(2, 4, 14);
        g.addEdge(3, 2, 9);
        g.addEdge(3, 5, 20);
        g.addEdge(4, 3, 7);
        g.addEdge(4, 5, 4);

        int maxFlow = g.edmondsKarp(0, 5);
        System.out.println("Maximum Flow: " + maxFlow);
    }
}
```

### **Ejemplo en Python con Matrices de Adyacencia**:

```python
class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        self.adjacency_matrix = [[0] * num_vertices for _ in range(num_vertices)]

    def add_edge(self, u, v, capacity):
        self.adjacency_matrix[u][v] = capacity

    def bfs(self, source, sink, parent):
        visited = [False] * self.num_vertices
        queue = [source]
        visited[source] = True

        while queue:
            u = queue.pop(0)

            for v in range(self.num_vertices):
                if not visited[v] and self.adjacency_matrix[u][v] > 0:
                    queue.append(v)
                    visited[v] = True
                    parent[v] = u
                    if v == sink:
                        return True
        return False

    def edmonds_karp(self, source, sink):
        parent = [-1] * self.num_vertices
        max_flow = 0

        while self.bfs(source, sink, parent):
            path_flow = float('Inf')
            s = sink
            while s != source:
                path_flow = min(path_flow, self.adjacency_matrix[parent[s]][s])
                s = parent[s]

            max_flow += path_flow

            v = sink
            while v != source:
                u = parent[v]
                self.adjacency_matrix[u][v] -= path_flow
                self.adjacency_matrix[v][u] += path_flow
                v = parent[v]

        return max_flow

# Usage
g = Graph(6)
g.add_edge(0, 1, 16)
g.add_edge(0, 2, 13)
g.add_edge(1, 2, 10)
g.add_edge(1, 3, 12)
g.add_edge(2, 1, 4)
g.add_edge(2, 4, 14)
g.add_edge(3, 2, 9)
g.add_edge(3, 5, 20)
g.add_edge(4, 3, 7)
g.add_edge(4, 5, 4)

max_flow = g.edmonds_karp(0, 5)
print("Maximum Flow:", max_flow)
```

### **Ejemplo en Java con Matrices de Adyacencia**:

```java
class Graph {
    private int[][] adjacencyMatrix

;
    private int numVertices;

    public Graph(int numVertices) {
        this.numVertices = numVertices;
        adjacencyMatrix = new int[numVertices][numVertices];
    }

    public void addEdge(int u, int v, int capacity) {
        adjacencyMatrix[u][v] = capacity;
    }

    public boolean bfs(int source, int sink, int[] parent) {
        boolean[] visited = new boolean[numVertices];
        visited[source] = true;
        Queue<Integer> queue = new LinkedList<>();
        queue.add(source);

        while (!queue.isEmpty()) {
            int u = queue.poll();

            for (int v = 0; v < numVertices; v++) {
                if (!visited[v] && adjacencyMatrix[u][v] > 0) {
                    queue.add(v);
                    visited[v] = true;
                    parent[v] = u;
                    if (v == sink) {
                        return true;
                    }
                }
            }
        }
        return false;
    }

    public int edmondsKarp(int source, int sink) {
        int[] parent = new int[numVertices];
        int maxFlow = 0;

        while (bfs(source, sink, parent)) {
            int pathFlow = Integer.MAX_VALUE;
            int s = sink;
            while (s != source) {
                pathFlow = Math.min(pathFlow, adjacencyMatrix[parent[s]][s]);
                s = parent[s];
            }

            maxFlow += pathFlow;

            int v = sink;
            while (v != source) {
                int u = parent[v];
                adjacencyMatrix[u][v] -= pathFlow;
                adjacencyMatrix[v][u] += pathFlow;
                v = parent[v];
            }
        }

        return maxFlow;
    }

    public static void main(String[] args) {
        Graph g = new Graph(6);
        g.addEdge(0, 1, 16);
        g.addEdge(0, 2, 13);
        g.addEdge(1, 2, 10);
        g.addEdge(1, 3, 12);
        g.addEdge(2, 1, 4);
        g.addEdge(2, 4, 14);
        g.addEdge(3, 2, 9);
        g.addEdge(3, 5, 20);
        g.addEdge(4, 3, 7);
        g.addEdge(4, 5, 4);

        int maxFlow = g.edmondsKarp(0, 5);
        System.out.println("Maximum Flow: " + maxFlow);
    }
}
```
