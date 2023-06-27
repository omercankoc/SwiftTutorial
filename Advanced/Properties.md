## Properties
Properties associate values with a particular class, structure, or enumeration. 
Stored properties store constant and variable values as part of an instance, whereas computed properties calculate (rather than store) a value. 
Computed properties are provided by classes, structures, and enumerations. Stored properties are provided only by classes and structures.

## Stored Properties
In its simplest form, a stored property is a constant or variable that’s stored as part of an instance of a particular class or structure.

### Lazy Stored Properties
Properties whose value is not calculated until they are used or executed.
- It is used with variables (var), not constants (let).
- They are not used with Computed Properties.
```swift
struct Creator {
    static func fill(start: Int, end: Int) -> [Int] {
        var array : [Int] = []
        for index in start...end {
            array.append(index)
        }
        
        return array
    }
}

struct Indexs {
    var start : Int
    var end : Int
    
    lazy var all = {
        Creator.fill(start: start, end: end)
    }()
    
    lazy var between = {
        return "Numbers from \(start) to \(end)"
    }()
}

```

```swift
var numbers = Indexs(start: 1, end: 100)
```
```
Indexs(start: 1, end: 100, $__lazy_storage_$_all: nil, $__lazy_storage_$_between: nil)
```

```swift
numbers.between
numbers.all
```

```
Indexs(start: 1, end: 100, $__lazy_storage_$_all: Optional([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]), $__lazy_storage_$_between: Optional("Numbers from 1 to 100"))
```
