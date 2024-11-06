### **Algoritmo de Dijkstra**

El algoritmo de Dijkstra es un método utilizado para encontrar la ruta más corta desde un vértice fuente a todos los demás vértices en un grafo ponderado con aristas no negativas. Es uno de los algoritmos más eficientes y utilizados para este propósito.

#### **Descripción del Algoritmo:**
1. **Inicialización**:
   - Establecer la distancia del vértice fuente a sí mismo como 0 y a todos los demás vértices como infinito.
   - Crear un conjunto de nodos no visitados, que inicialmente contiene todos los vértices del grafo.

2. **Selección del Vértice**:
   - Elegir el vértice no visitado con la menor distancia conocida y marcarlo como visitado.

3. **Actualización de Distancias**:
   - Para cada vecino del vértice seleccionado, calcular la distancia total desde el vértice fuente a ese vecino a través del vértice seleccionado. Si esta distancia es menor que la distancia previamente registrada, actualizar la distancia.

4. **Repetir**:
   - Repetir el proceso hasta que todos los vértices hayan sido visitados o se haya alcanzado el vértice destino.

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

    def dijkstra(self, start):
        distances = {vertex: float('infinity') for vertex in self.adjacency_list}
        distances[start] = 0
        priority_queue = [(0, start)]

        while priority_queue:
            current_distance, current_vertex = heapq.heappop(priority_queue)

            if current_distance > distances[current_vertex]:
                continue

            for neighbor, weight in self.adjacency_list[current_vertex]:
                distance = current_distance + weight

                if distance < distances[neighbor]:
                    distances[neighbor] = distance
                    heapq.heappush(priority_queue, (distance, neighbor))

        return distances

# Uso
g = Graph()
g.add_edge('A', 'B', 1)
g.add_edge('A', 'C', 4)
g.add_edge('B', 'C', 2)
g.add_edge('B', 'D', 5)
g.add_edge('C', 'D', 1)

