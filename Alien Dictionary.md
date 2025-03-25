# 📖 Foreign Dictionary Order

## 📝 Problem Statement
Given a list of words sorted in an alien language dictionary, determine the order of the characters in the language. If the order is inconsistent or cyclic, return an empty string.

## 🚀 Solution Approach
This solution constructs a **graph (adjacency list)** and then performs a **topological sort using DFS** to determine the order of characters.

### 🔹 Steps:
1. **Graph Construction**
   - Extract all unique characters.
   - Compare adjacent words to build order relationships.
   - If a word is a prefix of another but longer, return "" (invalid case).

2. **Topological Sorting (DFS)**
   - Detect cycles to ensure a valid order.
   - Perform **postorder DFS traversal** to derive the order.

## 🏗 Implementation (Swift)
```swift
func foreignDictionary(_ words: [String]) -> String {
    var adj = [Character: Set<Character>]()
    
    // Initialize adjacency list for all characters
    for word in words {
        for char in word {
            adj[char, default: Set<Character>()] = []
        }
    }
    
    // Build the graph by comparing adjacent words
    for i in 0..<words.count - 1 {
        let w1 = Array(words[i]), w2 = Array(words[i + 1])
        let minLen = min(w1.count, w2.count)

        if w1.count > w2.count && w1.prefix(minLen) == w2.prefix(minLen) {
            return ""
        }
        
        for j in 0..<minLen {
            if w1[j] != w2[j] {
                adj[w1[j], default: []].insert(w2[j])
                break
            }
        }
    }

    var visited = [Character: Bool]()
    var res = [Character]()
    
    func dfs(_ char: Character) -> Bool {
        if let state = visited[char] {
            return state
        }
        
        visited[char] = true
        if let neighbors = adj[char] {
            for neighbor in neighbors {
                if dfs(neighbor) {
                    return true
                }
            }
        }
        visited[char] = false
        res.append(char)
        
        return false
    }
    
    for char in adj.keys {
        if dfs(char) {
            return ""
        }
    }
    
    return String(res.reversed())
}
```

## ⏳ Complexity Analysis
- **Time Complexity**: `O(C + V)` where `C` is the number of unique characters and `V` is the number of order relationships.
- **Space Complexity**: `O(C + V)` for the adjacency list and recursion stack.

## ✅ Example Usage
```swift
let words = ["wrt", "wrf", "er", "ett", "rftt"]
print(foreignDictionary(words)) // Output: "wertf"
```

## 📌 Edge Cases Considered
- Words with duplicate characters.
- Words that form a cycle.
- Words with no constraints (single word input).

## 📜 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
🚀 **Happy Coding!**

