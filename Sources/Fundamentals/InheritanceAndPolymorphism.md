# Inheritance
Bir class'ın veya struct'un, başka bir sınıftan özellikleri ve metotları miras almasına "inheritance" denir. Bir class başka bir class'dan miras aldığında, miras alan class'a "subclass", miras aldığı class'a ise "superclass" denir.

### Superclass
Başka bir class'dan miras almayan, propertylerini ve methodlarını subclass'lara aktaran class'a "superclass" denir.

```swift
enum Fuel {
    case GASOLINE,DIESEL,HYDROGEN,HYBRID,ELECTRIC
}

class Vehicle {
    var weight: Double
    var width: Double
    var height: Double
    var length: Double
    var fuel: Fuel
    
    init(weight: Double, width: Double, height: Double, length: Double, fuel: Fuel) {
        self.weight = weight
        self.width = width
        self.height = height
        self.length = length
        self.fuel = fuel
        print("Created Vahicle")
    }
    
    func dimensions(){
        print("Vehicle Dimensions: \(self.width) x \(self.height) x \(self.length) and Weight \(self.weight)")
    }
}
```
### Subclass
Yeni bir class'ı var olan bir class'a dayandırma sürecidir. Subclass, daha sonra genişletebileceğiniz veya değiştirebileceğiniz var olan class'ın özelliklerini devralır. Ayrıca subclass'a yeni özellikler veya metotlar eklenebilir.

- "super" belirteci, superclass'ın propertylerine ve metholarına erişmek için kullanılır.
- "override" belirteci, bir class'ın methodlarına, o class'dan türetilen başka bir class'a aynı adlı bir method tanımlayarak superclass'daki methodla değiştirilmesi anlamına gelir. Bu işlem, bir method'un aynı class'dan türetilen farklı classlarda farklı işlevler gerçekleştirmesine olanak tanır. Superclass'daki method, subclass'daki method'un adından önce override anahtar sözcüğünin eklenmesi ile geçersiz kılınır.

```swift
enum Segment {
    case A,B,C,D,E,F,J,M,S
}

class Car: Vehicle {
    var segment: Segment
    var passenger: Int = 0
    
    init(segment: Segment, passenger: Int, weight: Double, width: Double, height: Double, length: Double, fuel: Fuel) {
        self.segment = segment
        self.passenger = passenger
        super.init(weight: weight, width: width, height: height, length: length, fuel: fuel)
        
        print("Created Car")
    }
    
    func superDimensions(){
        super.dimensions()
    }
    
    override func dimensions() {
        print("This car is \(segment) segment")
    }
    
    func capacity(){
        print("This car has a capacity of \(passenger) passengers.")
    }
}
```

```swift
class Truck: Vehicle {
    var axle: Int
    var tonnage: Int
    
    init(axle: Int, tonnage: Int, weight: Double, width: Double, height: Double, length: Double, fuel: Fuel) {
        self.axle = axle
        self.tonnage = tonnage
        super.init(weight: weight, width: width, height: height, length: length, fuel: fuel)
        print("Created Truck")
    }
    
    func superDimensions(){
        super.dimensions()
    }
    
    override func dimensions() {
        print("This truck has \(axle) axles.")
    }
    
    func limit(){
        print("The load carrying capacity of this truck is \(tonnage) tons.")
    }
}
```

```swift
let car = Car(segment: .B, passenger: 5, weight: 1120, width: 4065, height: 1450, length: 1750, fuel: .GASOLINE)
car.superDimensions()
car.dimensions()
car.capacity()
```
```
Created Vahicle
Created Car
Vehicle Dimensions: 4065.0 x 1450.0 x 1750.0 and Weight 1120.0
This car is B segment
This car has a capacity of 5 passengers.
```

```swift
let truck = Truck(axle: 3, tonnage: 35, weight: 2400, width: 5800, height: 3950, length: 1930, fuel: .DIESEL)
truck.superDimensions()
truck.dimensions()
truck.limit()
```
```
Created Vahicle
Created Truck
Vehicle Dimensions: 5800.0 x 3950.0 x 1930.0 and Weight 2400.0
This truck has 3 axles.
The load carrying capacity of this truck is 35 tons.
```

### Static, Class ve Final Keywords

- Static: Subclass'da override edilemezler. Superclass ve subclass üzerinden çağrılabilir fakat object üzerinden çağrılamazlar. Struct ve Class için geçerlidir.

```swift
struct Sphere {
    static var radius : Double = 0.0
    
    static func solve(_ radius: Double) -> (diameter: Double, area: Double, volume: Double) {
        return (radius * 2, 4 * Double.pi * pow(radius,2), (4 / 3) * Double.pi * pow(radius,3))
    }
}

Sphere.radius = 2.0
Sphere.solve(Sphere.radius)
```
```
2.0 (diameter: 4.0, area: 50.26548245743669, volume: 33.510321638291124)
```

- Class: Subclass'da override edilebilirler. Superclass ve subclass üzerinden çağrılabilir fakat object üzerinden çağrılamazlar. Sadece Class için geçerlidir.

```swift

```
```

```

- Final: Subclass'da override edilemezler. Superclass ve Subclass'dan instance edilen object üzerinden çağrılabilirler fakat class üzerinden çağrılamazlar. Sadece Class için geçerlidir.

```swift

```
```

```

# Polymorphism
Farklı class'lardaki object'lerin ortak bir superclass veya protocol nesneleri olarak ele alınmasına olanak tanır. Ortak bir arayüze veya protocol'e uydukları sürece farklı türlerdeki object'lerin birbirinin yerine kullanılabilmesini sağlar.

```swift
let car = Car(segment: .B, passenger: 5, weight: 1120, width: 4065, height: 1450, length: 1750, fuel: .GASOLINE)
let truck = Truck(axle: 3, tonnage: 35, weight: 2400, width: 5800, height: 3950, length: 1930, fuel: .DIESEL)
let other = Car(segment: .S, passenger: 1, weight: 1100, width: 3100, height: 1200, length: 1650, fuel: .HYBRID)

var vehicles: [Vehicle] = [car,truck,other]

for vehicle in vehicles {
    print(vehicle.dimensions())
}
```
```
Created Vahicle
Created Car
Created Vahicle
Created Truck
Created Vahicle
Created Car
This car is B segment
This truck has 3 axles.
This car is S segment
```

## Type Casting
Superclass'ın subclass'a dönüştürülmesine <b>"DOWNCASTING"</b>, subclass'ın superclass'a dönüştürülmesine <b>"UPCASTING"</b> denir.

- is -> Tip kontrolü için kullanılır.
- as -> Bir tipi diğerine dönüştürmek için kullanılır.
- as! (Force Downcasting) -> Bir tipi diğerine dönüştürmek için kullanılır. Başarılı ise değer, başarısız ise hata döndürür.
- as? (Optional Downcasting) -> Dönüştürme sırasında isteğe bağlı bir veri varsa kullanılır. Başarılı ise değer, başarısız ise nil döndürür.
