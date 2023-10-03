# Array

- Declaration
```swift
var os : [String] = ["macOS","iOS","iPadOS","watchOS"]
```
```swift
var os : Array<String> = ["iOS","iPadOS","macOS","watchOS"]
```
```swift
var os : [String] = []
```
```swift
var os : Array<String> = []
```   

- Elements in Array
```swift
for iterator in os {
    print(iterator)
}
```
- Enumerated Elements in Array
```swift
for (index,iterator) in os.enumerated() {
    print("\(index) : \(iterator)")
}
```

## Methods

- Count
```swift
os.count
```
```
4
```

- Is Empty
```swift
os.isEmpty
```
```
false
```

- Append
```swift
os.append("tvOS")
```
```
["macOS", "iOS", "iPadOS", "watchOS", "tvOS"]
```
```swift
os.append(contentsOf: os)
```
```
["macOS", "iOS", "iPadOS", "watchOS", "macOS", "iOS", "iPadOS", "watchOS"]
```

- Insert
```swift
os.insert("tvOS", at: 2)
```
```
["macOS", "iOS", "tvOS", "iPadOS", "watchOS"]
```

- Remove
```swift
os.remove(at: 2)
```
```
["macOS", "iOS", "watchOS"]
```
```swift
os.removeFirst()
```
```
["iOS", "iPadOS", "watchOS"]
```
```swift
os.removeLast()
```
```
["macOS", "iOS", "iPadOS"]
```
```swift
os.removeAll()
```
```
[]
```

- Sort
```swift
os.sort()
```
```
["iOS", "iPadOS", "macOS", "watchOS"]
```
```swift
os.sort(by: <)
```
```
["iOS", "iPadOS", "macOS", "watchOS"]
```
```swift
os.sort(by: >)
```
```
["watchOS", "macOS", "iPadOS", "iOS"]
```

- Sorted
```swift
var numbers : [Int] = [2,1,3,21,8,1,13,5]
var result = numbers.sorted{$0 < $1}
```
```
[1, 1, 2, 3, 5, 8, 13, 21]
```
```swift
var numbers : [Int] = [2,1,3,21,8,1,13,5]
var result = numbers.sorted{$0 > $1}
```
```
[21, 13, 8, 5, 3, 2, 1, 1]
```

- Reverse
```swift
os.reverse()
```
```
["watchOS", "iPadOS", "iOS", "macOS"]
```

- Swap
```swift
os.swapAt(1, 2)
```
```
["macOS", "iPadOS", "iOS", "watchOS"]
```

- Shuffle
```swift
os.shuffle()
```
```
["iPadOS", "iOS", "macOS", "watchOS"]
```

- Contains
```swift
if os.contains("iOS") { print("TRUE") } else { print(false) }
```
```
TRUE
```

- First
```swift
var first = os.first
```
```
"macOS"
```
```swift
var first = os.first(where: {$0.lowercased().hasPrefix("io".lowercased())})
```
```
"iOS"
```
```swift
var first = os.first(where: {$0.lowercased().hasSuffix("dos".lowercased())})
```
```
"iPadOS"
```

- Last
```swift
var last = os.last
```
```
"watchOS"
```
```swift
var last = os.last(where: {$0.lowercased().hasPrefix("i".lowercased())})
```
```
"iPadOS"
```
```swift
var last = os.last(where: {$0.lowercased().hasSuffix("os".lowercased())})
```
```
"watchOS"
```

- Filter
```swift
var result = os.filter({$0.hasPrefix("i")})
```
```
["iOS", "iPadOS"]
```

- Reduce
```swift
var os : [String] = ["macOS","iOS","iPadOS","watchOS"]
var result = os.reduce("Apple OS List : ", {$0 + " " + $1})
```
```
Apple OS List :  macOS iOS iPadOS watchOS
```

- Map
```swift
var numbers : [Double] = [1.0,1.0,2.0,3.0,5.0,8.0,13.0,21.0]
var result = (numbers.map{$0 * 3.14}.sorted{$0 < $1}.filter{$0 > 4})
```
```
[6.28, 9.42, 15.700000000000001, 25.12, 40.82, 65.94]
```
