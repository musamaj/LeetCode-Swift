### Number of Compartments
* and | problem. Given a string with * and | and 2 arrays of startIndices and endIndices, output an array of the number of compartments (between 2 sticks)
*|**| has 1 compartment with 2 *.
Doable in O(N) time.

Here's the Swift method numberOfItems, which calculates the number of items between | characters in a string for given ranges:

```swift
func numberOfItems(s: String, startIndices: [Int], endIndices: [Int]) -> [Int] {
    let chars = Array(s)
    let n = chars.count
    var dp = [Int](repeating: 0, count: n)
    var count = 0

    for i in 0..<n {
        if chars[i] == "|" {
            dp[i] = count
        } else {
            count += 1
        }
    }

    var result = [Int]()
    for i in 0..<startIndices.count {
        var start = startIndices[i] - 1 // Adjust for 1-based index
        var end = endIndices[i] - 1     // Adjust for 1-based index

        while start < n && chars[start] != "|" { start += 1 }
        while end >= 0 && chars[end] != "|" { end -= 1 }

        if start < end && start < n && end >= 0 {
            result.append(dp[end] - dp[start])
        } else {
            result.append(0)
        }
    }

    return result
}
```
