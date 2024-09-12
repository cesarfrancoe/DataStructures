# **Tema 3: Árboles**

## **Introducción**
Los árboles son estructuras de datos jerárquicas que se utilizan para modelar relaciones entre elementos de una manera organizada. Un árbol está compuesto por nodos conectados por aristas. Cada nodo contiene un valor y puede tener varios nodos hijos. El nodo superior se denomina raíz, y los nodos sin hijos se llaman hojas. Los árboles son útiles para representar estructuras como jerarquías, sistemas de archivos, entre otros.

## **Recorridos principales de los árboles**
Los recorridos de árboles permiten visitar todos los nodos de un árbol de manera sistemática. Los principales métodos de recorrido son:

- **Preorden (Pre-order)**: Visita el nodo raíz, luego recorre el subárbol izquierdo y finalmente el subárbol derecho.

  ```python
  def preorder_traversal(node):
      if node:
          print(node.value)
          preorder_traversal(node.left)
          preorder_traversal(node.right)
  ```

- **Inorden (In-order)**: Recorre el subárbol izquierdo, luego visita el nodo raíz, y finalmente el subárbol derecho.

  ```python
  def inorder_traversal(node):
      if node:
          inorder_traversal(node.left)
          print(node.value)
          inorder_traversal(node.right)
  ```

- **Postorden (Post-order)**: Recorre el subárbol izquierdo, luego el subárbol derecho, y finalmente visita el nodo raíz.

  ```python
  def postorder_traversal(node):
      if node:
          postorder_traversal(node.left)
          postorder_traversal(node.right)
          print(node.value)
  ```

- **Nivel por nivel (Level-order)**: Visita los nodos por niveles, comenzando desde la raíz y bajando nivel por nivel.

  ```python
  from collections import deque

  def level_order_traversal(root):
      if not root:
          return
      
      queue = deque([root])
      
      while queue:
          node = queue.popleft()
          print(node.value)
          
          if node.left:
              queue.append(node.left)
          if node.right:
              queue.append(node.right)
  ```

## **Árboles Binarios**
Un árbol binario es un árbol en el que cada nodo tiene como máximo dos hijos, conocidos como hijo izquierdo y hijo derecho.

### **Árboles Binarios de Búsqueda (BST)**
Un árbol binario de búsqueda es un árbol binario con la propiedad de que para cada nodo:
- Los valores de los nodos en el subárbol izquierdo son menores que el valor del nodo.
- Los valores de los nodos en el subárbol derecho son mayores que el valor del nodo.

Esta propiedad permite realizar búsquedas, inserciones y eliminaciones de forma eficiente.

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def insert(root, value):
    if not root:
        return TreeNode(value)
    
    if value < root.value:
        root.left = insert(root.left, value)
    else:
        root.right = insert(root.right, value)
    
    return root
```

### **Árboles AVL**
Un árbol AVL es un tipo de árbol binario de búsqueda auto-balanceado. El árbol AVL mantiene un equilibrio mediante la restricción de que la diferencia de alturas entre los subárboles izquierdo y derecho de cualquier nodo no puede ser mayor a 1.

```python
class AVLNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
        self.height = 1

def get_height(node):
    return node.height if node else 0

def right_rotate(y):
    x = y.left
    T2 = x.right
    x.right = y
    y.left = T2
    y.height = max(get_height(y.left), get_height(y.right)) + 1
    x.height = max(get_height(x.left), get_height(x.right)) + 1
    return x

def left_rotate(x):
    y = x.right
    T2 = y.left
    y.left = x
    x.right = T2
    x.height = max(get_height(x.left), get_height(x.right)) + 1
    y.height = max(get_height(y.left), get_height(y.right)) + 1
    return y
```

### **Árboles Rojo-Negro**
Un árbol Rojo-Negro es otro tipo de árbol binario de búsqueda balanceado que sigue reglas específicas de coloración y balance.

```python
class RedBlackNode:
    def __init__(self, value, color="red"):
        self.value = value
        self.color = color
        self.left = None
        self.right = None
        self.parent = None
```

## **Árboles n-arios**
Un árbol n-ario es un árbol en el que cada nodo puede tener como máximo n hijos.

### **Árboles 2-3**
Los árboles 2-3 son árboles de búsqueda balanceados en los que cada nodo puede tener 2 o 3 hijos.

```python
class TwoThreeNode:
    def __init__(self, value=None):
        self.values = [] if value is None else [value]
        self.children = []

def insert_2_3(node, value):
    # Insertion logic for 2-3 tree
    pass
```

### **Árboles B**
Un árbol B es una generalización de los árboles 2-3, en el que cada nodo puede tener más de tres hijos.

```python
class BTreeNode:
    def __init__(self, t):
        self.keys = []
        self.children = []
        self.t = t  # Minimum degree

def insert_b_tree(node, key):
    # Insertion logic for B-tree
    pass
```
