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
