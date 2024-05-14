# Stored Properties
A constant or variable stored as part of an instance of a class or structure. Stored properties can be mutable stored properties (declared with the var keyword) or immutable stored properties (declared with the let keyword).

```swift
struct User {
    var name: String
    var surname: String
}

var user = User(name: "Omer", surname: "Koc")
print(user)

user.name = "Omer Can"
print(user)
```
```
User(name: "Omer", surname: "Koc")
User(name: "Omer Can", surname: "Koc")
```

### Lazy Stored Properties
It is a property that has no value until first use. They cannot be used with immutable (let) and computed properties.

```swift
struct User {
    var name: String
    var surname: String
    
    lazy var username: String = {
        return (self.name.lowercased() + "." + self.surname.lowercased())
            .replacingOccurrences(of: " ", with: "")
    }()
}
```
```swift
var user = User(name: "Omer Can", surname: "KOC")
print(user)
```
```
User(name: "Omer Can", surname: "KOC", $__lazy_storage_$_username: nil)
```
```swift
_ = user.username
print(user)
```
```
User(name: "Omer Can", surname: "KOC", $__lazy_storage_$_username: Optional("omercan.koc"))
```

## Computed Properties
They are variables that take value as a result of operations determined within a class, structure or enumeration. They implement the "get" method for access and the optional "set" method for assignment.

### Getter and Setter Declaration
```swift
struct Body {
    var area: Double = 0.0
    var volume: Double = 0.0
}

struct Radius {
    var radius: Double = 0.0
}

struct Sphere {
    var radius = Radius()
    var body: Body {
        get {
            let area = 4 * Double.pi * pow(self.radius.radius,2)
            let volume = (4 / 3) * Double.pi * pow(radius.radius,3)
            return Body(area: area, volume: volume)
        }
        
        set(new) {
            if new.area != 0.0 {
                radius.radius = pow(new.area / (4 * Double.pi), 1/2)
            } else if new.volume != 0.0 {
                radius.radius = pow(new.volume / ((4/3) * Double.pi), 1/3)
            } else {
                radius.radius = 0.0
            }
        }
    }
}
```
```swift
var sphere: Sphere = Sphere(radius: Radius(radius: 2.0))
print(sphere, sphere.body.area, sphere.body.volume)

sphere.body = Body(area: 50.26548245743669)
print(sphere)

sphere.body = Body(volume: 33.510321638291124)
print(sphere)
```
```
Sphere(radius: Console.Radius(radius: 2.0)) 50.26548245743669 33.510321638291124
Sphere(radius: Console.Radius(radius: 2.0))
Sphere(radius: Console.Radius(radius: 2.0))
```

### Shorthand Getter and Setter Declaration
```swift
struct Body {
    var area: Double = 0.0
    var volume: Double = 0.0
}

struct Radius {
    var radius: Double = 0.0
}

struct Sphere {
    var radius = Radius()
    var body: Body {
        get {
            Body(area: 4 * Double.pi * pow(self.radius.radius,2), volume: (4 / 3) * Double.pi * pow(radius.radius,3))
        }
        
        set {
            if newValue.area != 0.0 {
                radius.radius = pow(newValue.area / (4 * Double.pi), 1/2)
            } else if newValue.volume != 0.0 {
                radius.radius = pow(newValue.volume / ((4/3) * Double.pi), 1/3)
            } else {
                radius.radius = 0.0
            }
        }
    }
}
```
### Read-Only Computed Properties
```swift
struct Body {
    var area: Double = 0.0
    var volume: Double = 0.0
}

struct Radius {
    var radius: Double = 0.0
}

struct Sphere {
    var radius = Radius()
    var body: Body {
        get {
            Body(area: 4 * Double.pi * pow(self.radius.radius,2), volume: (4 / 3) * Double.pi * pow(radius.radius,3))
        }
    }
}
```
```swift
var sphere: Sphere = Sphere(radius: Radius(radius: 2.0))
print(sphere, sphere.body.area, sphere.body.volume)
```
```
Sphere(radius: Console.Radius(radius: 2.0)) 50.26548245743669 33.510321638291124
```

## Property Observers
Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.
```swift
class Logic {
    var status : Bool = false {
        willSet {
            print("WILL SET : Current Value -> \(status) : New Value -> \(newValue)")
        }
        
        didSet {
            print("DID SET : Current Value  -> \(status) : Old Value -> \(oldValue)")
        }
    }
}

var first = Logic()
first.status = true
```

```
WILL SET : Current Value -> false : New Value -> true
DID SET : Current Value  -> true : Old Value -> false
```

## Property Wrappers
It adds a layer of separation between the code that manages how the property is stored and the code that defines a property. When you use a feature wrapper, you write management code once when you define the wrapper and then reuse that management code by applying it to multiple features.

```swift
@propertyWrapper
struct Positive {
    var wrappedValue: Int
    
    init(wrappedValue: Int) {
        if wrappedValue < 0 { self.wrappedValue = 0 }
        else { self.wrappedValue = wrappedValue }
    }
}

struct Victory {
    var winner: String
    @Positive var score: Int
}
```
```swift
var victory = Victory(username: "victory", score: 120)
print(victory)
```
```
Victory(username: "victory", _score: Console.Positive(wrappedValue: 120))
```
```swift
var victory = Victory(username: "victory", score: -120)
print(victory)
```
```
Victory(username: "victory", _score: Console.Positive(wrappedValue: 0))
```

### Property Wrapper Properties
```swift
@propertyWrapper
struct Storage<T> {
    var storageKey: String
    var storageValue: T
    let storage: UserDefaults = .standard
    
    var wrappedValue: T {
        get {
            let value = storage.value(forKey: storageKey) as? T
            return value ?? storageValue
        }
        
        set {
            storage.setValue(newValue, forKey: storageKey)
        }
    }
}

struct LastWinner {
    @Storage(storageKey: "username", storageValue: "guest") var username: String
    @Storage(storageKey: "score", storageValue: 0) var score: Int
}
```

```swift
var lastWinner = LastWinner()
lastWinner.username = "lastWinner"
lastWinner.score = 95

print(lastWinner.username, lastWinner.score)
```
```
lastWinner 95
```
```swift
var lastWinner = LastWinner()

print(lastWinner.username, lastWinner.score)
```
```
lastWinner 95
```
