# Swift Cheat Sheet

Comprehensive reference for Swift programming language covering iOS development basics, syntax, protocols, and essential features for modern Swift development.

---

## Table of Contents
- [Basic Syntax](#basic-syntax)
- [Variables and Constants](#variables-and-constants)
- [Data Types](#data-types)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Classes and Structures](#classes-and-structures)
- [Protocols](#protocols)
- [Optionals](#optionals)
- [Collections](#collections)
- [Error Handling](#error-handling)
- [Memory Management](#memory-management)
- [iOS Development Basics](#ios-development-basics)

---

## Basic Syntax

| Feature | Syntax | Example |
|---------|--------|---------|
| Print | `print()` | `print("Hello, World!")` |
| Comments | `//` or `/* */` | `// Single line` |
| Multi-line String | `"""..."""` | `"""Line 1\nLine 2"""` |
| String Interpolation | `\()` | `"Hello \(name)"` |
| Semicolons | Optional | `let x = 5; let y = 10` |
| Type Annotation | `: Type` | `let name: String = "Swift"` |

### Basic Program Structure
```swift
import Foundation

// Entry point for command-line programs
print("Hello, World!")

// Variables and constants
let constant = "I cannot change"
var variable = "I can change"

// String interpolation
let name = "Swift"
print("Hello, \(name)!")

// Multi-line string
let multiLine = """
    This is a
    multi-line string
    """
```

## Variables and Constants

### Declaration
```swift
// Constants (immutable)
let pi = 3.14159
let appName: String = "MyApp"

// Variables (mutable)
var counter = 0
var userName: String = "user"

// Type inference
let number = 42        // Int
let price = 29.99      // Double
let message = "Hello"  // String
let isActive = true    // Bool

// Multiple declarations
let x = 10, y = 20, z = 30
var a, b, c: Double
a = 1.0; b = 2.0; c = 3.0

// Computed properties
var fullName: String {
    return "\(firstName) \(lastName)"
}

var temperature: Double {
    get {
        return celsius
    }
    set {
        celsius = newValue
    }
}
```

### Property Observers
```swift
var score: Int = 0 {
    willSet {
        print("About to set score to \(newValue)")
    }
    didSet {
        print("Score changed from \(oldValue) to \(score)")
        if score > highScore {
            highScore = score
        }
    }
}
```

## Data Types

### Basic Types
```swift
// Integer types
let smallNumber: Int8 = 127
let mediumNumber: Int16 = 32767
let largeNumber: Int32 = 2147483647
let hugeNumber: Int64 = 9223372036854775807
let regularInt: Int = 42        // Platform-dependent (32 or 64-bit)

// Unsigned integers
let unsignedByte: UInt8 = 255
let unsignedInt: UInt = 42

// Floating point
let pi: Float = 3.14159         // 32-bit
let precisePi: Double = 3.14159265359  // 64-bit (default)

// Boolean
let isSwiftAwesome: Bool = true

// Character and String
let character: Character = "A"
let string: String = "Hello, Swift!"

// Unicode
let unicodeString = "Hello 👋 Swift 🚀"
let emoji: Character = "🦄"
```

### Type Conversion and Casting
```swift
// Explicit conversion
let intValue = 42
let doubleValue = Double(intValue)
let stringValue = String(intValue)

// Type casting
let someValue: Any = "This is a string"

// Conditional casting (returns optional)
if let stringValue = someValue as? String {
    print("It's a string: \(stringValue)")
}

// Forced casting (dangerous - can crash)
let forcedString = someValue as! String

// Type checking
if someValue is String {
    print("It's a string")
}
```

### Tuples
```swift
// Basic tuple
let coordinates = (3, 5)
let x = coordinates.0  // 3
let y = coordinates.1  // 5

// Named elements
let person = (name: "John", age: 30)
print(person.name)     // John
print(person.age)      // 30

// Destructuring
let (width, height) = (1920, 1080)
print(width)  // 1920

// Ignoring values
let (name, _) = ("Alice", 25)  // Ignore age

// Function returning tuple
func getCoordinates() -> (x: Int, y: Int) {
    return (10, 20)
}

let point = getCoordinates()
print(point.x, point.y)
```

## Control Flow

### Conditional Statements
```swift
// if-else
let temperature = 25
if temperature > 30 {
    print("It's hot!")
} else if temperature < 10 {
    print("It's cold!")
} else {
    print("It's mild!")
}

// Ternary operator
let weather = temperature > 25 ? "hot" : "cool"

// guard statement (early exit)
func greet(name: String?) {
    guard let name = name else {
        print("No name provided")
        return
    }
    print("Hello, \(name)!")
}

// switch statement
let grade = "A"
switch grade {
case "A":
    print("Excellent!")
case "B", "C":
    print("Good job!")
case "D":
    print("You can do better")
case "F":
    print("Sorry, you failed")
default:
    print("Invalid grade")
}

// Switch with ranges
let score = 85
switch score {
case 90...100:
    print("A")
case 80..<90:
    print("B")
case 70..<80:
    print("C")
case 60..<70:
    print("D")
default:
    print("F")
}

// Switch with tuples
let point = (1, 1)
switch point {
case (0, 0):
    print("Origin")
case (_, 0):
    print("On x-axis")
case (0, _):
    print("On y-axis")
case (-2...2, -2...2):
    print("Inside the square")
default:
    print("Outside the square")
}
```

### Loops
```swift
// for-in loop
for i in 1...5 {
    print(i)
}

// for-in with array
let names = ["Alice", "Bob", "Charlie"]
for name in names {
    print("Hello, \(name)")
}

// for-in with enumerated (index and value)
for (index, name) in names.enumerated() {
    print("\(index): \(name)")
}

// for-in with stride
for i in stride(from: 0, to: 10, by: 2) {
    print(i)  // 0, 2, 4, 6, 8
}

for i in stride(from: 10, through: 0, by: -2) {
    print(i)  // 10, 8, 6, 4, 2, 0
}

// while loop
var count = 0
while count < 5 {
    print(count)
    count += 1
}

// repeat-while loop (do-while equivalent)
repeat {
    print("This runs at least once")
    count += 1
} while count < 3

// Loop control
for i in 1...10 {
    if i == 3 {
        continue  // Skip 3
    }
    if i == 8 {
        break    // Stop at 8
    }
    print(i)
}

// Labeled statements
outerLoop: for i in 1...3 {
    for j in 1...3 {
        if i == 2 && j == 2 {
            break outerLoop
        }
        print("\(i), \(j)")
    }
}
```

## Functions

### Function Declaration
```swift
// Basic function
func greet() {
    print("Hello!")
}

// Function with parameters
func greet(name: String) {
    print("Hello, \(name)!")
}

// Function with return value
func add(a: Int, b: Int) -> Int {
    return a + b
}

// Function with multiple return values
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    
    return (currentMin, currentMax)
}

let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min: \(bounds.min), max: \(bounds.max)")
```

### Advanced Function Features
```swift
// External and internal parameter names
func greet(to name: String, from hometown: String) {
    print("Hello \(name)! Greetings from \(hometown)")
}
greet(to: "Alice", from: "New York")

// Default parameter values
func greet(name: String, greeting: String = "Hello") {
    print("\(greeting), \(name)!")
}
greet(name: "Bob")  // Uses default greeting

// Variadic parameters
func average(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
print(average(1, 2, 3, 4, 5))

// In-out parameters (pass by reference)
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var x = 3, y = 5
swapTwoInts(&x, &y)
print("x: \(x), y: \(y)")  // x: 5, y: 3

// Function types
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}

var mathFunction: (Int, Int) -> Int = addTwoInts
print(mathFunction(2, 3))  // 5

// Functions as parameters
func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
    print("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)

// Functions as return types
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    
    return backward ? stepBackward : stepForward
}
```

### Closures
```swift
// Basic closure
let sayHello = { print("Hello!") }
sayHello()

// Closure with parameters and return value
let multiply = { (a: Int, b: Int) -> Int in
    return a * b
}
print(multiply(4, 5))

// Closures as function parameters
func performOperation(_ a: Int, _ b: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

let result = performOperation(10, 5) { (x, y) -> Int in
    return x + y
}

// Simplified closure syntax
let numbers = [1, 2, 3, 4, 5]

// Full syntax
let doubled1 = numbers.map({ (number: Int) -> Int in
    return number * 2
})

// Inferred types
let doubled2 = numbers.map({ number in
    return number * 2
})

// Implicit return
let doubled3 = numbers.map({ number in number * 2 })

// Shorthand argument names
let doubled4 = numbers.map({ $0 * 2 })

// Trailing closure
let doubled5 = numbers.map() { $0 * 2 }
let doubled6 = numbers.map { $0 * 2 }

// Capturing values
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

let incrementByTen = makeIncrementer(forIncrement: 10)
print(incrementByTen())  // 10
print(incrementByTen())  // 20
```

## Classes and Structures

### Structures
```swift
struct Point {
    var x: Double
    var y: Double
    
    // Initializer
    init(x: Double, y: Double) {
        self.x = x
        self.y = y
    }
    
    // Method
    func distance(to other: Point) -> Double {
        let dx = x - other.x
        let dy = y - other.y
        return sqrt(dx * dx + dy * dy)
    }
    
    // Mutating method (can modify properties)
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
    
    // Static method
    static func origin() -> Point {
        return Point(x: 0, y: 0)
    }
}

var point1 = Point(x: 1.0, y: 2.0)
let point2 = Point(x: 4.0, y: 6.0)
print(point1.distance(to: point2))

point1.moveBy(x: 2.0, y: 3.0)
let originPoint = Point.origin()
```

### Classes
```swift
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    
    func makeNoise() {
        // Default implementation does nothing
    }
}

class Car: Vehicle {
    var gear = 1
    
    override var description: String {
        return super.description + " in gear \(gear)"
    }
    
    override func makeNoise() {
        print("Vroom vroom!")
    }
}

// Initialization
class Person {
    let name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    convenience init(name: String) {
        self.init(name: name, age: 0)
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

// Property observers in classes
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
```

### Access Control
```swift
public class PublicClass {}
internal class InternalClass {}  // Default
fileprivate class FilePrivateClass {}
private class PrivateClass {}

class SomeClass {
    private var privateProperty = "private"
    fileprivate var filePrivateProperty = "file private"
    internal var internalProperty = "internal"  // Default
    public var publicProperty = "public"
    
    private func privateMethod() {}
    public func publicMethod() {}
}
```

## Protocols

### Protocol Definition and Adoption
```swift
protocol Drawable {
    var area: Double { get }
    func draw()
}

protocol Named {
    var name: String { get set }
}

struct Circle: Drawable {
    var radius: Double
    
    var area: Double {
        return Double.pi * radius * radius
    }
    
    func draw() {
        print("Drawing a circle with radius \(radius)")
    }
}

class Rectangle: Drawable, Named {
    var width: Double
    var height: Double
    var name: String
    
    init(width: Double, height: Double, name: String) {
        self.width = width
        self.height = height
        self.name = name
    }
    
    var area: Double {
        return width * height
    }
    
    func draw() {
        print("Drawing rectangle \(name): \(width) x \(height)")
    }
}

// Protocol as type
let shapes: [Drawable] = [
    Circle(radius: 5),
    Rectangle(width: 10, height: 8, name: "MyRect")
]

for shape in shapes {
    shape.draw()
    print("Area: \(shape.area)")
}
```

### Protocol Extensions
```swift
protocol Vehicle {
    var numberOfWheels: Int { get }
    var color: String { get set }
    
    func accelerate()
    func stop()
}

extension Vehicle {
    // Default implementation
    func stop() {
        print("Vehicle is stopping")
    }
    
    var description: String {
        return "\(color) vehicle with \(numberOfWheels) wheels"
    }
}

struct Bicycle: Vehicle {
    let numberOfWheels = 2
    var color: String
    
    func accelerate() {
        print("Pedaling faster!")
    }
}

// Protocol inheritance
protocol ElectricVehicle: Vehicle {
    var batteryLevel: Double { get set }
    func charge()
}

// Associated types
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

struct IntStack: Container {
    typealias Item = Int
    
    var items = [Int]()
    
    mutating func append(_ item: Int) {
        items.append(item)
    }
    
    var count: Int {
        return items.count
    }
    
    subscript(i: Int) -> Int {
        return items[i]
    }
}
```

### Protocol-Oriented Programming
```swift
protocol Flyable {
    func fly()
}

protocol Swimmable {
    func swim()
}

struct Duck: Flyable, Swimmable {
    func fly() {
        print("Duck is flying")
    }
    
    func swim() {
        print("Duck is swimming")
    }
}

// Using protocol composition
func moveAround(_ creature: Flyable & Swimmable) {
    creature.fly()
    creature.swim()
}

let duck = Duck()
moveAround(duck)

// Conditional conformance
extension Array: Flyable where Element: Flyable {
    func fly() {
        for element in self {
            element.fly()
        }
    }
}
```

## Optionals

### Optional Basics
```swift
// Optional declaration
var optionalString: String? = "Hello"
var optionalInt: Int? = nil

// Force unwrapping (dangerous if nil)
if optionalString != nil {
    print(optionalString!)  // Use ! to force unwrap
}

// Optional binding (safe unwrapping)
if let actualString = optionalString {
    print(actualString)     // No need for !
} else {
    print("optionalString is nil")
}

// Multiple optional binding
if let string = optionalString,
   let number = optionalInt {
    print("\(string) and \(number)")
}

// Guard let (early exit)
func processOptional(_ value: String?) {
    guard let unwrappedValue = value else {
        print("Value is nil")
        return
    }
    print("Value is: \(unwrappedValue)")
}
```

### Optional Chaining
```swift
class Person {
    var residence: Residence?
}

class Residence {
    var address: Address?
    var numberOfRooms = 1
}

class Address {
    var street: String?
    var city: String?
}

let person = Person()

// Optional chaining
if let roomCount = person.residence?.numberOfRooms {
    print("Person has \(roomCount) room(s)")
} else {
    print("Unable to retrieve number of rooms")
}

// Chaining multiple levels
if let street = person.residence?.address?.street {
    print("Street: \(street)")
} else {
    print("Unable to retrieve street")
}

// Calling methods through optional chaining
person.residence?.address?.buildingIdentifier()?.hasPrefix("The")
```

### Nil-Coalescing Operator
```swift
let defaultColorName = "red"
var userDefinedColorName: String?

// Nil-coalescing operator
var colorNameToUse = userDefinedColorName ?? defaultColorName
// Equivalent to:
// colorNameToUse = userDefinedColorName != nil ? userDefinedColorName! : defaultColorName

// Chaining nil-coalescing
let first: String? = nil
let second: String? = nil  
let third: String? = "Third"
let result = first ?? second ?? third ?? "Default"  // "Third"
```

### Implicitly Unwrapped Optionals
```swift
// Sometimes you know an optional will always have a value
let possibleString: String? = "An optional string."
let forcedString: String = possibleString!  // Requires !

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString  // No need for !

// Still can be treated as optional
if assumedString != nil {
    print(assumedString!)
}

if let definiteString = assumedString {
    print(definiteString)
}
```

## Collections

### Arrays
```swift
// Array creation
var fruits = ["Apple", "Banana", "Cherry"]
var numbers: [Int] = []
var moreNumbers = [Int]()
var emptyArray = Array<String>()

// Array with default values
var threeDoubles = Array(repeating: 0.0, count: 3)

// Array operations
fruits.append("Date")
fruits += ["Elderberry", "Fig"]
fruits.insert("Apricot", at: 1)

let firstFruit = fruits[0]
fruits[1] = "Blueberry"
fruits[2...4] = ["Coconut", "Durian"]  // Replace range

let removedFruit = fruits.remove(at: 0)
let lastFruit = fruits.removeLast()

// Array properties and methods
print(fruits.count)
print(fruits.isEmpty)
fruits.reverse()
fruits.sort()

// Iterating
for fruit in fruits {
    print(fruit)
}

for (index, fruit) in fruits.enumerated() {
    print("\(index): \(fruit)")
}

// Array methods
let evenNumbers = numbers.filter { $0 % 2 == 0 }
let doubled = numbers.map { $0 * 2 }
let sum = numbers.reduce(0, +)
```

### Dictionaries
```swift
// Dictionary creation
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
var nameOfIntegers: [Int: String] = [:]
var emptyDict = [String: String]()

// Dictionary operations
airports["LHR"] = "London Heathrow"
airports["LHR"] = "London"  // Update value

if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("Old value was \(oldValue)")
}

let airportName = airports["DUB"]  // Optional String
let airportName2 = airports["DUB"] ?? "Unknown"

airports["YYZ"] = nil  // Remove key-value pair
airports.removeValue(forKey: "DUB")

// Dictionary properties and methods
print(airports.count)
print(airports.isEmpty)

// Iterating
for (code, name) in airports {
    print("\(code): \(name)")
}

for code in airports.keys {
    print("Code: \(code)")
}

for name in airports.values {
    print("Airport: \(name)")
}

// Convert keys/values to arrays
let codes = Array(airports.keys)
let names = Array(airports.values)
```

### Sets
```swift
// Set creation
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
var emptySet = Set<Int>()

// Set operations
favoriteGenres.insert("Jazz")
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre) was removed")
}

print(favoriteGenres.contains("Funk"))  // false

// Set operations
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

// Union
let unionSet = oddDigits.union(evenDigits).sorted()

// Intersection  
let intersectionSet = oddDigits.intersection(singleDigitPrimeNumbers).sorted()

// Symmetric difference
let symmetricDiffSet = oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()

// Subtraction
let subtractionSet = oddDigits.subtracting(singleDigitPrimeNumbers).sorted()

// Set relationships
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)        // true
farmAnimals.isSuperset(of: houseAnimals)      // true
farmAnimals.isDisjoint(with: cityAnimals)     // true
```

## Error Handling

### Error Protocol and Throwing Functions
```swift
enum ValidationError: Error {
    case tooShort
    case tooLong
    case invalidCharacters
}

func validatePassword(_ password: String) throws -> Bool {
    if password.count < 8 {
        throw ValidationError.tooShort
    }
    if password.count > 128 {
        throw ValidationError.tooLong
    }
    
    let allowedCharacters = CharacterSet.alphanumerics
    if password.rangeOfCharacter(from: allowedCharacters.inverted) != nil {
        throw ValidationError.invalidCharacters
    }
    
    return true
}

// Handling errors with do-catch
do {
    try validatePassword("abc")
    print("Password is valid")
} catch ValidationError.tooShort {
    print("Password is too short")
} catch ValidationError.tooLong {
    print("Password is too long")
} catch ValidationError.invalidCharacters {
    print("Password contains invalid characters")
} catch {
    print("Unknown error: \(error)")
}

// Converting errors to optionals
let isValid = try? validatePassword("mypassword123")  // Optional Bool

// Disabling error propagation (only if you're sure it won't throw)
let isDefinitelyValid = try! validatePassword("validpassword123")

// Propagating errors
func processUserInput(_ input: String) throws -> String {
    try validatePassword(input)
    return input.uppercased()
}
```

### Defer Statements
```swift
func processFile(filename: String) throws {
    let file = openFile(named: filename)
    defer {
        closeFile(file)  // This will always execute
    }
    
    if someCondition {
        return  // defer block still executes
    }
    
    // Process file
    if someOtherCondition {
        throw SomeError.processingFailed  // defer block still executes
    }
    
    // More processing
} // defer block executes here too
```

### Result Type
```swift
func divide(_ dividend: Double, by divisor: Double) -> Result<Double, ArithmeticError> {
    guard divisor != 0 else {
        return .failure(.divisionByZero)
    }
    return .success(dividend / divisor)
}

let result = divide(10, by: 2)
switch result {
case .success(let value):
    print("Result: \(value)")
case .failure(let error):
    print("Error: \(error)")
}

// Using with higher-order functions
let results = [
    divide(10, by: 2),
    divide(10, by: 0),
    divide(15, by: 3)
]

let successes = results.compactMap { result in
    try? result.get()
}
```

## Memory Management

### Automatic Reference Counting (ARC)
```swift
class Person {
    let name: String
    var apartment: Apartment?
    
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

class Apartment {
    let unit: String
    weak var tenant: Person?  // weak reference to break retain cycle
    
    init(unit: String) {
        self.unit = unit
    }
    
    deinit {
        print("Apartment \(unit) is being deinitialized")
    }
}

// Strong reference cycle example
var john: Person? = Person(name: "John")
var unit4A: Apartment? = Apartment(unit: "4A")

john!.apartment = unit4A
unit4A!.tenant = john      // Use weak var tenant to break the cycle

john = nil    // Person will be deallocated because tenant is weak
unit4A = nil  // Apartment will be deallocated
```

### Weak and Unowned References
```swift
class Customer {
    let name: String
    var card: CreditCard?
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

class CreditCard {
    let number: UInt64
    unowned let customer: Customer  // unowned reference
    
    init(number: UInt64, customer: Customer) {
        self.number = number
        self.customer = customer
    }
    
    deinit {
        print("Card #\(number) is being deinitialized")
    }
}

var john: Customer? = Customer(name: "John Appleseed")
john!.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)

john = nil  // Both Customer and CreditCard are deallocated

// Unowned optional references
class Department {
    var name: String
    var courses: [Course]
    
    init(name: String) {
        self.name = name
        self.courses = []
    }
}

class Course {
    var name: String
    unowned var department: Department
    unowned var nextCourse: Course?
    
    init(name: String, in department: Department) {
        self.name = name
        self.department = department
        self.nextCourse = nil
    }
}
```

### Closures and Capture Lists
```swift
class HTMLElement {
    let name: String
    let text: String?
    
    lazy var asHTML: () -> String = { [unowned self] in
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

// Capture list examples
var someString = "Hello"
let closure = { [someString] in  // Capture by value
    print(someString)
}

someString = "World"
closure()  // Prints "Hello"

// Weak capture
class ViewController {
    func setupButton() {
        button.onTap = { [weak self] in
            self?.handleTap()  // self is optional
        }
    }
    
    func handleTap() {
        print("Button tapped")
    }
}
```

## iOS Development Basics

### UIKit Fundamentals
```swift
import UIKit

class ViewController: UIViewController {
    @IBOutlet weak var label: UILabel!
    @IBOutlet weak var button: UIButton!
    @IBOutlet weak var textField: UITextField!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        // View is about to appear
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        // View has appeared
    }
    
    func setupUI() {
        label.text = "Hello, iOS!"
        label.textColor = .systemBlue
        button.setTitle("Tap Me", for: .normal)
        button.backgroundColor = .systemBlue
        button.layer.cornerRadius = 8
    }
    
    @IBAction func buttonTapped(_ sender: UIButton) {
        guard let text = textField.text, !text.isEmpty else {
            showAlert(message: "Please enter some text")
            return
        }
        
        label.text = "You entered: \(text)"
        textField.text = ""
    }
    
    func showAlert(message: String) {
        let alert = UIAlertController(title: "Alert",
                                    message: message,
                                    preferredStyle: .alert)
        
        alert.addAction(UIAlertAction(title: "OK", style: .default))
        present(alert, animated: true)
    }
}
```

### SwiftUI Basics
```swift
import SwiftUI

struct ContentView: View {
    @State private var name = ""
    @State private var showingAlert = false
    
    var body: some View {
        VStack(spacing: 20) {
            Text("Hello, SwiftUI!")
                .font(.largeTitle)
                .foregroundColor(.blue)
            
            TextField("Enter your name", text: $name)
                .textFieldStyle(RoundedBorderTextFieldStyle())
                .padding(.horizontal)
            
            Button("Say Hello") {
                showingAlert = true
            }
            .buttonStyle(RoundedButtonStyle())
            
            if !name.isEmpty {
                Text("Hello, \(name)!")
                    .font(.title2)
                    .transition(.slide)
            }
        }
        .padding()
        .alert("Hello!", isPresented: $showingAlert) {
            Button("OK") { }
        } message: {
            Text("Nice to meet you!")
        }
    }
}

struct RoundedButtonStyle: ButtonStyle {
    func makeBody(configuration: Configuration) -> some View {
        configuration.label
            .padding()
            .background(Color.blue)
            .foregroundColor(.white)
            .clipShape(RoundedRectangle(cornerRadius: 10))
            .scaleEffect(configuration.isPressed ? 0.95 : 1.0)
            .animation(.easeInOut(duration: 0.1), value: configuration.isPressed)
    }
}

// Preview
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

### Data Persistence
```swift
// UserDefaults
func saveUserPreference() {
    UserDefaults.standard.set("dark", forKey: "theme")
    UserDefaults.standard.set(true, forKey: "notificationsEnabled")
}

func loadUserPreference() {
    let theme = UserDefaults.standard.string(forKey: "theme") ?? "light"
    let notificationsEnabled = UserDefaults.standard.bool(forKey: "notificationsEnabled")
}

// Codable for JSON persistence
struct User: Codable {
    let id: Int
    let name: String
    let email: String
}

func saveUser(_ user: User) {
    let encoder = JSONEncoder()
    if let encoded = try? encoder.encode(user) {
        UserDefaults.standard.set(encoded, forKey: "savedUser")
    }
}

func loadUser() -> User? {
    guard let userData = UserDefaults.standard.data(forKey: "savedUser") else {
        return nil
    }
    
    let decoder = JSONDecoder()
    return try? decoder.decode(User.self, from: userData)
}

// File system
func getDocumentsDirectory() -> URL {
    FileManager.default.urls(for: .documentDirectory, 
                           in: .userDomainMask)[0]
}

func saveToFile(_ data: Data, filename: String) {
    let url = getDocumentsDirectory().appendingPathComponent(filename)
    try? data.write(to: url)
}

func loadFromFile(filename: String) -> Data? {
    let url = getDocumentsDirectory().appendingPathComponent(filename)
    return try? Data(contentsOf: url)
}
```

### Networking
```swift
import Foundation

// Simple GET request
func fetchData(completion: @escaping (Result<Data, Error>) -> Void) {
    guard let url = URL(string: "https://api.example.com/data") else {
        completion(.failure(URLError(.badURL)))
        return
    }
    
    URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            completion(.failure(error))
            return
        }
        
        guard let data = data else {
            completion(.failure(URLError(.badServerResponse)))
            return
        }
        
        completion(.success(data))
    }.resume()
}

// Async/await (iOS 15+)
@available(iOS 15.0, *)
func fetchDataAsync() async throws -> Data {
    guard let url = URL(string: "https://api.example.com/data") else {
        throw URLError(.badURL)
    }
    
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}

// JSON decoding
struct Post: Codable {
    let id: Int
    let title: String
    let body: String
    let userId: Int
}

func fetchPosts(completion: @escaping (Result<[Post], Error>) -> Void) {
    guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else {
        completion(.failure(URLError(.badURL)))
        return
    }
    
    URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            completion(.failure(error))
            return
        }
        
        guard let data = data else {
            completion(.failure(URLError(.badServerResponse)))
            return
        }
        
        do {
            let posts = try JSONDecoder().decode([Post].self, from: data)
            completion(.success(posts))
        } catch {
            completion(.failure(error))
        }
    }.resume()
}
```

---

## Resources
- [Swift Programming Language Guide](https://docs.swift.org/swift-book/)
- [Apple Developer Documentation](https://developer.apple.com/documentation/)
- [Swift.org](https://swift.org/)
- [iOS App Development with Swift](https://developer.apple.com/tutorials/app-dev-training)
- [SwiftUI Tutorials](https://developer.apple.com/tutorials/swiftui)

---
*Originally compiled from various sources. Contributions welcome!*