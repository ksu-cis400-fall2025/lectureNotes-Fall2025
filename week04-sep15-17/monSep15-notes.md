# Lecture Notes: Interfaces and Inheritance
- ### Reminders
- **Interfaces Tutorial**: due Tuesday
- **Inheritance Tutorial**: due Wednesday
- **Milestone 3**: due Friday
	- Make sure your solution **builds**
- **Milestone 1** grades published yesterday.
	- Verify what you submitted.
- ## Today
	- **Classes** (Concrete) - Not Flexible
	- **Abstract Class**.  - Some Flexibility
	- **Interface**.     - Flexible
	- Polymorphism
	- Casting
- ---
- # Interfaces
  
  **What goes in an interface?**
	- Acts like a template of methods for concrete classes to implement
- Lists **properties** and **method signatures** (no implementation)
	- In the general concept of interface, **ONLY** method signatures, but
	- C# allows other entities
- **Purpose**
- Requires classes to have certain properties and methods
  
  **Naming convention**
- Interfaces start with `I` (e.g., `IAnimal`)
- Implementing an **existing interface**
- Implementing **multiple interfaces** → Yes, this is allowed
  
  ---
- ### Example: Chicken and Dog
- Suppose we want a list of chickens and dogs and to get each animal’s sound.
- **Questions:**
	- What do they have in common?
	- How could we refactor?
- Interfaces allow us to define shared **behavior declaration**, but the **behavior implementation** is different.
- ---
- # Abstract Classes
	- Declared with `abstract` keyword
	- Cannot create an object of that type directly
	- Often include abstract methods (no implementation)
	  
	  If any member is abstract → class must be abstract
- **Abstract class + interface**
	- An abstract class can implement an interface
	- Must declare all required members
	- Any unimplemented members remain abstract
- **Extending an Abstract Class**
  
  ```
  public class Child : AbstractClass
  ```
- Inherits public/protected members
- Must implement any abstract members, or else mark itself abstract
  
  ---
- ### Key Rules
	- Can implement **multiple interfaces**
	- Can extend only **one concrete class**
	- Can extend only **one abstract class**
	- Abstract class does **not** have to contain abstract members
		- You don't want anybody to make a 'generic' object (In C#)
- **Protected keyword**
	- Visible inside class and to descendants (children)
- ---
- ### Vocabulary
- Parent class → parent, base, super
- Child class → child, derived, sub
  
  ---
- ### Constructors and Inheritance
  
  ```
  Corgi c = new Corgi();
  ```
- Calls `Corgi` constructor → which calls `Dog` constructor → which calls `Animal` constructor
- Execution flows back up: `Animal` → `Dog` → `Corgi`
  
  **If parent constructor requires parameters**
	- Child constructor must supply them
- ---
- ### Examples
	- On Wednesday.
	  
	  ---
- ## Polymorphism in OOP
  
  **Polymorphism** means “many forms.” In OOP, it allows the same method, operator, or interface to work in different ways depending on the context.
  
  There are **three main types of polymorphism**:
- ## Inheritance
  
  **Purpose**
	- Less work, less duplicate code
	- Pull out common features
- **How is it different from interfaces?**
	- Interfaces: define requirements only
	- Inheritance: shares implementation
- **When should we refactor to use inheritance?**
	- Example: Drinks — price scaling logic is the same across sizes
	- Example: Entrees — bread + ingredients + size
- ---
- ### Extending a Regular Class
  
  ```
  public class Child : ParentClass
  ```
- Inherits public/protected properties and methods
- Child does not have to do anything unless overriding
  
  **Overriding Methods/Properties**
	- Parent: mark member as `virtual` (allows override)
	- Child: mark member as `override` (redefines behavior)
	  
	  Do we have to override? → No, just when necessarily
- ---
- ### 1. Subtype Polymorphism (Inheritance / Interfaces)
- Achieved when a **child class** that extends a **parent class**, or a concrete class implementing an **interface**, is treated as its **parent type**.
- Enables writing **general code** that works with different **specific** types.
  
  **Example – Using an Interface:**
  
  ```
  interface IAnimal {
    void Sound();
  }
  
  class Dog : IAnimal {
    public void Sound() => Console.WriteLine("Woof!");
  }
  
  class Cat : IAnimal {
    public void Sound() => Console.WriteLine("Meow!");
  }
  
  List<IAnimal> animals = new() { new Dog(), new Cat() };
  
  foreach (var animal in animals) {
    animal.Sound();   // Works even though the exact type doesn't show in the statement
  }
  ```
  
  ---
