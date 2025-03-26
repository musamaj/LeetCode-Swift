# Can Attend Meetings

## Problem Statement
Given an array of meeting time intervals where each interval is represented as `[start, end]`, determine if a person can attend all meetings without overlap.

## Approach
The function sorts the intervals by their start times and then checks for any overlap between consecutive meetings.

## Algorithm
1. **Sort** the intervals based on their start times.
2. **Iterate** through the sorted intervals.
3. **Check overlap**: If the previous meeting's end time is greater than the next meeting's start time, return `false`.
4. If no overlaps are found, return `true`.

## Implementation in Swift
```swift
class Solution {
    func canAttendMeetings(_ intervals: [[Int]]) -> Bool {
        let sortedIntervals = intervals.sorted { $0[0] < $1[0] }

        for i in 1..<sortedIntervals.count {
            let prev = sortedIntervals[i - 1]
            let curr = sortedIntervals[i]

            if prev[1] > curr[0] {
                return false
            }
        }
        return true
    }
}
```

## Complexity Analysis
- **Sorting Complexity**: \(O(n \log n)\)
- **Iteration Complexity**: \(O(n)\)
- **Overall Complexity**: \(O(n \log n)\)

## Example
```swift
let solution = Solution()
print(solution.canAttendMeetings([[0, 30], [5, 10], [15, 20]])) // false
print(solution.canAttendMeetings([[7, 10], [2, 4]])) // true
```

## Edge Cases Considered
- No intervals (`[]`)
- Single meeting (`[[1, 5]]`)
- Meetings that don't overlap
- Meetings that start exactly when the previous one ends

## Notes
This solution efficiently determines if a person can attend all meetings using sorting and iteration.

