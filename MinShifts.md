To solve this problem, we need to compute the minimum number of shifts (up or down) to go from setTime to timeToSet in both hours and minutes, considering the cyclic nature of a clock:

Hours range from 0...23 (24 hours)

Minutes range from 0...59 (60 minutes)

For each part (hours and minutes), we compute:

Shift up: (target - current + range) % range

Shift down: (current - target + range) % range

Then, we take the minimum of both options.


### ✅ Swift Implementation:

```swift
func solution(setTime: String, timeToSet: String) -> Int {
    let setParts = setTime.split(separator: ":").map { Int($0)! }
    let targetParts = timeToSet.split(separator: ":").map { Int($0)! }

    let setHour = setParts[0]
    let setMinute = setParts[1]
    let targetHour = targetParts[0]
    let targetMinute = targetParts[1]

    // Hour shifts (cyclic on 24)
    let hourUp = (targetHour - setHour + 24) % 24
    let hourDown = (setHour - targetHour + 24) % 24
    let hourShifts = min(hourUp, hourDown)

    // Minute shifts (cyclic on 60)
    let minuteUp = (targetMinute - setMinute + 60) % 60
    let minuteDown = (setMinute - targetMinute + 60) % 60
    let minuteShifts = min(minuteUp, minuteDown)

    return hourShifts + minuteShifts
}
```

### Example

```swift
solution(setTime: "07:30", timeToSet: "08:00")
// Output: 31
// 1 hour up + 30 minutes down

```
