# Graph Valid Tree Check

## Problem Statement
Given `n` nodes labeled from `0` to `n - 1` and a list of undirected edges, determine whether these edges form a **valid tree**.

A **valid tree** satisfies two conditions:
1. It must be **connected** (all nodes must be reachable from any other node).
2. It must not contain any **cycles**.

### Example
#### Input:
let n = 5
let edges = [[0, 1], [0, 2], [0, 3], [1, 4]]

## Approach
To check if the given edges form a valid tree, we use Breadth-First Search (BFS):

## Edge Condition:

A tree with n nodes must have exactly n - 1 edges.
If edges.count != n - 1, return false.
Graph Representation:

Construct an adjacency list to represent the graph.
BFS Traversal & Cycle Detection:

Start BFS from node 0, marking nodes as visited.
If a node is visited twice (except from its parent), the graph contains a cycle → return false.
Check Connectivity:

Ensure all n nodes were visited; otherwise, it's not a single connected component.

```swift
func validTree(_ n: Int, _ edges: [[Int]]) -> Bool {
    if edges.count != n - 1 {
        return false
    }
    
    var adj = [[Int]](repeating: [], count: n)
    for edge in edges {
        let u = edge[0]
        let v = edge[1]
        adj[u].append(v)
        adj[v].append(u)
    }
    
    var visit = Set<Int>()
    var queue = [(0, -1)] // (current node, parent node)
    visit.insert(0)
    
    while !queue.isEmpty {
        let (node, parent) = queue.removeFirst()
        for neighbor in adj[node] {
            if neighbor == parent {
                continue
            }
            if visit.contains(neighbor) {
                return false
            }
            visit.insert(neighbor)
            queue.append((neighbor, node))
        }
    }
    
    return visit.count == n
}
```
