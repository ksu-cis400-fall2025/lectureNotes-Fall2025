# Testing and Nullables
- ## Announcements
- **This Week**
	- Tue September 23: Testing Tutorial due
	- Wed September 24: UML Tutorial due
	- Fri September 26: **Milestone 4 due**
- **Next Week**
	- No tutorials or milestones
	- Monday: Review session
	- Wednesday: **Exam 1**
	- Friday: Work day
	- **All past due assignments must be submitted by Friday, October-03 for any partial credit**
- After Exam 1, we will begin working with **WPF (Windows Presentation Foundation)** to create user interfaces.
  
  ---
- ## Today’s Topics
- Creating a test project
- Writing test cases
- Working with nullables
  
  ---
- ## Example Task
- Implement the **PeopleYears** property in the `Dog` class.
  
  ---
- ## Unit Testing with XUnit
- ### Creating an XUnit Testing Project
- Add a project reference to the class library you want to test.
- ### Basics of Writing a Unit Test
- **Fact tests** – used for default values or fixed outcomes.
	- Example: *What properties in `Dog` have default values?*
	- Question: *Why can’t we see the `Dog` class?* → Fix: add the project reference.
- **Theory tests** – used for testing derived properties and methods with different data inputs.
	- Example: *How do we choose appropriate inline data?*
	  
	  ---
- ## What to Test in General
- Default values
- Property values after construction
- Behavior of methods
- Edge cases
  
  ---
- ## Common Assert Methods
- `Assert.Equal(expected, actual);`
- `Assert.Equal(expected, actual, precision);` *(for decimals)*
- `Assert.True(condition);`
- `Assert.False(condition);`
- `Assert.Contains(expectedItem, collection);`
- `Assert.All(collection, item => condition);`
- `Assert.IsAssignableFrom<T>(item);`
  
  ---
- ## Nullables
- ### Value Type
  
  A **value type** in C# directly contains its data, and a copy of the value is created whenever it’s assigned to a new variable. Examples include primitives (`int`, `double`, `bool`) and structs (`struct`, `enum`).
- ### Reference Type
  
  A **reference type** in C# stores a reference (memory address) to its data rather than the data itself, so multiple variables can point to the same object. Examples include `class`, `string`, `object`, arrays, and delegates.
-
- ### What Are Nullables in C#?
  
  In C#, *nullables* are value types (like `int`, `bool`, `DateTime`) that can also represent the absence of a value (`null`). Normally, value types cannot be null, but by declaring them as nullable (using `?`), you allow them to hold either a valid value or `null`.
  
  Example:
  
  ```
  int? age = null;  // Nullable int
  bool? isActive = true; // Nullable bool
  ```
-
- Nullable reference type:
  
  ```
  Dog? d = (some value);
  d?.Print();  // Print is only called if d is not null
  ```
- **Why use nullables?**
- Allow value types and reference types to represent “no value.”
- Useful for optional data.
  
  ---
- ## UML Review
- Be familiar with how to list **all members** in UML.
- For milestones:
	- Only **public members** are required.
	- Constructors: *default constructors do not need to be listed.*
- ### UML Class Diagram Relationships
	- **Realization (IS_A)**
	- **Generalization (IS_A)**
	- **Aggregation (HAS_A)**
	- **Composition (HAS_A)**
- (Other relationships exist, but focus on these for now.)
- ### What Members to Show
- **Implementing an interface:** show **all** members in each implementing class.
- **Extending a class:**
	- Non-overridden members → listed only in the parent class.
	- Overridden members → list in both the parent and the child class.
	  
	  ---