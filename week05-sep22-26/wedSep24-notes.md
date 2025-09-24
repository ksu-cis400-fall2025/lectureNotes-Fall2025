## UML, and Collections
- ### Reminders
- Testing Tutorial due yesterday
- Wed September 24:
	- UML Tutorial due, and
	- MIlestone 4 - pre release
		- Implement all test cases listed in the section "Specific *Required Test Cases".*
		- All test cases **must** pass.
		- You commit and push your code by Wednesday at 11:59 PM**.**
		- Make a **pre-release** for Milestone 4. Follow the steps for a release using the tag and release name "**v0.4.0rc**" (rc -> release candidate).
		- Post your release in Canvas as first submission to Milestone 4 assignment **before 11:59pm.**
- Fri September 26: **Milestone 4 due**
- ---
- ### Review
	- Nullables
	- ``` 
	  type? name;
	  ```
	- What does it mean? name is a variable with given type, **now** is allowed to be null
	- So, value types can be nullable too:
	- ```
	  int? a = null;
	  ```
	- Why use them?
		- when in an application there are fields or values that may not apply to all scenarios and the dfaul value suc a 0 for int, or false for bool
	-
	- null condition operator
	- ```
	  Dog? d = (some value)
	    d?.Print(); //when is Print called? (assuming we have a Print method...)
	    d?.Print(); //when is Print called? (assuming we have a Print method...)
	    // if d not null, will call Print
	    // if d null, won't do anything
	  ```
	- ---
	-
- ## UML for MIlestone 4
- Relationships:
    Realization (is-a):  implementing an interface
        dashed line with an open arrow pointing at the interface
        Drink/Entree/Side/Combo implement IMenuItem
- Generalization (is-a): extending a class
        solid line with an open arrow pointing at the parent class
        ClubSub extends Entree
- Aggregation (has-a): 
        open diamond with the diamond touching the collection
        Order is a collection of IMenuItem
- Composition (has-a):
        closed diamond with the diamond touching the collection
        Entree is a collection of IMenuItem
- (and others, but this is it for now)
- Where in our code do we have these relationships?
- Enums? put near class that uses, but no lines
-
- ## Collections
- ICollection? Order implements ICollection
- Implementing a collection.
- Example: AnimalCollection
  Adds a legs count property
- ### Steps
	- Declare the `AnimalCollection` class implementing `ICollection<IAnimal>`.
		- **Why a List<T>**
		  collapsed:: true
			- **Dynamic sizing**: Automatically resizes as items are added
			- **Indexed access**: O(1) random access by index.
			- **Efficient iteration**: Optimized for `foreach` and LINQ.
			- **Backed by an array**: Compact memory and cache-friendly.
			- **Well-tested**: Built into the .NET runtime, highly optimized.
		- ### When you might  **not**  want a  `List<T>` :
		  collapsed:: true
			- **Fast lookups required** → use `HashSet<T>` or `Dictionary<TKey,TValue>`.
			- **FIFO behavior** → use `Queue<T>`.
			- **LIFO behavior** → use `Stack<T>`.
			- **Sorted data** → use `SortedList<TKey,TValue>` or `SortedDictionary<TKey,TValue>`.
	- Add a private field _animals of type List<IAnimal>
	- Add the `LegCount` property to sum all legs.
	- Implement the `Count` property.
	- Implement the `IsReadOnly` property.
	- Implement the `Add` method.
	- Implement the `Clear` method.
	- Implement the `Contains` method.
	- Implement the `CopyTo` method.
	- Implement the `Remove` method.
	- Implement the `GetEnumerator` methods.