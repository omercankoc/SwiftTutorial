# Function

- Declaration
```swift
func message(){
    print("Hello!")
}
```
```swift
message()
```
```
Hello!
```

- Function Parameter(s)
```swift
func message(name : String){
    print("Hello \(name)!" )
}
```
```swift
message(name : "Omer")
```
```
Hello Omer!
```

- Return Value
```swift
func message(name: String, surname: String) -> String {
    return "Hello \(name) \(surname)!"
}
```
```swift
message(name: "Omer", surname: "Koc")
```
```
Hello Omer Koc!
```

### Overloading
```swift
func power(base: Int) -> Int {
    return base * base
}

func power(base: Int, exponent: Int) -> Int {
    var result = 1
    var iteration = 1
    
    while iteration <= exponent {
        result *= base
        iteration += 1
    }
    
    return result
}
```
```swift
power(base: 2)
power(base: 2, exponent: 3)
```
```
4
8
```

### Multiple Results
```swift
func endpoints(array: [Int]) -> (min: Int, max: Int) {
    var minimum = array[0]
    var maximum = array[0]
    for value in array[1..<array.count] {
        if value < minimum {
            minimum = value
        } else if value > maximum {
            maximum = value
        }
    }
    return (minimum, maximum)
}
```
```swift
var max : Int = endpoints(array: [1,1,2,3,5,8,13,21]).max
var min : Int = endpoints(array: [1,1,2,3,5,8,13,21]).min
```
```
21 1
```

### Variadic Parameters
```swift
func totalizer(values : Int...) -> Int {
    var total = 0
    for value in values {
        total += value
    }
    return total
}
```
```swift
var sum = totalizer(values: 1,2,3,4,5,6,7,8,9)
```
```
45
```

### Mutating Function
Mutating cannot be used with classes as it is a reference type.
The mutating keyword is only required if you are changing any properties contained within the struct. 
```swift
struct Sphere {
    var radius : Int?
    var area : Double?
    var circumference : Double?
    var volume : Double?
       
    mutating func parameters(radius : Int){
        self.radius = radius
        self.area = 4 * Double.pi * pow(Double(radius),2)
        self.circumference = 2 * Double.pi * Double(radius)
        self.volume = (4 / 3) * Double.pi * pow(Double(radius), 3)
    }
}
```
```swift
var sphere = Sphere(radius: 3, area: 113, circumference: 18, volume: 113)
print(sphere)

sphere.parameters(radius: 2)
print(sphere)
```
```
Sphere(radius: Optional(3), area: Optional(113.0), circumference: Optional(18.0), volume: Optional(113.0))
Sphere(radius: Optional(2), area: Optional(50.26548245743669), circumference: Optional(12.566370614359172), volume: Optional(33.510321638291124))
```

### Functions in "for" Keyword
```swift
struct Message {
    mutating func show(for type : Int) -> String {
        switch type {
        case 100:
            return "Information Responses"
        case 200:
            return "Successful Responses"
        case 300:
            return "Redirection Messages"
        case 400:
            return "Client Error Responses"
        case 500:
            return "Server Error Responses"
        default:
            return "Undefined"
        }
    }
}

var status = Message()
var message = status.show(for: 200)
print(message)
```
```
Successful Responses
```
### Functions in "_" Keyword
```swift
struct Messages {
    func status(_ code : Int) -> String {
        switch code {
        case 100 :
            return "Informational Responses"
        case 200:
            return "Successful Responses"
        case 300:
            return "Redirection Messages"
        case 400:
            return "Client Error Responses"
        case 500:
            return "Server Error Responses"
        default:
            return "Undefined"
        }
    }
}

var response = Messages()
var message = response.status(200)
```
```
Successful Responses
```
