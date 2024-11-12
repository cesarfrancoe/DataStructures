## **Algoritmo de Boruvka**

El **algoritmo de Boruvka** es otro algoritmo utilizado para encontrar el **árbol de expansión mínimo** (MST, por sus siglas en inglés) de un grafo ponderado. Este algoritmo fue uno de los primeros desarrollados para resolver el problema de los árboles de expansión mínimos y tiene una implementación paralela muy eficiente. 

El algoritmo de Boruvka es particularmente útil para grafos densos y es considerado eficiente en situaciones en las que el grafo tiene muchas aristas.

### **Descripción del Algoritmo:**

1. **Inicialización**:
   - Cada vértice del grafo comienza en su propio componente conectado. Por lo tanto, cada vértice comienza siendo un "árbol" independiente.

2. **Selección de la Arista Mínima**:
   - En cada paso, para cada componente, se selecciona la arista de menor peso que conecta dicho componente con otro componente distinto.

3. **Unión de Componentes**:
   - Una vez que se han seleccionado las aristas mínimas para cada componente, se unen estos componentes mediante las aristas seleccionadas, formando nuevos árboles más grandes.

4. **Repetir**:
   - Este proceso se repite hasta que todos los vértices están en un único componente, lo que forma el árbol de expansión mínimo.

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

    def boruvka(self):
        # Initialize the parent and rank for each vertex
        parent = {vertex: vertex for vertex in self.adjacency_list}
        rank = {vertex: 0 for vertex in self.adjacency_list}
        
        # Helper function to find the parent of a vertex
        def find(v):
            if parent[v] != v:
                parent[v] = find(parent[v])
            return parent[v]

        # Helper function to union two sets
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
                    rank[root_u] += 1

        mst = []
        num_components = len(self.adjacency_list)

        while num_components > 1:
            # For each component, find the minimum edge connecting it to another component
            min_edges = {vertex: None for vertex in self.adjacency_list}

            for u in self.adjacency_list:
                for v, weight in self.adjacency_list[u]:
                    root_u = find(u)
                    root_v = find(v)
                    if root_u != root_v:
                        if min_edges[root_u] is None or min_edges[root_u][2] > weight:
                            min_edges[root_u] = (u, v, weight)
                        if min_edges[root_v] is None or min_edges[root_v][2] > weight:
                            min_edges[root_v] = (v, u, weight)

            for u in min_edges:
                if min_edges[u] is not None:
                    u, v, weight = min_edges[u]
                    if find(u) != find(v):
                        union(u, v)
                        mst.append((u, v, weight))
                        num_components -= 1

        return mst

# Usage
g = Graph()
g.add_edge('A', 'B', 1)
g.add_edge('A', 'C', 4)
g.add_edge('B', 'C', 2)
g.add_edge('B', 'D', 5)
g.add_edge('C', 'D', 3)

mst = g.boruvka()
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

    public List<Pair<String, String>> boruvka() {
        Map<String, String> parent = new HashMap<>();
        Map<String, Integer> rank = new HashMap<>();
        for (var vertex : adjacencyList.keySet()) {
            parent.put(vertex, vertex);
            rank.put(vertex, 0);
        }

        // Helper function to find the parent of a vertex
        var find = new HashMap<String, String>();
        for (var vertex : adjacencyList.keySet()) {
            find.put(vertex, vertex);
        }

        // Helper function to union two sets
        var union = (String u, String v) -> {
            String root_u = find.get(u);
            String root_v = find.get(v);
            if (!root_u.equals(root_v)) {
                if (rank.get(root_u) > rank.get(root_v)) {
                    find.put(root_v, root_u);
                } else if (rank.get(root_u) < rank.get(root_v)) {
                    find.put(root_u, root_v);
                } else {
                    find.put(root_v, root_u);
                    rank.put(root_u, rank.get(root_u) + 1);
                }
            }
        };

        List<Pair<String, String>> mst = new ArrayList<>();
        int numComponents = adjacencyList.size();

        while (numComponents > 1) {
            Map<String, Pair<String, Integer>> minEdges = new HashMap<>();
            for (var u : adjacencyList.keySet()) {
                for (var edge : adjacencyList.get(u)) {
                    String v = edge.getKey();
                    int weight = edge.getValue();
                    String root_u = find.get(u);
                    String root_v = find.get(v);

                    if (!root_u.equals(root_v)) {
                        if (!minEdges.containsKey(root_u) || minEdges.get(root_u).getValue() > weight) {
                            minEdges.put(root_u, new Pair<>(u, weight));
                        }
                        if (!minEdges.containsKey(root_v) || minEdges.get(root_v).getValue() > weight) {
                            minEdges.put(root_v, new Pair<>(v, weight));
                        }
                    }
                }
            }

            for (var u : minEdges.keySet()) {
                Pair<String, Integer> edge = minEdges.get(u);
                if (find.get(u) != find.get(edge.getKey())) {
                    union.accept(u, edge.getKey());
                    mst.add(new Pair<>(u, edge.getKey()));
                    numComponents--;
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

        var mst = g.boruvka();
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
class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        self.adjacency_matrix = [[float('inf')] * num_vertices for _ in range(num_vertices)]

        for i in range(num_vertices):
            self.adjacency_matrix[i][i] = 0  # Distance to self is 0

    def add_edge(self, u, v, weight):
        self.adjacency_matrix[u][v] = weight
        self.adjacency_matrix[v][u] = weight  # For undirected graph

    def boruvka(self):
        parent = [i for i in range(self.num_vertices)]
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
                    rank[root_u] += 1

        mst = []
        num_components = self.num_vertices

        while num_components > 1:
            min_edges = [-1] * self.num_vertices
            for u in range(self.num_vertices):
                for v in range(self.num_vertices):
                    if self.adjacency_matrix[u][v] != float('inf'):
                        root_u = find(u)
                        root_v = find(v)
                        if root_u != root_v:
                            if min_edges[root_u] == -1 or self.adjacency_matrix[u][v] < self.adjacency_matrix[min_edges[root_u]][root_u]:
                                min_edges[root_u] = v

            for u in range(self.num_vertices):
                if min_edges[u] != -1:
                    union(u, min_edges[u])
                    mst.append((u, min_edges[u], self.adjacency_matrix[u][min_edges[u]]))
                    num_components -= 1

        return mst

# Usage
g = Graph(4)
g.add_edge(0, 1, 1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 5)
g.add_edge(2, 3, 3)

mst = g.boruvka()
print("Minimum Spanning Tree:", mst)
```
