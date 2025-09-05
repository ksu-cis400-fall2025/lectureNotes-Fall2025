## Deadlines & Announceme
- **GitHub repo problems**
	- Send me and email with your GitHub username
- **Encapsulation Tutorial**: due Tuesday
- **Properties Tutorial**: due today Wednesday
- **Milestone 1**: due Friday **September 5th**
- ### Reminders
	- Make sure your project **builds** (but it won’t run yet).
- **Save your files!**
	- How to check what you submitted?
	- “You are ahead of branch main...” → what does this mean?
	  
	  ---
- ## Properties vs. Fields
- ### Example: Field vs. Property
  
  ```
  // Field
  public int Num;
  
  // Property
  public int Num { get; set; }
  ```
- Properties give more control over **visibility** (especially when setting values).
- ### Auto-Property
  
  ```
  public int Num { get; set; }
  ```
  
  is equivalent to:
  
  ```
  private int _num;
  public int Num
  {
    get { return _num; }
    set { _num = value; }
  }
  ```
- ### Visibility and Default Values
  
  ```
  public int Num { get; set; } = 10;
  ```
  
  or initialize in the constructor:
  
  ```
  public WhateverClass()
  {
    Num = 10;
  }
  ```
- ### Lambda Notation
	- What is it?
		- A lambda expression in C# is a quick way to write a small function right where you need it, 
		  without naming it. (Anonymous function)
		  var numbers = new[] {1, 2, 3, 4, 5};
		  var evens = numbers.Where(n => n % 2 == 0);
		  Here, n => n % 2 == 0 is the lambda: “take a number n and check if it’s even.”
		- In contrast:
		  bool IsEven(int n)
		  {
		      return n % 2 == 0;
		  }
	- ```
	  // Lambda used in properties
	  private int _num = 10;
	  public int Num
	  {
	    get => _num;
	    set => _num = value;
	  }
	  ```
	  ---
	  Usage:
	  
	  ```
	  obj.Num = 10;
	  ```
	  ---
	  Other examples **>> Interesting <<**:
	  
	  ```
	  public string Name => "Club Sub";
	  ```
	- `public` → The property is accessible outside the class.
	- `string` → The property’s type is `string`.
	- `Name` → The property’s name.
	- `=> "Club Sub";` → Instead of a backing field, it always returns the string `"Club Sub"`.
	  
	  So effectively, it’s the same as writing:
	- ```public string Name
	  public string Name
	  {
	      get { return "Club Sub"; }
	  }
	  ```
		- Meaning:
		- The `Name` property is **read-only**.
		- It always returns the constant value `"Club Sub"`.
		- You cannot assign to it (no `set` accessor).
		  
		  **>>> It’s a concise way of creating a property with a fixed return value. <<<**
	- ---
- ## Common Mistake with Properties
  
  ```
  public int Property
  {
    get { return Property; }
    set { Property = value; }
  }
  ```
  
  ⚠ This causes **infinite recursion**.
- Fix:
	- private int _property;
	- public int Property
	  {
	    get { return _property; }
	    set { _property = value; }
	  }
- ---
- ## Practice: LabRoom Class
- Turn **fields into properties**. (name, size, windows)
- Enforce **room size 10–30**.
- Make `Windows` value **get-only** (except at creation):
	- Using a constructor
	- Using `init`
	- ```
	  public class LabRoom
	  {
	      // Backing fields
	      private string _name;
	      private int _size;
	  
	      // Properties
	      public string Name
	      {
	          get => _name;
	          set => _name = value;
	      }
	  
	      public int Size
	      {
	          get => _size;
	          set
	          {
	              if (value < 10 || value > 30)
	                  throw new ArgumentOutOfRangeException(nameof(Size), "Size must be between 10 and 30.");
	              _size = value;
	          }
	      }
	          // Get-only property (can only be set at creation)
	      public int Windows { get; init; }  // using init for creation-time assignment
	  
	      // Constructor
	      public LabRoom(string name, int size, int windows)
	      {
	          Name = name;
	          Size = size;
	          Windows = windows;
	      }
	  }
	  // Using constructor to set init-only properties
	          var lab = new LabRoom("Chemistry Lab", 20, 3);
	          
	  // Using object initializer to set the init-only properties
	          var lab = new LabRoom
	          {
	              Name = "Physics Lab",
	              Size = 35,
	              Windows = 4
	          };
	  ```
	- ---
