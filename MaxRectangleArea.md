## 🧠 Approach:
We need to form rectangles using 4 sticks – 2 for width and 2 for height.

The array may include duplicate lengths, and each element can be reduced by at most 1 to potentially match another for pairing.

We collect all usable pairs (i.e., two sides of the same or reduced length).

Sort the usable pairs in descending order.

Pick the two largest different-length pairs to form the rectangle with the maximum area.

```swift
func maxRectangleArea(_ arr: [Int]) -> Int {
    var freq = [Int: Int]()
    
    // Count frequencies
    for num in arr {
        freq[num, default: 0] += 1
    }

    var sides = [Int]()

    // Form pairs from available sides (including reductions)
    var keys = Array(freq.keys).sorted(by: >)
    
    for key in keys {
        // First, check how many pairs we can form with this number
        while freq[key, default: 0] >= 2 {
            sides.append(key)
            freq[key]! -= 2
        }

        // Now check if we can reduce this to make a pair with (key - 1)
        if freq[key, default: 0] == 1 && key > 1 {
            if freq[key - 1, default: 0] >= 1 {
                sides.append(key - 1)
                freq[key]! -= 1
                freq[key - 1]! -= 1
            }
        }
    }

    // Sort the collected sides in descending order
    sides.sort(by: >)

    // Form rectangles from side pairs
    var area = 0
    var i = 0
    while i + 1 < sides.count {
        area += sides[i] * sides[i + 1]
        i += 2
    }

    return area
}

// Test Cases
print(maxRectangleArea([2, 3, 3, 4, 6, 6, 8, 8])) // Output: 54
print(maxRectangleArea([2, 1, 6, 5, 4, 4]))       // Output: 20
```
