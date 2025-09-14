# Lecture Notes: Memory, Enums, and Milestone 2

**Reminders:**
- Methods Tutorial → ** due Monday**
- Milestone 2 → **due Friday**
- ### Today
	- ~~Memory~~
	- ~~Enums~~
	- Milestone 2
	- Documentation
- ---
-
- ## 1. Memory in C#
- ### What goes in different sections of memory?
- ### Von Neumann-style computer
- ![Von Neuman.png](../assets/Von_Neuman_1757338827068_0.png)
- **Static Memory**
	- Stores anything marked `static`.
	- **Size:** Fixed; does not change once allocated.
- **Stack Memory**
	- Stores scoped data (e.g., method params and vars, inside loops, inside conditionals).
	- **Size:** Grows when entering a new scope (like a method call) and shrinks when leaving a scope.
	- Limited, but stack overflow is uncommon in most programs.
- **Heap Memory**
	- Stores dynamic memory (anytime you use `new` to create objects or arrays).
	- **Size:** Expands when allocating new objects.
	- Shrinks when objects are no longer referenced by stack or heap (garbage collection).
	  
	  **Question:** What about memory leaks?
	- In C#, garbage collection usually prevents memory leaks.
	- But leaks can still occur if references are kept unnecessarily.
	- ```
	  class Car {
	     public int passangers;
	     
	     public void printNumPassangers() {
	        Console.WriteLine(Person.numberOfPeople);
	     }
	  }
	  
	  class Person {
	     static int numberOfPeople = 0;
	     
	     private string Name{get; set;}
	     
	     
	     public Person() {
	        numberOfPeople++;
	     }
	     
	     public void PrintNumOfPeople() {
	        Console.WriteLine(numberOfPeople);
	     }
	  }
	  ```
	- ---
- ## 2. Enums in C#
- ### Definition
  
  ```
  public enum SomeName
  {
    Value1,
    Value2,
    Value3
  }
  ```
- Enums are essentially integers (`0, 1, 2, …`).
- You can cast an enum to its underlying integer.
- Enums can be defined in a standalone file or nested inside a class.
  
  ---
- ### Example: Days of the Week
  
  ```
  public enum DaysOfWeek
  {
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
  }
  ```
- #### Declaring and Using an Enum
  
  ```
  DaysOfWeek today = DaysOfWeek.Monday;
  Console.WriteLine($"Today is {today}");
  
  // Prints the integer value: "2" (since Wednesday is the 3rd element, starting from 0)
  today = DaysOfWeek.Wednesday;
  Console.WriteLine((int)today); 
  ```
  
  Output:
  
  ```
  Today is Monday
  2
  ```
- #### Custom Display (e.g., “Wed” instead of “Wednesday”)
- By default, enums print their name.
- To customize, use conditionals or a mapping (e.g., dictionary or `switch`).
- #### Looping Through All Enum Values
  
  ```
  foreach (DaysOfWeek day in Enum.GetValues<DaysOfWeek>())
  {
    Console.WriteLine(day);
  }
  ```
  
  ---
- ### Enums and Project Structure
- Enums can be placed in their own **namespace** and file.
- In Visual Studio:
	- Create a **new enum file**.
	- Organize files into **folders**.
	- Moving a file into a folder may also change its namespace.
	  
	  ---
- ## 3. Milestone 2 Requirements
- ### Add New Enums
  
  Create enums for:
- Size of a menu item
- Type of bread
- Flavor of chips (new menu item)
- Flavor of soda (new menu item)
- Flavor of cookie (new menu item)
  
  **Why enums instead of strings?**
- They enforce valid values.
- Easier to use in switch/loop logic.
- Safer than strings (avoids typos).
  
  ---
- ### New Classes
- `Chips`
- `FountainDrink`
- `Cookies` (with bounds: **2–6 cookies**)
	- Correction: The class name should be **Cookies**.
	  
	  ---
- ### Sub/Wrap/Sandwich Size and Bread Rules
- Default size = **Medium**
- Default bread = Given in writeup
  
  **Restrictions:**
- Hoagies → Any size allowed
- Wraps → Only Medium
- Wheat/Sourdough → Only Small or Medium
  
  **Rules:**
- Do NOT allow size/bread changes that violate restrictions.
- You can first change bread or size to something else, then adjust.
  
  Example:
- Mediterranean wrap → default bread: wrap, default size: medium.
  
  ---
- ### Calories and Pricing
- **Base calories**: For a medium with default bread.
	- Adjust for non-default ingredients or bread.
	- Scale by size:
		- Small = ×0.5
		- Large = ×1.5
- **Base price**: For a medium with default ingredients.
	- Adjust for extras (cheese, bread changes, etc.).
	- Scale by size:
		- Small = $3 less
		- Large = $2 more
		  
		  **Example:** Small Turkey Cranberry Sandwich on a hoagie (default: medium on wheat)
- With provolone, no red onion.
  
  Calories:
- Base = 605
- +40 for hoagie instead of wheat
- +80 for provolone
- –5 for no onion
- = 720 (medium) → scaled small = 360
  
  Price:
- Base = $8.49
- +$1 for cheese
- –$3 for small
- = $6.49
  
  ---
- ### Documentation Guidelines
- Add **XML documentation** (`///`) above:
	- Classes
	- Properties
	- Methods (include `param` and `return` tags).
	  
	  Example:
	  
	  ``/// <summary>
	  /// Determines whether this ClubSub contains lettuce.
	  /// </summary>
	  public bool ContainsLettuce() { ... }
	  
	  }
	  ```
	  
	  ---
- ### Code Organization
- Reorganize code into folders.
- Be careful when moving files: namespaces may need updating.
  
  ---