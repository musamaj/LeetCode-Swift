# Number of Connected Components in an Undirected Graph

## Problem Statement
Given an undirected graph with `n` nodes, and an `edges` array where `edges[i] = [a, b]` represents an edge between node `a` and node `b`, determine the number of connected components in the graph.

A **connected component** is a subset of nodes such that there is a path between any two nodes in the subset, and no node in the subset is connected to any node outside of it.

The nodes are labeled from `0` to `n - 1`.

## Example

### Example 1:
#### Input:
n = 3 edges = [[0,1], [0,2]]

### Example 2:
#### Input:
n = 6 edges = [[0,1], [1,2], [2,3], [4,5]]

#### Explanation:
- Nodes `{0,1,2,3}` form one connected component.
- Nodes `{4,5}` form another connected component.

## Approach

### 1. **Graph Representation**
- We use an **adjacency list** to represent the graph.

### 2. **Graph Traversal**
- Use **Breadth-First Search (BFS)** or **Depth-First Search (DFS)** to explore connected components.

### 3. **Counting Components**
- Iterate over all nodes. If a node hasn't been visited, perform BFS/DFS from it and count it as a new connected component.

## Complexity Analysis
- **Time Complexity**: `O(N + E)`, where `N` is the number of nodes and `E` is the number of edges.
- **Space Complexity**: `O(N + E)` for storing the graph in an adjacency list.

## Solution Code (Python)
```Swift
import Foundation

func countComponents(_ n: Int, _ edges: [[Int]]) -> Int {
    var adj = [[Int]](repeating: [], count: n)
    var visited = [Bool](repeating: false, count: n)

    // Build adjacency list
    for edge in edges {
        let u = edge[0], v = edge[1]
        adj[u].append(v)
        adj[v].append(u)
    }

    func bfs(_ node: Int) {
        var queue = [node]
        visited[node] = true
        
        while !queue.isEmpty {
            let cur = queue.removeFirst()
            for neighbor in adj[cur] {
                if !visited[neighbor] {
                    visited[neighbor] = true
                    queue.append(neighbor)
                }
            }
        }
    }

    var res = 0
    for node in 0..<n {
        if !visited[node] {
            bfs(node)
            res += 1
        }
    }

    return res
}
```

Edge Cases Considered:
Graph with No Edges: n = 5, edges = [] → Output: 5 (Each node is its own component).
Fully Connected Graph: n = 4, edges = [[0,1], [1,2], [2,3], [3,0]] → Output: 1 (All nodes are connected).
Disconnected Graph: n = 6, edges = [[0,1], [2,3], [4,5]] → Output: 3 (Three separate components).
Summary
This problem helps in understanding graph traversal and connected components.
BFS and DFS are efficient techniques to explore the graph.