print("Distancias desde A:", g.dijkstra('A'))
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

    public Map<String, Integer> dijkstra(String start) {
        var distances = new HashMap<String, Integer>();
        for (var vertex : adjacencyList.keySet()) {
            distances.put(vertex, Integer.MAX_VALUE);
        }
        distances.put(start, 0);

        var priorityQueue = new PriorityQueue<Pair<String, Integer>>(Comparator.comparingInt(Pair::getValue));
        priorityQueue.add(new Pair<>(start, 0));

        while (!priorityQueue.isEmpty()) {
            var current = priorityQueue.poll();
            var currentVertex = current.getKey();
            var currentDistance = current.getValue();

            if (currentDistance > distances.get(currentVertex)) {
                continue;
            }

            for (var neighbor : adjacencyList.get(currentVertex)) {
                var neighborVertex = neighbor.getKey();
                var weight = neighbor.getValue();
                var newDistance = currentDistance + weight;

                if (newDistance < distances.get(neighborVertex)) {
                    distances.put(neighborVertex, newDistance);
                    priorityQueue.add(new Pair<>(neighborVertex, newDistance));
                }
            }
        }
        return distances;
    }

    public static void main(String[] args) {
        var g = new Graph();
        g.addEdge("A", "B", 1);
        g.addEdge("A", "C", 4);
        g.addEdge("B", "C", 2);
        g.addEdge("B", "D", 5);
        g.addEdge("C", "D", 1);

        System.out.println("Distancias desde A: " + g.dijkstra("A"));
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
            self.adjacency_matrix[i][i] = 0  # La distancia a sí mismo es 0

    def add_edge(self, u, v, weight):
        self.adjacency_matrix[u][v] = weight
        self.adjacency_matrix[v][u] = weight  # Para un grafo no dirigido

    def dijkstra(self, start):
        visited = [False] * self.num_vertices
        distances = [float('inf')] * self.num_vertices
        distances[start] = 0

        for _ in range(self.num_vertices):
            # Encontrar el vértice con la distancia mínima
            min_distance = float('inf')
            min_index = 0
            for v in range(self.num_vertices):
                if distances[v] < min_distance and not visited[v]:
                    min_distance = distances[v]
                    min_index = v

            visited[min_index] = True

            # Actualizar las distancias de los vecinos
            for v in range(self.num_vertices):
                if (self.adjacency_matrix[min_index][v] != float('inf') and
                        not visited[v] and
                        distances[min_index] + self.adjacency_matrix[min_index][v] < distances[v]):
                    distances[v] = distances[min_index] + self.adjacency_matrix[min_index][v]

        return distances

# Uso
g = Graph(4)
g.add_edge(0, 1, 1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 5)
g.add_edge(2, 3, 1)

print("Distancias desde el vértice 0:", g.dijkstra(0))
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
                adjacencyMatrix[i][j] = Integer.MAX_VALUE; // Inicializar como infinito
            }
            adjacencyMatrix[i][i] = 0; // La distancia a sí mismo es 0
        }
    }

    public void addEdge(int u, int v, int weight) {
        adjacencyMatrix[u][v] = weight;
        adjacencyMatrix[v][u] = weight; // Para un grafo no dirigido
    }

    public int[] dijkstra(int start) {
        var visited = new boolean[numVertices];
        var distances = new int[numVertices];

        for (int i = 0; i < numVertices; i++) {
            distances[i] = Integer.MAX_VALUE; // Inicializar distancias
        }
        distances[start] = 0;

        for (int count = 0; count < numVertices - 1; count++) {
            int minDistance = Integer.MAX_VALUE;
            int minIndex = -1;

            // Encontrar el vértice con la distancia mínima
            for (int v = 0; v < numVertices; v++) {
                if (!visited[v] && distances[v] <= minDistance

) {
                    minDistance = distances[v];
                    minIndex = v;
                }
            }

            visited[minIndex] = true;

            // Actualizar distancias de los vecinos
            for (int v = 0; v < numVertices; v++) {
                if (!visited[v] && adjacencyMatrix[minIndex][v] != Integer.MAX_VALUE &&
                        distances[minIndex] + adjacencyMatrix[minIndex][v] < distances[v]) {
                    distances[v] = distances[minIndex] + adjacencyMatrix[minIndex][v];
                }
            }
        }

        return distances;
    }

    public static void main(String[] args) {
        var g = new Graph(4);
        g.addEdge(0, 1, 1);
        g.addEdge(0, 2, 4);
        g.addEdge(1, 2, 2);
        g.addEdge(1, 3, 5);
        g.addEdge(2, 3, 1);

        System.out.println("Distancias desde el vértice 0: " + Arrays.toString(g.dijkstra(0)));
    }
}
```

### **Problemas Prácticos para Aplicar el Algoritmo de Dijkstra**

#### **Problema 1: Mapa de la Ciudad**

Tienes un mapa de una ciudad que se representa como un grafo ponderado, donde los nodos son las intersecciones y las aristas son las calles que conectan esas intersecciones. Cada calle tiene un peso que representa la distancia entre las intersecciones. Tu tarea es implementar el algoritmo de Dijkstra para encontrar la ruta más corta desde una intersección específica (el punto de partida) a todas las demás intersecciones de la ciudad.

**Entradas:**
- **Intersecciones (Nodos)**: Plaza Central, Calle 1, Calle 2, Avenida Principal, Parque, Mercado
- **Conexiones (Aristas) y Distancias (Pesos)**:
  - Plaza Central <-> Calle 1: 4
  - Plaza Central <-> Calle 2: 2
  - Calle 1 <-> Calle 2: 5
  - Calle 1 <-> Avenida Principal: 10
  - Calle 2 <-> Avenida Principal: 3
  - Calle 2 <-> Parque: 4
  - Avenida Principal <-> Parque: 1
  - Avenida Principal <-> Mercado: 5
  - Parque <-> Mercado: 7

- **Punto de partida**: Calle 2

**Salida esperada:**
- Distancias mínimas desde la intersección Calle 2 a cada una de las otras intersecciones.

---

#### **Problema 2: Red de Transporte Público**

Imagina que trabajas en la planificación de una red de transporte público en una ciudad. El sistema de transporte se puede modelar como un grafo, donde los nodos son paradas de autobús y las aristas son las rutas de autobús que conectan estas paradas. Cada ruta tiene un costo asociado que representa el tiempo o el costo del viaje.

Tu tarea es usar el algoritmo de Dijkstra para encontrar la ruta más corta en términos de costo desde una parada de autobús específica hasta todas las demás paradas en la red de transporte.

**Entradas:**
- **Paradas de autobús (Nodos)**: Estación de Trenes, Plaza de Toros, Centro Comercial, Parque de la Ciudad, Hospital
- **Rutas (Aristas) y Costos (Pesos)**:
  - Estación de Trenes <-> Plaza de Toros: 3
  - Estación de Trenes <-> Centro Comercial: 7
  - Plaza de Toros <-> Centro Comercial: 1
  - Plaza de Toros <-> Parque de la Ciudad: 4
  - Centro Comercial <-> Parque de la Ciudad: 2
  - Centro Comercial <-> Hospital: 5
  - Parque de la Ciudad <-> Hospital: 6

- **Parada de autobús de inicio**: Estación de Trenes

**Salida esperada:**
- La ruta de menor costo desde la parada de inicio Estación de Trenes a cada una de las otras paradas de autobús en la red.
