if sender/recipent ids appear more than or equal to threshold in transactions


```swift
func processLogs(logs: [String], threshold: Int) -> [String] {
    var usersMap: [String: Int] = [:]
    var resultSet = Set<String>()

    for log in logs {
        let split = log.split(separator: " ")
        if split.count == 3 {
            let senderId = String(split[0])
            let recipientId = String(split[1])
            
            if senderId == recipientId {
                usersMap[senderId, default: 0] += 1
            } else {
                usersMap[senderId, default: 0] += 1
                usersMap[recipientId, default: 0] += 1
            }
        }
    }

    for (user, count) in usersMap where count >= threshold {
        resultSet.insert(user)
    }

    return resultSet.sorted(by: { Int($0)! < Int($1)! })
}
```
