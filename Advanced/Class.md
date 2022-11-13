# Class
Classes are general-purpose, flexible constructs that become the building blocks of your program code. 
You define properties and methods to add functionality to your structures and classes using the same syntax you use to define constants, 
variables, and methods. Classes are reference types.
Objects have two properties, state and behavior.

- Define the Properties of the Class:
They are properties of objects. Here language, developer, year and type variables are properties.
```swift
class Languages { 
    var language : String
    var developer : String
    var year : Int
    
    init(initLanguage : String, initDeveloper : String, initYear : Int) {
        self.language = initLanguage
        self.developer = initDeveloper
        self.year = initYear
        
        print("Created Language Object!")
    }
}
```
- Create an Instance of the Class:
```swift
let kotlin = Languages(initLanguage: "Kotlin", initDeveloper: "JetBrains", initYear: 2014)
```
