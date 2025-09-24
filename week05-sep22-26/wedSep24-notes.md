## UML, and Collections
- ### Reminders
- **Interfaces Tutorial**: due Thursday September 18th
- **Inheritance Tutorial**: due Friday September 19th
- **Milestone 3**: due Friday
	- Make sure your solution **builds**
	- Make sure you submit the right commit + release
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
	- Add a private
	- Add the `LegCount` property to sum all legs.
	- Implement the `Count` property.
	- Implement the `IsReadOnly` property.
	- Implement the `Add` method.
	- Implement the `Clear` method.
	- Implement the `Contains` method.
	- Implement the `CopyTo` method.
	- Implement the `Remove` method.
	- Implement the `GetEnumerator` methods.