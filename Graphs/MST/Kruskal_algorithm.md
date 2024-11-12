## **Algoritmo de Kruskal**

El **algoritmo de Kruskal** es un algoritmo de grafo utilizado para encontrar el **árbol de expansión mínimo** (MST, por sus siglas en inglés) de un grafo ponderado y conexo. A diferencia del algoritmo de Prim, que crece de un vértice a otro, el algoritmo de Kruskal crece seleccionando las aristas de menor peso y uniendo los vértices en componentes disjuntos.

El algoritmo de Kruskal es especialmente eficiente en grafos dispersos, donde el número de aristas es mucho menor que el número máximo posible.

### **Descripción del Algoritmo:**

1. **Inicialización**:
   - Se comienza con un conjunto vacío de aristas en el árbol de expansión mínimo (MST).
   - Se ordenan todas las aristas del grafo por peso de manera ascendente.

2. **Selección de Aristas**:
   - Se seleccionan las aristas de menor peso, una por una, y se agregan al MST si no forman un ciclo.

3. **Unión de Componentes**:
   - Para determinar si añadir una arista formaría un ciclo, se utilizan **estructuras de conjuntos disjuntos** (como la **estructura de unión-find**).
   - Si los dos vértices de la arista pertenecen a componentes diferentes, la arista se agrega al MST y los componentes se unen.

4. **Repetir**:
   - Este proceso continúa hasta que se han añadido \( V-1 \) aristas, donde \( V \) es el número de vértices en el grafo.

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
        self.adjacency_list[v].append((u, weight))  # For undirected graph

    def find(self, parent, i):
        if parent[i] == i:
            return i
        else:
            parent[i] = self.find(parent, parent[i])
            return parent[i]

    def union(self, parent, rank, x, y):
        xroot = self.find(parent, x)
        yroot = self.find(parent, y)
        if rank[xroot] < rank[yroot]:
            parent[xroot] = yroot
        elif rank[xroot] > rank[yroot]:
            parent[yroot] = xroot
        else:
            parent[yroot] = xroot
            rank[xroot] += 1

    def kruskal(self):
        mst = []
        edges = []
        for u in self.adjacency_list:
            for v, weight in self.adjacency_list[u]:
                edges.append((weight, u, v))

        edges = sorted(edges)

        parent = {vertex: vertex for vertex in self.adjacency_list}
        rank = {vertex: 0 for vertex in self.adjacency_list}

        for weight, u, v in edges:
            if self.find(parent, u) != self.find(parent, v):
                mst.append((u, v, weight))
                self.union(parent, rank, u, v)

        return mst

# Usage
g = Graph()
g.add_edge('A', 'B', 1)
g.add_edge('A', 'C', 4)
g.add_edge('B', 'C', 2)
g.add_edge('B', 'D', 5)
g.add_edge('C', 'D', 3)