- ### 2. Compile-Time Polymorphism (Static)
- Decided at **compile time**.
- Achieved through **method overloading** or **operator overloading**.
  
  **Example – Method Overloading:**
  
  ```
  class MathUtils {
    public int Add(int a, int b) => a + b;
    public double Add(double a, double b) => a + b;
  }
  
  var utils = new MathUtils();
  Console.WriteLine(utils.Add(2, 3));       // 5 (int version)
  Console.WriteLine(utils.Add(2.5, 3.1));   // 5.6 (double version)
  ```
  
  ---
- ### 3. Run-Time Polymorphism (Dynamic)
- Decided at **runtime**.
- Achieved through **method overriding** using `virtual` and `override`.
  
  **Example – Method Overriding:**
  
  ```class Animal {
  class Animal {
      public virtual void Speak() => Console.WriteLine("Some sound");
  }
  
  class Dog : Animal {
    public override void Sound() => Console.WriteLine("Woof!");
  }
  
  class Cat : Animal {
    public override void Sound() => Console.WriteLine("Meow!");
  }
  
  Animal a1 = new Dog();
  Animal a2 = new Cat();
  
  a1.Sound();  // Woof!
  a2.Sound();  // Meow!
  !
  ```
  
  ---
- Achieved at **runtime**.
- Common examples:
	- **Method overriding** → a child class provides a new implementation for a method already defined in its parent class.
	- Typically uses **inheritance** and **virtual functions** (or interfaces).
- ```
  Dog d = new Dog();
  ```
  
  What types could store `d`?
- `Dog`
- `IAnimal`
- `object`
  
  ---
- # Casting
  
  **Casting** means converting one type of object or value into another type.
  
  In C#, there are two main kinds: **implicit** and **explicit**.
  ---
- ### 1. Implicit Casting (safe conversion)
- Happens **automatically**, no extra code needed.
- Allowed when there’s **no risk of data loss**.
  
  ```
  int num = 3;
  double d = num;   // Implicit cast
  ```
  
  Why it works:
- Every integer can be represented as a double (`3` → `3.0`).
- Nothing is lost, so the compiler does the conversion automatically.
  
  ---
- ### 2. Explicit Casting (manual conversion)
- Happens only when you **tell the compiler** to do it, using `(Type)`.
- Needed when there **might be data loss** or the conversion isn’t guaranteed.
  
  ```
  double pi = 3.14;
  int val = (int)pi;   // Explicit cast
  ```
  
  Why explicit?
- A double can hold decimals, but an int cannot.
- The fractional part (`.14`) is **lost**, so the compiler forces you to write `(int)` to show you understand that risk.
  
  ---
- ### 3. Casting Between Classes (specific vs. general types)
  
  In OOP, we also cast between classes in an **inheritance hierarchy**.
- **More specific → less specific** (child → parent):
	- Implicit cast allowed (safe).
	- Example: A `Dog` *is* always an `Animal`.
	  
	  ```
	  Dog d = new Dog();
	  Animal a = d;     // Implicit cast: safe
	  ```
- **Less specific → more specific** (parent → child):
	- Explicit cast required (not always safe).
	- Example: Not every `Animal` is a `Dog`.
	  
	  ```
	  Animal a = new Dog();
	  Dog d2 = (Dog)a;  // Explicit cast: safe here, because 'a' really is a Dog
	  
	  Animal a2 = new Animal();
	  Dog d3 = (Dog)a2; // Runtime error! 'a2' is not actually a Dog
	  ```
	  ---
- Example with Dog and IAnimal**
  
  ```
  Dog d = new() { Name = "Fido" };
  IAnimal a = d;               // OK
  Console.WriteLine(a.Name);   // Error: IAnimal may not have Name
  
  Console.WriteLine(((Dog)a).Name); // Works with explicit cast
  ```
  
  ```
  IAnimal another = new Dog();
  Dog d2 = another;    // Error
                     // Not all IAnimals are Dogs
                     // Explicit cast required
  ```
  
  ---
- ### `as`  and  `is`  Keywords
  
  ```
  IAnimal animal = something;
  Dog dog = animal as Dog;
  ```
- If `animal` is a `Dog`: same as `(Dog)` cast
- If not: returns `null`
  
  ```
  IAnimal another = something;
  if (another is Dog d) {
    Console.WriteLine(d.Name);
  }
  ```
  
  ---