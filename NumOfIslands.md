# 🌊 Number of Islands - DFS & BFS Solutions in Swift  

## Problem Statement  
Given a **2D grid** containing `'1'` (land) and `'0'` (water), find the **number of islands**. An **island** is formed by adjacent land cells (horizontally or vertically), and the entire island is **surrounded by water**.  

Your goal is to count the number of distinct islands in the grid.  

---

## Pattern: Flood Fill / Connected Components  
This problem follows the **Flood Fill** pattern, where we explore connected components (**land `'1'`**) and mark them as visited to avoid counting the same island multiple times.  

### Solution Approach  
1. **Iterate through the grid**, checking each cell.  
2. If a **land cell (`'1'`)** is found, trigger a **DFS or BFS traversal** to explore and mark all connected land cells.  
3. **Increment the island count** each time a new unvisited `'1'` is found.  
4. **Continue scanning the grid** until all cells are visited.  

---

## 🏝️ DFS Approach (Recursive)  

### How It Works  
- When a land cell (`'1'`) is found, start a **Depth-First Search (DFS)**.  
- Mark the current cell as visited (`'0'`) to prevent re-processing.  
- Recursively **explore all four directions** (up, down, left, right).  
- Continue until the entire island is traversed.  

### Implementation  

```swift
func numIslands(_ grid: [[Character]]) -> Int {
    var grid = grid
    let rows = grid.count
    let cols = grid[0].count
    var islandCount = 0
    
    func dfs(_ r: Int, _ c: Int) {
        if r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] == "0" {
            return
        }
        
        grid[r][c] = "0" // Mark as visited
        
        dfs(r + 1, c) // Down
        dfs(r - 1, c) // Up
        dfs(r, c + 1) // Right
        dfs(r, c - 1) // Left
    }
    
    for r in 0..<rows {
        for c in 0..<cols {
            if grid[r][c] == "1" {
                islandCount += 1
                dfs(r, c) // Explore and mark the entire island
            }
        }
    }
    
    return islandCount
}
```
## ✅ Complexity Analysis
Time Complexity: O(m × n) (Each cell is visited once)
Space Complexity: O(m × n) (Worst case recursive stack depth)


```swift
func numIslands(_ grid: [[Character]]) -> Int {
    var grid = grid
    let rows = grid.count
    let cols = grid[0].count
    var islandCount = 0
    let directions = [(0,1), (0,-1), (1,0), (-1,0)] // Right, Left, Down, Up
    
    func bfs(_ r: Int, _ c: Int) {
        var queue = [(r, c)]
        grid[r][c] = "0" // Mark as visited
        
        while !queue.isEmpty {
            let (row, col) = queue.removeFirst()
            for (dr, dc) in directions {
                let newRow = row + dr
                let newCol = col + dc
                if newRow >= 0, newRow < rows, newCol >= 0, newCol < cols, grid[newRow][newCol] == "1" {
                    queue.append((newRow, newCol))
                    grid[newRow][newCol] = "0" // Mark as visited
                }
            }
        }
    }
    
    for r in 0..<rows {
        for c in 0..<cols {
            if grid[r][c] == "1" {
                islandCount += 1
                bfs(r, c) // Explore the island
            }
        }
    }
    
    return islandCount
}
```

## ✅ Complexity Analysis
Time Complexity: O(m × n) (Each cell is processed once)
Space Complexity: O(min(m, n)) (Queue stores one level of nodes at most)
