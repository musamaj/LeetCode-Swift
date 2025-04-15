### Falling Shapes
Yes, this sounds like a variation of a falling shapes problem, often inspired by Tetris-like mechanics. The matrix contains:

* → part of a figure or shape (like a block)

- → empty space

# → obstacle

Goal:
Find the minimum number of # obstacles that must be removed to let the * figure fall straight down vertically until it touches the bottom row or is blocked by another obstacle.

### 🔍 Problem Breakdown:
Think of the * figure as a block that should fall as one piece (not rotate or split).

It will stop when it touches the bottom or an obstacle #.

To let it fall as far as possible, you may need to remove obstacles (#) below it.

You need to count how many obstacles are in the way directly below the figure at each column it occupies.

### 🧠 Solution Idea:
Identify the rows & columns that contain the figure *.

Simulate the drop: For each column with *, move down and:

If it hits -, keep going.

If it hits #, count it as one to remove.

Find the minimum shift possible without breaking the figure or hitting unremovable obstacles.

```swift
func minObstaclesToRemove(matrix: [[Character]]) -> Int {
    let rows = matrix.count
    let cols = matrix[0].count
    
    var figureRows = [Int]()
    var figureCols = [Int]()
    
    // Identify positions of '*'
    for r in 0..<rows {
        for c in 0..<cols {
            if matrix[r][c] == "*" {
                figureRows.append(r)
                figureCols.append(c)
            }
        }
    }

    // Find the minimum distance to drop the figure
    var minDrop = rows
    for i in 0..<figureRows.count {
        let row = figureRows[i]
        let col = figureCols[i]
        var drop = 0
        for r in (row+1)..<rows {
            if matrix[r][col] == "#" {
                break
            }
            drop += 1
        }
        minDrop = min(minDrop, drop)
    }
    
    // Count how many obstacles are in the way after moving down by minDrop
    var removeCount = 0
    for i in 0..<figureRows.count {
        let newRow = figureRows[i] + minDrop
        let col = figureCols[i]
        if newRow < rows && matrix[newRow][col] == "#" {
            removeCount += 1
        }
    }

    return removeCount
}
```
