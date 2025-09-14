## 3. Milestone 2 Requirements
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