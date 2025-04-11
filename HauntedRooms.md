## Haunted Rooms

The "Leaked LeetCode Questions" series often features a scenario where CodeBots have moved into a new building with rooms of varying costs, including some free rooms. However, there's a rumor that the free rooms are haunted, so the CodeBots are unwilling to stay in them. This scenario is used to explore problem-solving strategies in a coding context

Here's the Swift version of the JavaScript function matrixElementsSum. This function calculates the sum of values in a 2D matrix where any element below a 0 is also considered 0 (like in a haunted house floor plan problem).

```swift
func matrixElementsSum(_ matrix: [[Int]]) -> Int {
    var matrix = matrix
    let rows = matrix.count
    let cols = matrix[0].count

    for i in 0..<rows {
        for j in 0..<cols {
            if matrix[i][j] == 0 && i + 1 < rows {
                matrix[i + 1][j] = 0
            }
        }
    }

    // Flatten and sum
    let total = matrix.flatMap { $0 }.reduce(0, +)
    return total
}
```

###  Explanation:
matrix is copied as a var because we mutate it.

Loops through the matrix. If a cell is 0, it sets the cell directly below it in the same column to 0.

Finally, it flattens the 2D array using flatMap and sums it using reduce.
