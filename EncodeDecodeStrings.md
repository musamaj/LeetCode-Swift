### Encode and Decode Strings
Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement encode and decode

Example 1:

Input: ["neet","code","love","you"]

Output:["neet","code","love","you"]
Example 2:

Input: ["we","say",":","yes"]

Output: ["we","say",":","yes"]


```swift
class Solution {
    func encode(_ strs: [String]) -> String {
        var res = ""
        for s in strs {
            res += "\(s.count)#\(s)"
        }
        return res
    }

    func decode(_ s: String) -> [String] {
        var res = [String]()
        let sArr = Array(s)
        var i = 0

        while i < sArr.count {
            var j = i
            while sArr[j] != "#" {
                j += 1
            }
            let lengthStr = String(sArr[i..<j])
            let length = Int(lengthStr)!

            i = j + 1
            let end = i + length
            let substring = String(sArr[i..<end])
            res.append(substring)
            i = end
        }

        return res
    }
}
```
