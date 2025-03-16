# Dijkstra's Algorithm in Swift

## Overview
Dijkstra’s Algorithm is used to find the **shortest path** from a single source node to all other nodes in a **weighted graph** (with non-negative weights). It is widely used in routing and navigation systems.

## Algorithm Explanation
1. **Initialize Distances**:  
   - Set the distance to the source node as `0` and all other nodes as `infinity`.
   - Use a **priority queue (min-heap)** to always expand the node with the **smallest known distance**.  
2. **Process Nodes**:  
   - Extract the **closest node** from the priority queue.  
   - Relax all its neighbors:  
     - If going through the current node offers a **shorter path** to a neighbor, update its distance and push it into the priority queue.  
3. **Repeat Until All Nodes Are Processed**.

## Swift Implementation
```swift
import Foundation

struct Edge {
    let to: Int
    let weight: Int
}

func dijkstra(_ graph: [[Edge]], _ source: Int) -> [Int] {
    let n = graph.count
    var distances = Array(repeating: Int.max, count: n)
    distances[source] = 0
    
    var minHeap = [(dist: Int, node: Int)]()  // Min-heap (priority queue)
    minHeap.append((0, source))
    
    while !minHeap.isEmpty {
        minHeap.sort { $0.dist < $1.dist }  // Sorting to simulate priority queue behavior
        let (currentDist, node) = minHeap.removeFirst()
        
        if currentDist > distances[node] {
            continue
        }
        
        for edge in graph[node] {
            let newDist = currentDist + edge.weight
            if newDist < distances[edge.to] {
                distances[edge.to] = newDist
                minHeap.append((newDist, edge.to))
            }
        }
    }
    
    return distances
}

// Example usage
let graph: [[Edge]] = [
    [Edge(to: 1, weight: 4), Edge(to: 2, weight: 1)],   // Edges from node 0
    [Edge(to: 3, weight: 1)],                           // Edges from node 1
    [Edge(to: 1, weight: 2), Edge(to: 3, weight: 5)],   // Edges from node 2
    []                                                  // Node 3 has no outgoing edges
]

let sourceNode = 0
let shortestPaths = dijkstra(graph, sourceNode)
print(shortestPaths)  // Output: Shortest distances from source node
```

## Time Complexity
- **Using a priority queue (min-heap):** `O((V + E) log V)`, where `V` is vertices and `E` is edges.
- **Without a min-heap (naïve implementation):** `O(V²)`.

## Example Walkthrough
### **Graph Representation**
```
    (0) --4--> (1)
     | \      /
     |  \    / 1
     |   \  /
    1|    (2)
     |      \
     |       \ 5
     |        \
    (3) <----- (2)
```
For `source = 0`, the algorithm finds the shortest path to all nodes.

### **Final Output (Shortest Distances from Node `0`)**:
```
[0, 3, 1, 4]
```
Where:
- Distance to **node 0** = `0` (source node).
- Distance to **node 1** = `3` (via node 2).
- Distance to **node 2** = `1` (direct edge).
- Distance to **node 3** = `4` (via node 1).

## Applications
- **GPS Navigation Systems** 🚗
- **Network Routing Algorithms** 🖧
- **AI Pathfinding (e.g., in Games)** 🎮
- **Traffic Management Systems** 🚦

## Contributing
Feel free to submit pull requests if you find any optimizations or improvements!

## License
This project is open-source under the MIT License.

