### Extract Ordered Highlights

Modifying the Array While Iterating:

Removing elements while scanning can be tricky because indices shift.

You need to be careful to either mark and collect items to remove after iteration, or rebuild the array without certain elements.

Edge Handling:

You can't check height[i - 1] or height[i + 1] if you're at the start or end.

So you'd typically start from i = 1 and go up to heights.count - 2.

Greedy Choice of "Minimum Highlight":

You need to track previously added highlights and only add a new one if it’s smaller than all previous.

Ah, got it — you're saying for:

First element (i == 0): only check if height[0] > height[1]

Last element (i == heights.count - 1): only check if height[i] > height[i - 1]

For all other elements: check if height[i] > height[i - 1] && height[i] > height[i + 1]

```swift
func extractOrderedHighlights(from input: [Int]) -> [Int] {
    var heights = input
    var orderedHighlights = [Int]()

    while true {
        var localMaxIndex: Int? = nil
        var localMaxValue = Int.max

        for i in 0..<heights.count {
            let isLocalMax: Bool = {
                if i == 0 {
                    return heights.count > 1 && heights[i] > heights[i + 1]
                } else if i == heights.count - 1 {
                    return heights[i] > heights[i - 1]
                } else {
                    return heights[i] > heights[i - 1] && heights[i] > heights[i + 1]
                }
            }()

            if isLocalMax && heights[i] < localMaxValue {
                localMaxValue = heights[i]
                localMaxIndex = i
            }
        }

        // No local max found
        guard let idx = localMaxIndex else { break }

        orderedHighlights.append(heights[idx])
        heights.remove(at: idx)
    }

    return orderedHighlights
}
```
