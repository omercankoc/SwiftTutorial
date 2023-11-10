# Loops
```swift
var base : [Int] = []
var square : [Int] = []

var limit : Int = 10

var iterator : Int = 0
var repeater : Int = 0
```
### While
```swift
while iterator <= limit {
    base.append(iterator)
    iterator += 1
}
```
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Repeat While
```swift
repeat {
    repeater += 1
    base.append(repeater)
} while repeater <= limit
```
```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

### For
```swift
for index in base {
    if index == 0 { continue }
    square.append(base[index]*base[index])
}
```
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

- Closed Range Operator
```swift
for index in 0...limit {
    print(index) 
}
```
```
0 1 2 3 4 5 6 7 8 9 10
```

- Half-Open Range Operator
```swift
for index in 0..<limit {
    print(index)
}
```
```
0 1 2 3 4 5 6 7 8 9
```

- One-Sided Ranges
```swift
for index in base[2...]{
    print(index)
}
```
```
2 3 4 5 6 7 8 9 10
```

```swift
for index in base[...5]{
    print(index)
}
```
```
0 1 2 3 4 5
```

```swift
for index in base[..<5]{
    print(index)
}
```
```
0 1 2 3 4 
```

- Stride
```swift
for index in stride(from: 0, to: 60, by: 10){
    print(index)
}
```
```
0 10 20 30 40 50
```

### For Each
```swift
var os : [String] = ["iOS","iPadOS","macOS","watchOS","tvOS"]
os.forEach { item in print("\(item)") }
```
```
iOS iPadOS macOS watchOS tvOS
```

# Conditional Statements
```swift
var midterm : Float = 65
var final : Float = 55
var score : Float = (midterm + final) / 2

var modulus = Int(score) % 2
```

### If
```swift
if final >= 50 {
    if score >= 50 && score < 55 {
        print("DC")
    } else if score >= 55 && score < 60 {
        print("DD")
    } else if score >= 60 && score < 68 {
        print("CC")
    } else if score >= 68 && score < 76 {
        print("CB")
    } else if score >= 76 && score < 84 {
        print("BB")
    } else if score >= 84 && score < 92 {
        print("BA")
    } else if score >= 92 && score <= 100 {
        print("AA")
    }
}
else {
   print("FF")
}
```
```
CC
```

### Switch
```swift
switch modulus {
    case 0:
        print("Even")
        break
    case 1:
        print("Odd")
        break
    default:
        print("ANY!")
}
```
```
Even
```
- Guard Let
```swift
var isNumeric = "5"
var notNumeric = "A"

func convertToInteger(value : String) -> Int {
    guard let result = Int(value) else {
        return 0
    }
    return result
}
```
```swift
convertToInteger(value: isNumeric)
convertToInteger(value: notNumeric)
```
```
5 0
```

- If Let
```swift
var isNumeric = "5"
var notNumeric = "A"

func convertToInteger(value : String) -> Int {
    if let result = Int(value) {
        return result
    } else {
        return 0
    }
}
```
```swift
convertToInteger(value: isNumeric)
convertToInteger(value: notNumeric)
```
```
5 0
```
