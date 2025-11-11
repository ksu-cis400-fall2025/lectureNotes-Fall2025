## Announcements
	- ### Due Dates
		- **UML in WPF Tutorial**:  Monday
		- **Milestone 9**:  Friday
		  
		  ---
- ## Upcoming Exam
  collapsed:: true
	- **Exam 2:** Wednesday, November 12
		- Review materials will be posted with next week’s module.
	- **Monday, Nov 10** will be a **review day**.
		- No tutorials or milestones are due next week.
		- **All tutorials and milestones since Exam 1** must be submitted by **Friday, Nov 14** for any partial credit.
	- After the exam, we’ll begin working with **Razor Pages**.
	  
	  ---
- ## Milestone 9 Overview
  collapsed:: true
	- ### Requirements
		- Update your **UML diagrams** to reflect the current state of your application.
		- Add or update **unit tests** for changes from Milestones 6–8.
		- Perform **integration testing** as described below.
		  
		  ---
- ## UML Guidelines and Considerations
  collapsed:: true
	- ### Namespaces
		- Show namespace designations (e.g., `SubHero.PointOfSale`) around corresponding classes.
		- Fully qualify any class names (`namespace.ClassName`) when referring to a class from a different namespace.
	- ### Inheritance
		- Indicate that `MainWindow` extends `Window`.
		- Indicate that **every user control** extends `UserControl`.
	- ### Content and Structure
		- Include all:
			- Named controls
			- Public properties, methods, and events
			- Event handlers (even if private)
		- Show the **DataContext** of every control (unless inherited from a parent):
			- `MainWindow`: `Order`
			- `PaymentView`: `PaymentViewModel` *(move to Data library)*
			- Customization controls: corresponding menu item
		- Indicate **composition** (when one control contains another):
			- `MainWindow` contains the order summary, menu, all customization controls, and payment control.
			- Each customization control contains its corresponding helper control.
	- ### UML Layout Recommendation
		- Organize your UML diagram into clear sections:
			- **Window/UserControl inheritance**
			- **DataContexts**
			- **Control composition**
	- ### Custom Event Args
		- Extend `RoutedEventArgs`.
		- Include a property of type `IMenuItem`.
		- Use **directed association** to indicate class usage.
			- For example: `(MenuSelectionControl) → CustomEventArgs`.
	- ### PaymentViewModel
		- Serves as the **DataContext** for the payment control.
	- ### UML Updates in the Data Project
		- Include the following in your UML:
		- **Order**
			- Implements `INotifyCollectionChanged` and `INotifyPropertyChanged`.
			- Include `PropertyChanged` and `CollectionChanged` events.
			- Add new properties: `PlacedAt`, `Number`.
			- Include any new public members.
		- **IMenuItem**
			- Implements `INotifyPropertyChanged`.
		- **Combo, Entree, Side, Drink**
			- Each implements `PropertyChanged`.
			- Show relationships:
				- `Combo` → EntreeTypes, SideTypes, DrinkTypes
				- `Entree` → new size/bread choice properties (Milestone 7)
		- **PaymentViewModel**
			- Implements `INotifyPropertyChanged`.
		- **IngredientItem**
			- Implements `INotifyPropertyChanged`.
			  
			  ---
- ## Unit Testing
  collapsed:: true
	- ### Order Class
		- Test that `Order` implements both `INotifyPropertyChanged` and `INotifyCollectionChanged` using `Assert.IsAssignableFrom`.
		- Verify that `Number` updates correctly for subsequent orders.
		- Confirm that `Number` and `PlacedAt` remain constant once assigned.
		- Test that `PropertyChanged` is triggered appropriately:
			- Adding/removing/clearing items → `Subtotal`, `Tax`, `Total`
			- Changing `TaxRate` → `Tax`, `Total`, `TaxRate`
	- ### Menu Items
		- Test that every menu item implements `INotifyPropertyChanged`.
		- For each menu item:
			- Identify all properties that can change.
			- Test all combinations of `(changedProperty, affectedProperty)` to ensure `PropertyChanged` fires.
			  
			  Example:
				- **Chips**
					- Changing `Flavor` should trigger `PropertyChanged` for:
						- `Calories`
						- `PreparationInformation`
						- `Flavor`
	- ### Entrees
		- Test changing ingredient inclusion/exclusion and verify that `PropertyChanged` triggers for:
			- `Calories`
			- `PreparationInformation`
			- `Price`
		- ### Combo
			- Test changing entree, side, or drink choice and verify that `PropertyChanged` triggers for:
				- `EntreeChoice` / `SideChoice` / `DrinkChoice`
				- `EntreeTypes` / `SideTypes` / `DrinkTypes`
				- `Calories`, `Price`, and `PreparationInformation`
				  
				  (You may use specific entrees, sides, or drinks for testing; no need to test every customization combination.)
- ## Integration Testing
  collapsed:: true
	- Complete the integration tests for `PaymentViewModel` as outlined in the milestone description.
	- ### Example: FountainDrink Tests
		- Implements:`INotifyPropertyChanged`
		- **Changeable Properties:**
			- `Ice`, `Size`, `Flavor`
			  
			  **Affected Properties:**
			  | | Changed Property | | Affected Properties | |
			  | ---- |
			  | | Ice | | `PreparationInformation`, `Ice` | |
			  | | Size | | `Price`, `Calories`, `PreparationInformation`, `Size` | |
			  | | Flavor | | `PreparationInformation`, `Calories`, `Flavor` | |
			  
			  **Example Test:**
			  
			  ```
			  [Theory]
			  [InlineData(SodaType.Coke, "PreparationInformation")]
			  [InlineData(SodaType.CokeZero, "Calories")]
			  [InlineData(SodaType.OrangeFanta, "Flavor")]
			  [InlineData(SodaType.CokeZero, "PreparationInformation")]
			  [InlineData(SodaType.MountainDew, "Calories")]
			  [InlineData(SodaType.DrPepper, "Flavor")]
			  [InlineData(SodaType.OrangeFanta, "Calories")]
			  [InlineData(SodaType.MountainDew, "Flavor")]
			  public void CheckFlavorChangeProperties(SodaType flavor, string affectedProperty)
			  {
			    FountainDrink drink = new();
			    Assert.PropertyChanged(drink, affectedProperty, () => {
			        drink.Flavor = flavor;
			    });
			  }
			  ```
			  
			  Repeat similar tests for **Size** and **Ice**.
			  
			  ---