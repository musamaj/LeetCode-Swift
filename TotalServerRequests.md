Here's a Swift solution to the problem where you're given:

A list of initial server IDs.

A list of replacement IDs.

A list of corresponding new IDs.

The task is to simulate the server replacements and return the total sum of server IDs (which represents the total number of requests the servers can handle) after each day's replacement.


```swift
func getTotalRequests(server: [Int], replaceId: [Int], newId: [Int]) -> [Int] {
    var idCounts = [Int: Int]()  // Dictionary to store counts of each server ID
    var total = 0

    // Initialize the counts and total
    for id in server {
        idCounts[id, default: 0] += 1
        total += id
    }

    var result = [Int]()

    // Simulate each day's replacement
    for i in 0..<replaceId.count {
        let oldID = replaceId[i]
        let newID = newId[i]

        // If oldID doesn't exist, skip replacement
        if let count = idCounts[oldID], count > 0 {
            // Update total: subtract oldID total, add newID total
            total -= oldID * count
            total += newID * count

            // Update the idCounts dictionary
            idCounts[oldID] = 0
            idCounts[newID, default: 0] += count
        }

        result.append(total)
    }

    return result
}

// Sample Input
let server = [20, 10]
let replaceId = [10, 20]
let newId = [20, 1]

// Output: [40, 2]
print(getTotalRequests(server: server, replaceId: replaceId, newId: newId))
```

### 🧠 How It Works:
We use a dictionary to track the count of each server ID.

On each day:

We remove all servers with replaceId[i] and add the same count of newId[i].

The total sum of server IDs is adjusted accordingly.

This makes the solution efficient (O(n)) and scalable for large inputs (up to 100,000 elements).
