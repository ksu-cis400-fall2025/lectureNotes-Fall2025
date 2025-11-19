##  Announcements
collapsed:: true
	- **Friday** November 21: **Milestone 10**.
	- #### Recommended Order of Approach
		- Add the **About** page and edit the **Privacy** page.
		- Write the **static `Menu` class** (`SubHero.Data`).
		- Write the **Index** page to make the menu information *appear*.
		- Conduct **Testing**.
		- Update your **UML** diagram.
		- Complete **Styling**.
		  
		  ---
- ## Testing the Static  `Menu`  Class
  collapsed:: true
	- ### For Each Type of Menu Item:
		- (Entrees, Sides, Drinks, Combos)
		- **Test that the count matches your expectations.**
			- It’s recommended to keep the expected value as an *expression*:
			  
			  ```
			  5*3 + 2*3 + 2*3
			  ```
		- **Test that the collection contains all expected menu items.**
		  
		  ---
	- ### Using  `Assert.Contains`
	  
	  Use a boolean expression to verify that an expected item is present.
	- ``Assert.Contains(collection, item => (some bool expression about item));``
	-
	- **Example:** Check whether the `Drinks` collection contains a *small, unsweetened iced tea*.
	  
	  ```
	  Assert.Contains(Menu.Drinks, 
	    item => item is IcedTea tea 
	            && !tea.Sweet 
	            && tea.Size == SizeType.Small);
	  ```
		- ### Would this work?
			- This will *not* work unless you override `==` or `Equals`:
			-
			- ```
			  Assert.Contains(Menu.Drinks, 
			    item => item == new IcedTea(){ ... });
			  ```
			  
			  ---
	- ### IngredientItem
		- You are **not required** to test the `IngredientItem` collection.
		  
		  ---
	- ### Looping Through Enumerations
		- Example using `SizeType`:
			- ```
			  foreach (SizeType size in Enum.GetValues<SizeType>())
			  {
			    ...
			  }
			  ```
			  
			  ---
- ## Testing Combos
  collapsed:: true
	- Create a `List` of entrees, a `List` of sides, and a `List` of drinks.
	- Use `Assert.Contains` to check that each valid combination exists.
	  
	  Example pattern:
	  
	  ```
	  Assert.Contains(Menu.Combos,
	    item =>
	        item is Combo c
	        && c.SandwichChoice.GetType() == e.GetType()
	        && ...
	  );
	  ```
	  
	  You **don’t** need to check anything more specific.
	  
	  **Alternative:** Override `Equals` for Entree/Side/Drink and assert using equality.
	  ---
- ## UML Updates
  collapsed:: true
	- ### Static  `Menu`  Class
		- Add the static `Menu` class (in `SubHero.Data`).
		- Show static classes using **underlining** in UML.
		- Relationships:
			- Aggregation of `IMenuItem`
			- Aggregation of `IngredientItem`
	- ### Pages
		- Add each Razor Page:
			- **Index**, **Privacy**, **About**, **Error**
			- Note the new namespace.
			- In each `PageModel` (code-behind):
				- Identify properties/members.
				- Document inheritance.
		- #### Relationship Notes
			- There is a **directed association** from the **Index** page *toward* `Menu`.
		- #### Not Needed in UML
			- `Program.cs`
			- `_Layout.cshtml`
			- `_ViewImports.cshtml`
			  
			  ---
- ## Styling the Menu Items
  collapsed:: true
	- ### Suggested Structure
		- Wrap each section (Entrees, Sides, Drinks, Combos) in a `<div>`.
		- Wrap each **menu item** in its own `<div>`.
	- ### CSS Suggestions
		- **For Entrees/Sides/Drinks/Combos sections:**
		  
		  ```
		  display: flex;
		  flex-wrap: wrap;
		  ```
		  
		  
		  **For each menu item (gives the item consistent width):**
		  
		  ```
		  flex-basis: 200px;
		  ```
		  ---