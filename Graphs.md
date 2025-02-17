# **Graphs**

## **1. What is a Graph?**

A **Graph** is a non-linear data structure consisting of nodes (also called **vertices**) connected by edges (also called **links**). A graph can represent many real-world problems like social networks, web pages, and transportation systems.

✅ **Key Terms:**

- **Vertex (Node)** – A fundamental unit (element) in the graph.

- **Edge (Link)** – A connection between two vertices.

- **Directed Graph (Digraph)** – Edges have a direction (one-way connection).

- **Undirected Graph** – Edges have no direction (two-way connection).

- **Weighted Graph** – Edges have weights (cost or distance).

- Degree

   – The number of edges incident to a vertex.

  - **In-degree** (for directed graphs): Number of incoming edges.
  - **Out-degree** (for directed graphs): Number of outgoing edges.

✅ **Types of Graphs:**

1. **Directed Graph** – Edges have a direction (from one node to another).
2. **Undirected Graph** – Edges do not have a direction (bidirectional).
3. **Weighted Graph** – Edges have a value or weight associated with them.
4. **Unweighted Graph** – All edges are assumed to have the same weight (1).
5. **Complete Graph** – Every pair of vertices is connected by an edge.
6. **Bipartite Graph** – The vertices can be divided into two disjoint sets, and every edge connects a vertex from one set to another.

------

# **2. Graph Representation**

Graphs can be represented in two main ways:

1. **Adjacency Matrix**
2. **Adjacency List**

### **Adjacency Matrix Representation:**

In an **Adjacency Matrix**, a 2D array `matrix[i][j]` is used to represent the edges. If there is an edge from vertex `i` to vertex `j`, `matrix[i][j]` is set to `1` (or the weight of the edge in a weighted graph), otherwise `0`.

#### Code:

```python
def adjacency_matrix(n, edges):
    graph = [[0] * n for _ in range(n)]  # Initialize matrix
    for u, v in edges:
        graph[u][v] = 1  # For unweighted graph
        graph[v][u] = 1  # For undirected graph (uncomment for directed graph)
    return graph

# Example usage
n = 4  # Number of vertices
edges = [(0, 1), (0, 2), (1, 3), (2, 3)]  # List of edges
graph = adjacency_matrix(n, edges)

for row in graph:
    print(row)
```

#### Output:

```
[0, 1, 1, 0]
[1, 0, 0, 1]
[1, 0, 0, 1]
[0, 1, 1, 0]
```

### **Adjacency List Representation:**

In an **Adjacency List**, each vertex has a list of connected vertices. This representation is more space-efficient for sparse graphs (graphs with fewer edges).

#### Code:

```python
def adjacency_list(n, edges):
    graph = {i: [] for i in range(n)}  # Initialize empty lists for each vertex
    for u, v in edges:
        graph[u].append(v)  # For directed graph
        graph[v].append(u)  # For undirected graph (uncomment for directed graph)
    return graph

# Example usage
n = 4  # Number of vertices
edges = [(0, 1), (0, 2), (1, 3), (2, 3)]  # List of edges
graph = adjacency_list(n, edges)

for vertex, neighbors in graph.items():
    print(f"Vertex {vertex}: {neighbors}")
```

#### Output:

```
Vertex 0: [1, 2]
Vertex 1: [0, 3]
Vertex 2: [0, 3]
Vertex 3: [1, 2]
```

------

# **3. Graph Traversal**

There are two main methods for graph traversal:

1. **Depth-First Search (DFS)** – Explore as far as possible along a branch before backtracking.
2. **Breadth-First Search (BFS)** – Explore all neighbors at the present depth level before moving on to nodes at the next depth level.

### **(1) Depth-First Search (DFS)**

DFS can be implemented using **recursion** or a **stack**. It explores the graph deeply before backtracking.

#### Code:

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start, end=" ")
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

# Example usage
dfs(graph, 0)  # Output: 0 1 3 2
```

✅ **Used in:** Finding connected components, solving puzzles, pathfinding.

### **(2) Breadth-First Search (BFS)**

BFS uses a **queue** to explore the graph level by level.

#### Code:

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)

    while queue:
        vertex = queue.popleft()
        print(vertex, end=" ")
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

# Example usage
bfs(graph, 0)  # Output: 0 1 2 3
```

✅ **Used in:** Shortest path problems, web crawlers, finding connected components.

------

# **4. Types of Graphs and Their Applications**

### **Complete Graph:**

A **Complete Graph** is a graph in which every pair of vertices is connected by an edge. If there are `n` vertices, a complete graph will have:

n(n−1)2 edges\frac{n(n-1)}{2} \text{ edges}

#### Code (for a complete graph):

```python
def complete_graph(n):
    edges = []
    for i in range(n):
        for j in range(i + 1, n):
            edges.append((i, j))
    return edges

# Example usage
n = 4
edges = complete_graph(n)
print(edges)  # Output: [(0, 1), (0, 2), (0, 3), (1, 2), (1, 3), (2, 3)]
```

✅ **Use Cases:**

- Network design.
- Fully connected systems in computer science.

### **Bipartite Graph:**

A **Bipartite Graph** is a graph whose vertices can be divided into two disjoint sets such that every edge connects a vertex in one set to a vertex in the other set.

#### Code:

```python
def is_bipartite(graph, start):
    color = {}
    queue = deque([start])
    color[start] = 0

    while queue:
        vertex = queue.popleft()
        for neighbor in graph[vertex]:
            if neighbor not in color:
                color[neighbor] = 1 - color[vertex]
                queue.append(neighbor)
            elif color[neighbor] == color[vertex]:
                return False  # Not bipartite
    return True

# Example usage
print(is_bipartite(graph, 0))  # Output: True/False based on graph structure
```

✅ **Used in:** Scheduling problems, matching problems, graph coloring.

------

# **5. Summary of Graph Representations and Traversal**

| **Operation**        | **Adjacency Matrix**       | **Adjacency List**                     |
| -------------------- | -------------------------- | -------------------------------------- |
| **Space Complexity** | O(n^2)                     | O(n + m), where `m` is number of edges |
| **Traversal (DFS)**  | O(n^2)                     | O(n + m)                               |
| **Traversal (BFS)**  | O(n^2)                     | O(n + m)                               |
| **Search**           | O(1) (for a specific edge) | O(n) in worst case                     |

------

# **6. Applications of Graphs**

✅ **Graphs in Competitive Programming:**

- **Pathfinding Algorithms**: Dijkstra, Bellman-Ford, A*.
- **Connectivity**: DFS, BFS to find connected components.
- **Network Flow**: Max flow, Min cut problems.
- **Graph Coloring**: Checking for bipartiteness, 2-coloring.
- **Cycle Detection**: Detecting cycles in directed and undirected graphs.

Graphs are used to model real-world problems like social networks, maps, web crawling, network routing, and much more. Understanding graph representation, traversal, and types is crucial for solving many complex problems efficiently in competitive programming.