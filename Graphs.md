# **Grafos**

## **1. Definición de Grafos y sus Componentes**

Un **grafo** es una estructura de datos compuesta por un conjunto de **nodos** (o vértices) y un conjunto de **aristas** (o bordes) que conectan pares de nodos. Los grafos se utilizan para representar relaciones entre objetos en diversas áreas, como redes sociales, mapas y rutas de transporte.

### **Componentes de un Grafo:**
- **Vértices (Nodos)**: Son los elementos individuales del grafo. Se representan generalmente con círculos o puntos. Por ejemplo, en un grafo que representa una red social, cada persona puede ser un vértice.
  
- **Aristas (Bordes)**: Son las conexiones entre los vértices. Pueden ser **dirigidas** (una dirección) o **no dirigidas** (sin dirección). En un grafo dirigido, si hay un borde de A a B, no implica que haya un borde de B a A.

- **Grado de un Vértice**: Es el número de aristas que inciden en un vértice. En un grafo dirigido, se distingue entre el **grado de entrada** y el **grado de salida**.

- **Caminos**: Una secuencia de vértices donde cada par de vértices adyacentes están conectados por una arista. 

- **Ciclo**: Un camino que comienza y termina en el mismo vértice sin repetir aristas.

## **2. Representación de Grafos**

Los grafos se pueden representar de varias maneras, siendo las más comunes:

### **Matrices de Adyacencia**
Una matriz de adyacencia es una representación bidimensional que utiliza una matriz para indicar la presencia o ausencia de aristas entre los vértices.

**Ejemplo en Python:**

```python
class Graph:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        # Create a 2D array (matrix) initialized to 0
        self.adjacency_matrix = [[0 for _ in range(num_vertices)] for _ in range(num_vertices)]

    def add_edge(self, u, v):
        # Add an edge between vertex u and vertex v
        self.adjacency_matrix[u][v] = 1
        self.adjacency_matrix[v][u] = 1  # For undirected graph

    def display(self):
        # Display the adjacency matrix
        for row in self.adjacency_matrix:
            print(row)

# Example of usage
g = Graph(3)  # Create a graph with 3 vertices
g.add_edge(0, 1)  # Add edge between vertex 0 and 1
g.add_edge(1, 2)  # Add edge between vertex 1 and 2
g.display()  # Display the adjacency matrix
```

### **Listas de Adyacencia**
Una lista de adyacencia es una representación más eficiente en términos de espacio, especialmente para grafos dispersos.

**Ejemplo en Python:**

```python
class Graph:
    def __init__(self):
        self.adjacency_list = {}  # Initialize an empty dictionary to hold the adjacency list

    def add_vertex(self, vertex):
        # Add a new vertex to the adjacency list
        if vertex not in self.adjacency_list:
            self.adjacency_list[vertex] = []

    def add_edge(self, u, v):
        # Add an edge between vertex u and vertex v
        self.add_vertex(u)  # Ensure u is in the adjacency list
        self.add_vertex(v)  # Ensure v is in the adjacency list
        self.adjacency_list[u].append(v)  # Append v to u's list
        self.adjacency_list[v].append(u)  # Append u to v's list (for undirected graph)

    def display(self):
        # Display the adjacency list
        for vertex in self.adjacency_list:
            print(vertex, ":", self.adjacency_list[vertex])

# Example of usage
g = Graph()  # Create a new graph
g.add_edge('A', 'B')  # Add edge between vertex A and B
g.add_edge('B', 'C')  # Add edge between vertex B and C
g.display()  # Display the adjacency list
```

### **Implementación en Java**

#### **Matrices de Adyacencia**

```java
class Graph {
    private int[][] adjacencyMatrix;
    private int numVertices;

    public Graph(int numVertices) {
        this.numVertices = numVertices;
        // Create a 2D array (matrix) initialized to 0
        adjacencyMatrix = new int[numVertices][numVertices];
    }

    public void addEdge(int u, int v) {
        // Add an edge between vertex u and vertex v
        adjacencyMatrix[u][v] = 1;
        adjacencyMatrix[v][u] = 1;  // For undirected graph
    }

    public void display() {
        // Display the adjacency matrix
        for (var row : adjacencyMatrix) {
            for (var value : row) {
                System.out.print(value + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        var g = new Graph(3);  // Create a graph with 3 vertices
        g.addEdge(0, 1);  // Add edge between vertex 0 and 1
        g.addEdge(1, 2);  // Add edge between vertex 1 and 2
        g.display();  // Display the adjacency matrix
    }
}
```

