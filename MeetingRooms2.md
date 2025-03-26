# Minimum Meeting Rooms

## Problem Statement
Given an array of meeting time intervals where each interval is represented as `[start, end]`, return the minimum number of meeting rooms required.

## Approach
- Extract start and end times from the intervals and sort them separately.
- Use two pointers to iterate through the sorted start and end times.
- Maintain a counter to track active meetings.
- If a meeting starts before another one ends, increment the count.
- If a meeting ends, decrement the count.
- The maximum value of the counter during this process gives the required number of meeting rooms.

## Complexity Analysis
- Sorting takes **O(n log n)**.
- The iteration through the sorted lists takes **O(n)**.
- Overall time complexity: **O(n log n)**.

## Swift Implementation
```swift
import Foundation

class Solution {
    func minMeetingRooms(_ intervals: [[Int]]) -> Int {
        let start = intervals.map { $0[0] }.sorted()
        let end = intervals.map { $0[1] }.sorted()
        
        var res = 0, count = 0
        var s = 0, e = 0
        
        while s < intervals.count {
            if start[s] < end[e] {
                count += 1
                s += 1
            } else {
                count -= 1
                e += 1
            }
            res = max(res, count)
        }
        
        return res
    }
}

// Example Usage:
let solution = Solution()
print(solution.minMeetingRooms([[0, 30], [5, 10], [15, 20]])) // Output: 2
```

## Example Test Cases
### Example 1:
#### Input:
```
[[0, 30], [5, 10], [15, 20]]
```
#### Output:
```
2
```

### Example 2:
#### Input:
```
[[7, 10], [2, 4]]
```
#### Output:
```
1
```

## Edge Cases Considered
- No meetings: `[]` → Output: `0`
- Meetings with the same start and end time.
- Large inputs for performance testing.

