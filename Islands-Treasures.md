# 🏝️ Islands and Treasure - BFS Solution in Swift  

## Problem Statement  
Given a grid where:  
- `0` represents water (starting points for BFS).  
- `-1` represents obstacles.  
- Positive integers represent land cells that need to be filled with the shortest distance to the nearest `0`.  

The goal is to update each land cell with the shortest distance to the nearest water cell (`0`). If a cell is unreachable, it remains unchanged.

---

## Solution Approach - Breadth-First Search (BFS)  

### Why BFS?  
Since we need the shortest distance to the nearest `0`, BFS is the optimal approach as it explores neighbors level by level.  

### Approach  
1. **Initialize a queue** with all `0` cells since they act as starting points.  
2. **Mark visited cells** using a `Set<[Int]>` to avoid redundant processing.  
3. **Perform BFS traversal**:
   - Process all cells in the queue level by level.
   - Update the grid with the shortest distance from a `0`.
   - Add adjacent valid land cells (`INF` or unvisited cells) to the queue.
   - Increase the distance counter.  
4. **Return the modified grid** after processing.  

---

## Swift Implementation 🚀  

```swift
import Foundation

func islandsAndTreasure(_ grid: inout [[Int]]) {
    let rows = grid.count
    let cols = grid[0].count
    var visited = Set<[Int]>()
    var queue = [[Int]]()

    func addCell(_ r: Int, _ c: Int) {
        if r < 0 || c < 0 || r >= rows || c >= cols || visited.contains([r, c]) || grid[r][c] == -1 {
            return
        }
        visited.insert([r, c])
        queue.append([r, c])
    }

    // Add all cells with 0 to the queue
    for r in 0..<rows {
        for c in 0..<cols {
            if grid[r][c] == 0 {
                queue.append([r, c])
                visited.insert([r, c])
            }
        }
    }

    var dist = 0
    while !queue.isEmpty {
        for _ in 0..<queue.count {
            let cell = queue.removeFirst()
            let r = cell[0], c = cell[1]
            grid[r][c] = dist
            addCell(r + 1, c)
            addCell(r - 1, c)
            addCell(r, c + 1)
            addCell(r, c - 1)
        }
        dist += 1
    }
}