#### **Listas de Adyacencia**

```java
import java.util.*;

class Graph {
    private Map<String, List<String>> adjacencyList;  // Initialize a map for the adjacency list

    public Graph() {
        adjacencyList = new HashMap<>();  // Create a new HashMap
    }

    public void addVertex(String vertex) {
        // Add a new vertex to the adjacency list
        adjacencyList.putIfAbsent(vertex, new ArrayList<>());
    }

    public void addEdge(String u, String v) {
        // Add an edge between vertex u and vertex v
        addVertex(u);  // Ensure u is in the adjacency list
        addVertex(v);  // Ensure v is in the adjacency list
        adjacencyList.get(u).add(v);  // Add v to u's adjacency list
        adjacencyList.get(v).add(u);  // Add u to v's adjacency list (for undirected graph)
    }

    public void display() {
        // Display the adjacency list
        for (var vertex : adjacencyList.keySet()) {
            System.out.println(vertex + " : " + adjacencyList.get(vertex));
        }
    }

    public static void main(String[] args) {
        var g = new Graph();  // Create a new graph
        g.addEdge("A", "B");  // Add edge between vertex A and B
        g.addEdge("B", "C");  // Add edge between vertex B and C
        g.display();  // Display the adjacency list
    }
}
```

## **3. Ejemplos de Uso de Grafos en Casos Reales**

### **Ejemplo 1: Redes Sociales**
Las redes sociales utilizan grafos para representar las conexiones entre usuarios. Cada usuario es un vértice y cada amistad o relación es una arista. 

**Importancia:**
- Los algoritmos de grafos permiten encontrar amigos en común, sugerencias de amistad y analizar la estructura de la red social. Por ejemplo, el algoritmo de búsqueda en profundidad (DFS) puede ser utilizado para explorar conexiones entre usuarios.

### **Ejemplo 2: Rutas de Transporte**
Los sistemas de navegación utilizan grafos para modelar las rutas de transporte. Las intersecciones son vértices y las carreteras son aristas que conectan estos vértices.

**Importancia:**
- Los algoritmos de grafos, como Dijkstra, se utilizan para encontrar la ruta más corta entre dos puntos. Esto es esencial para aplicaciones de mapas y navegación, ya que permite a los usuarios obtener direcciones eficientes y optimizadas.

### **Ejemplo 3: Redes de Comunicación**
En las redes de computadoras, cada dispositivo es un vértice y cada conexión de red es una arista. Esto incluye redes de telecomunicaciones, Internet y redes locales.

**Importancia:**
- Los grafos ayudan a gestionar la comunicación entre dispositivos, optimizar el tráfico de datos y detectar fallas en la red. Algoritmos como el de Prim o Kruskal pueden ser usados para construir redes eficientes y minimizar costos en la conectividad.

### **Ejemplo 4: Sistemas de Recomendación**
Las plataformas de streaming y comercio electrónico utilizan grafos para ofrecer recomendaciones personalizadas a los usuarios. En este contexto, los productos o contenidos son vértices y las interacciones (como visualizaciones o compras) son aristas.

**Importancia:**
- Los algoritmos de grafos permiten identificar patrones de comportamiento entre usuarios y productos, lo que ayuda a generar recomendaciones más precisas y relevantes. Esto no solo mejora la experiencia del usuario, sino que también aumenta la retención de clientes.

### **Ejemplo 5: Planificación de Rutas en Drones**
En la entrega de paquetes mediante drones, los grafos se utilizan para planificar rutas eficientes. Los puntos de entrega son vértices y las posibles trayectorias entre ellos

 son aristas.

**Importancia:**
- La optimización de rutas en un grafo permite que los drones minimicen el tiempo de entrega y el consumo de energía. Utilizando algoritmos como el de A*, se pueden calcular las rutas más rápidas y seguras, mejorando así la eficiencia del servicio de entrega.