- ## Practice: PointStruct
- Try to use it.
- Discussion:
	- Differences between **class** and **struct**?
		- How **value types (structs)** and **reference types (classes)** differ in C#
		- Memory
			- **Struct**: Stored on the stack (variable holds the data directly)
			- **Class**: Stored on the heap (variable holds a reference)
		- Assignment
			- **Struct**: Copies the *value* (two independent copies)
			- **Class**: Copies the *reference* (two variables refer to the same object)
		- Default Constructor
			- **Struct**: Always has a parameterless default constructor (implicitly sets fields to default values, e.g. `0` for numbers)
			- **Class**: You can define custom constructors
		- Usage
			- **Struct**: Best for small data types that represent a single value or small group (e.g., `Point`, `DateTime`)
			- **Class**: Best for complex objects with identity (e.g., `Person`, `Car`)
	- How to make **PointStruct immutable**?
	- ```
	  public struct PointStruct
	  {  
	      public int X { get; }   // Read-only  
	      public int Y { get; }   // Read-only  
	      
	      public PointStruct(int x, int y)
	      {  
	          X = x;  
	          Y = y;  
	      }  
	  }
	    
	  // Usage
	  var p1 = new PointStruct(2, 3);
	  
	  // p1.X = 5; // Not allowed (read-only)
	  
	  ```
	- Why should structs usually be immutable?
		- **Value semantics** → When you pass a struct around, it’s *copied*.
			- If it were mutable, changes in one copy wouldn’t reflect in another, leading to confusion.
		- **Thread safety** → Immutable structs cannot be changed after creation, so they’re naturally safe to share between threads.
		- **Consistency** → Most built-in structs in .NET (`DateTime`, `Guid`, `Decimal`, etc.) are immutable. Users expect the same behavior in custom structs.
	- ---
- ## Static vs. Non-Static
- When can/should a **field/method/property** be static?
- When is a field/method/property **not allowed** to be static?
- When should a **class** be static?
  
  Other questions:
- Can a static class have a constructor?
- Can a non-static class have a static constructor?
  
  Example:
- What if we wanted a **consistent drinks policy** (yes/no) across all lab rooms?
	- ```
	  class LabRoom
	  {
	      // Static field: shared across all instances
	      public static bool DrinksAllowed;
	  }
	  ```
-
- How could we **initialize** the drinks policy for everyone?
- ``` Option-1
  class LabRoom
  {
      public static bool DrinksAllowed = true; // default is yes
  }
  
  ```
- ```Option-1
  class LabRoom
  {
      public static bool DrinksAllowed;
  
      static LabRoom() // runs once before first use
      {
          DrinksAllowed = true; // set default policy
      }
  }
  
  ```
-
- How could we **modify** the drinks policy for everyone?
- ```
  LabRoom.DrinksAllowed = false; // no drinks in any lab room
  ```
-
- Stop!
- ---!
- **What is encapsulation?**
- ### What is it?
	- Abstracting complexity
	- Putting together fields and the methods that manipulate those fields in single entity - **class**
- ### Benefits:
	- **Protects data integrity** – prevent invalid states.
	- **Hides implementation details** – allows internal changes without breaking clients.
	- **Controls access** – expose only what is necessary, simplify usage, and enforce rules.
	- ![Screenshot 2025-09-05 at 10.48.59 AM.png](../assets/Screenshot_2025-09-05_at_10.48.59 AM_1757087429504_0.png)
-
- ## Key Vocabulary
- Encapsulation
- Information Hiding
- State
  
  ---