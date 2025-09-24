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
- ### Casting
  
  **Implicit vs. Explicit Casting**
  
  ```
  double pi = 3.14;
  int val = (int)pi;   // Explicit cast required
  ```
  
  ```
  int num = 3;
  double d = num;      // Implicit cast (no info lost)
  ```
-
- **Explicit cast**: when there’s potential data loss (e.g., double → int).
- **Implicit cast**: when the conversion is always safe (e.g., int → double).
	-
- **Example with Dog/Animal**
  
  ```
  Dog d = new() { Name = "Fido" };
  IAnimal a = d;               // Implicit upcast: Dog → IAnimal
  Console.WriteLine(a.Name);   // Error: IAnimal may not define Name
  
  Console.WriteLine(((Dog)a).Name); // Explicit downcast back to Dog, Okay
  ```
  
  ```
  IAnimal another = new Dog();
  Dog d2 = another;    // Error
                     // Not all IAnimals are Dogs
                     // Explicit cast required
  ```
  
  ---
- ## Keywords
- ### `as`  and  `is`  
  
  **Using `as`**
  
  ```
  IAnimal animal = something;
  Dog dog = animal as Dog;
  ```
- If `animal` is actually a `Dog`, the cast succeeds (same as `(Dog)animal`).
- If not, `dog` will be `null` instead of throwing an exception.
  
  ---
  
  **Using `is`**
  
  ```
  IAnimal another = something;
  if (another is Dog d)
  {
    Console.WriteLine(d.Name);
  }
  ```
- The `is` keyword checks type compatibility.
- With pattern matching (`is Dog d`), it both checks the type **and** declares a variable `d` of type `Dog`.
- Safer and cleaner than casting first and then checking.
  
  ---
-