mst = g.kruskal()
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

    public String find(Map<String, String> parent, String vertex) {
        if (parent.get(vertex).equals(vertex)) {
            return vertex;
        }
        parent.put(vertex, find(parent, parent.get(vertex)));
        return parent.get(vertex);
    }

    public void union(Map<String, String> parent, Map<String, Integer> rank, String x, String y) {
        String rootX = find(parent, x);
        String rootY = find(parent, y);

        if (!rootX.equals(rootY)) {
            if (rank.get(rootX) > rank.get(rootY)) {
                parent.put(rootY, rootX);
            } else if (rank.get(rootX) < rank.get(rootY)) {
                parent.put(rootX, rootY);
            } else {
                parent.put(rootY, rootX);
                rank.put(rootX, rank.get(rootX) + 1);
            }
        }
    }

    public List<Pair<String, String>> kruskal() {
        List<Pair<String, String>> mst = new ArrayList<>();
        List<Triple<Integer, String, String>> edges = new ArrayList<>();

        for (var u : adjacencyList.keySet()) {
            for (var edge : adjacencyList.get(u)) {
                edges.add(new Triple<>(edge.getValue(), u, edge.getKey()));
            }
        }

        Collections.sort(edges, Comparator.comparingInt(Triple::getFirst));

        Map<String, String> parent = new HashMap<>();
        Map<String, Integer> rank = new HashMap<>();

        for (var vertex : adjacencyList.keySet()) {
            parent.put(vertex, vertex);
            rank.put(vertex, 0);
        }

        for (var edge : edges) {
            int weight = edge.getFirst();
            String u = edge.getSecond();
            String v = edge.getThird();

            if (!find(parent, u).equals(find(parent, v))) {
                mst.add(new Pair<>(u, v));
                union(parent, rank, u, v);
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

        var mst = g.kruskal();
        System.out.println("Minimum Spanning Tree: " + mst);
    }
}

// Helper class for Pair and Triple
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

class Triple<F, S, T> {
    private F first;
    private S second;
    private T third;

    public Triple(F first, S second, T third) {
        this.first = first;
        this.second = second;
        this.third = third;
    }

    public F getFirst() {
        return first;
    }

    public S getSecond() {
        return second;
    }

    public T getThird() {
        return third;
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
        self.adjacency_matrix[v][u] = weight  # For undirected graph

    def kruskal(self):
        edges = []
        for u in range(self.num_vertices):
            for v in range(self.num_vertices):
                if self.adjacency_matrix[u][v] != float('inf'):
                    edges.append((self.adjacency_matrix[u][v], u, v))

        edges = sorted(edges)

        parent = list(range(self.num_vertices))
        rank = [0] * self.num_vertices

        def find(u):
            if parent[u] != u:
                parent[u] = find(parent[u])
            return parent[u]

        def union(u, v):
            root_u = find(u)
            root_v = find(v)
            if root_u != root_v:
                if rank[root_u] > rank[root_v]:
                    parent[root_v] = root_u
                elif rank[root_u] < rank[root_v]:
                    parent[root_u] = root_v
                else:
                    parent[root_v] = root_u
                    rank[root_u] +=

 1

        mst = []

        for weight, u, v in edges:
            if find(u) != find(v):
                mst.append((u, v, weight))
                union(u, v)

        return mst

# Usage
g = Graph(4)
g.add_edge(0, 1, 1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 5)
g.add_edge(2, 3, 3)

mst = g.kruskal()
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

    public int[][] kruskal() {
        List<int[]> edges = new ArrayList<>();
        for (int u = 0; u < numVertices; u++) {
            for (int v = 0; v < numVertices; v++) {
                if (adjacencyMatrix[u][v] != Integer.MAX_VALUE) {
                    edges.add(new int[]{adjacencyMatrix[u][v], u, v});
                }
            }
        }

        edges.sort(Comparator.comparingInt(a -> a[0]));

        int[] parent = new int[numVertices];
        int[] rank = new int[numVertices];
        for (int i = 0; i < numVertices; i++) {
            parent[i] = i;
            rank[i] = 0;
        }

        List<int[]> mst = new ArrayList<>();

        for (int[] edge : edges) {
            int weight = edge[0];
            int u = edge[1];
            int v = edge[2];

            int rootU = find(parent, u);
            int rootV = find(parent, v);

            if (rootU != rootV) {
                mst.add(new int[]{u, v, weight});
                union(parent, rank, u, v);
            }
        }

        return mst.toArray(new int[0][0]);
    }

    private int find(int[] parent, int u) {
        if (parent[u] != u) {
            parent[u] = find(parent, parent[u]);
        }
        return parent[u];
    }

    private void union(int[] parent, int[] rank, int u, int v) {
        int rootU = find(parent, u);
        int rootV = find(parent, v);
        if (rootU != rootV) {
            if (rank[rootU] > rank[rootV]) {
                parent[rootV] = rootU;
            } else if (rank[rootU] < rank[rootV]) {
                parent[rootU] = rootV;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++;
            }
        }
    }

    public static void main(String[] args) {
        var g = new Graph(4);
        g.addEdge(0, 1, 1);
        g.addEdge(0, 2, 4);
        g.addEdge(1, 2, 2);
        g.addEdge(1, 3, 5);
        g.addEdge(2, 3, 3);

        int[][] mst = g.kruskal();
        System.out.println("Minimum Spanning Tree:");
        for (int[] row : mst) {
            System.out.println(Arrays.toString(row));
        }
    }
}
```
