# Operators

### 1. Assignment Operator
Initializes or updates the value.
```swift
let count = 10
var item = 0
print("Count : \(count) and Item :\(item)")
item = count
print("Count : \(count) and Item :\(item)")
```
```
Count : 10 and Item :0
Count : 10 and Item :10
```
### 2. Arithmetic Operators
Swift supports the four standard arithmetic operators for all number types:
- Addition (+)
- Subtraction (-)
- Multiplication (*)
- Division (/)
- Remainder (%)
```swift
let additionClousure = {
    (first : Int, second : Int) -> Int in
    return first + second
}

let subractionClousure = {
    (first : Int, second : Int) -> Int in
    return first - second
}

let multiplicationClousure = {
    (first : Int, second : Int) -> Int in
    return first * second
}

let divisionClousure = {
    (first : Int, second : Int) -> Int in
    return first / second
}

func modulus(first : Int, second : Int) -> Int {
    return first % second
}
```

```swift
let addition = additionClousure(6,4) // 10
let subraction = subractionClousure(6,4) // 2
let multiplication = multiplicationClousure(6,4) // 24
let division = divisionClousure(6,4) // 1
modulus(first: 6, second: 4)
```
