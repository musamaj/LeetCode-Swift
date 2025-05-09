Lexicographically smallest string after apply any number of operations

String -> “act”
Operations - any number of times
Arr = [0,1]
Brr = [1,0]

Pick any index from from indices arrays like pick first index from both would be 0 & 1, so swap the chars in string at these indices and keep doing so until it becomes lexicographically smallest

To solve this problem, we can model it as a graph problem, where each index in the string is a node, and each pair (Arr[i], Brr[i]) is an edge — allowing characters at these indices to be swapped any number of times.

This means that each connected component in the graph can have its characters rearranged freely. So for each connected component:

Collect the indices and characters.

Sort both the indices and characters.

Place the smallest character at the smallest index, next smallest at next smallest, etc.

```swift
class Solution {
    func smallestString(_ s: String, _ arr: [Int], _ brr: [Int]) -> String {
        let n = s.count
        var graph = Array(repeating: [Int](), count: n)

        // Build the undirected graph
        for i in 0..<arr.count {
            graph[arr[i]].append(brr[i])
            graph[brr[i]].append(arr[i])
        }

        var visited = Array(repeating: false, count: n)
        var chars = Array(s)

        func dfs(_ node: Int, _ indices: inout [Int]) {
            visited[node] = true
            indices.append(node)
            for neighbor in graph[node] {
                if !visited[neighbor] {
                    dfs(neighbor, &indices)
                }
            }
        }

        for i in 0..<n {
            if !visited[i] {
                var indices = [Int]()
                dfs(i, &indices)

                // Sort indices and corresponding characters
                let sortedIndices = indices.sorted()
                let sortedChars = sortedIndices.map { chars[$0] }.sorted()

                // Assign sorted characters to sorted indices
                for (j, idx) in sortedIndices.enumerated() {
                    chars[idx] = sortedChars[j]
                }
            }
        }

        return String(chars)
    }
}
```

