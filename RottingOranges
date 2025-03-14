# Rotten Oranges - BFS Solution in Swift 🍊  

## Problem Statement  
You are given an `m x n` grid where:  
- `0` represents an empty cell.  
- `1` represents a fresh orange.  
- `2` represents a rotten orange.  

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange **becomes rotten**.  
Return the **minimum time** required for all oranges to rot. If it's impossible, return `-1`.  

---

## Solution Approach - Breadth-First Search (BFS)  

We use **Breadth-First Search (BFS)** to simulate the rotting process, as it spreads layer by layer (minute by minute).  

1. **Initialize a queue** with the coordinates of all rotten oranges.  
2. **Count the fresh oranges** in the grid.  
3. **Perform BFS traversal**:
   - At each step, process all rotten oranges in the queue.
   - Spread the rot to adjacent fresh oranges and update the grid.
   - Reduce the count of fresh oranges.
   - Increase the time counter.  
4. **Return the time taken** if all fresh oranges are rotten; otherwise, return `-1`.  

---

## Swift Implementation 🚀  

```swift
import Foundation

func orangesRotting(_ grid: inout [[Int]]) -> Int {
    var queue = [(Int, Int)]()
    var fresh = 0
    var time = 0

    let rows = grid.count
    let cols = grid[0].count
    let directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

    // Count fresh oranges and add rotten ones to the queue
    for r in 0..<rows {
        for c in 0..<cols {
            if grid[r][c] == 1 {
                fresh += 1
            } else if grid[r][c] == 2 {
                queue.append((r, c))
            }
        }
    }

    // BFS traversal
    while fresh > 0 && !queue.isEmpty {
        let length = queue.count
        for _ in 0..<length {
            let (r, c) = queue.removeFirst()

            for (dr, dc) in directions {
                let row = r + dr
                let col = c + dc
                
                if row >= 0, row < rows, col >= 0, col < cols, grid[row][col] == 1 {
                    grid[row][col] = 2
                    queue.append((row, col))
                    fresh -= 1
                }
            }
        }
        time += 1
    }

    return fresh == 0 ? time : -1
}

###Complexity Analysis
Time Complexity: O(m × n)
Each cell is processed at most once.
Space Complexity: O(m × n)
In the worst case, all oranges are stored in the queue.
