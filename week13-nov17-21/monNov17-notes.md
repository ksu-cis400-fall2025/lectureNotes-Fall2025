## Announcements
collapsed:: true
	- ### Deadlines and Remind
		- **Today:** Tutorial 1 **Intro to Razor Pages**.
			- Create a new ASP.NET Core project.
			- Review basic HTML and CSS.
			- Explore the use of **PageModels**.
		- **Tuesday:** Tutorial 2:  **More with Razor Pages**
			- Read movie information from a JSON file and display it on a webpage.
			- Practice additional styling and layout techniques.
		- **Friday** November 21: **Milestone 10**.
		  
		  ---
	- ### Exam 2
		- Quickly Review the Solution
		  
		  
		  
		  ---
- ## Begin Razor Pages
  collapsed:: true
	- ### What Are Razor Pages?
		- Razor Pages allow you to inject C# code into HTML to create dynamic web pages.
		- You will need to add a **new ASP.NET Core Web App** project.
			- If prompted, select **“Install more tools and features”** when adding the new project.
			- Then search for the **ASP.NET and web development** bundle.
		- ### Adding the ASP.NET Project
			- When adding your new web project:
			- Right-click the **SubHero solution**
			- Select **Add → New Project**
			- Or, from the **File** menu option
			- ---
	- ### Additional Notes
		- ### Creating a New Project
			- Choose **ASP.NET Core Web App** (not MVC), so the project is cross-platform.
			- ### Checking Your .NET Version
			- Ensure your .NET SDK matches the version used in class.
			- ### Quick Display in Razor Pages
				- Use the **PageModel** to easily pass data to your page for display.
				  
				  ---
- ## Milestone 10
  collapsed:: true
	- ### Goal
		- Create a website for **SubHero** that includes:
		- collapsed:: true
		  
		  **Home Page** — Displays *all* menu options, organized by:
			- Entrees
			- Sides
			- Drinks
			- Combos
			- Also: show *available ingredients* under Entrees.
		- **About Page**
		- **Privacy Page**
	- ### Approach: Pre-Generate Items
	  collapsed:: true
		- Create instances of as many menu items as reasonably possible so they are ready for next week’s search/filter features.
		- #### Entrees
			- Create an instance of *each sandwich/wrap/sub* in *each possible bread/size combination*.
			- Ingredient combinations are **not** required at this stage.
		- #### Sides
			- Create all possible combinations **except** Side Salad (just use its default).
		- #### Drinks
			- Create all possible combinations **except** Ice customization.
		- #### Combos
			- Create all possible combinations using:
				- Each entree in its **default configuration**
				- Each side in its **default configuration**
				- Each drink in its **default configuration**
		- ### Examples
			- #### Fountain Drink
				- Flavors: 5
				- Sizes: 3
				  
				  → **5 × 3 = 15 combinations**
			- #### Combo
				- Entree choices: 7
				- Side choices: 4
				- Drink choices: 3
				  
				  → **7 × 4 × 3 = 84 combinations**
	- ### Display Requirements (for each item)
	  collapsed:: true
		- Name
		- Description (optional for Combos)
		- Preparation Information
		- Price
		- Calories
	- ### Navigation
	  collapsed:: true
		- Users should be able to click to view:
			- Entrees
			- Drinks
			- Sides
			- Combos
	- ### Styling
	  collapsed:: true
		- You may style the site however you prefer.
		- Feel free to look online for CSS inspiration.
	- ### Important Notes About Display
	  collapsed:: true
		- If you do not like the look of displaying all menu combinations:
			- Next week we will add **search and filtering**, which will improve the layout.
			- You may rearrange the look next week, but having all combinations now will make searching easier.
			  
			  ---
- ## Menu Classes
  collapsed:: true
	- `FullMenu`
	- `Entrees`
	- `Sides`
	- `Drinks`
	- `Combos`
	- ### Useful Patterns / Snippets
	  
	  ```
	  (someList).AddRange(someIEnumerable);
	  ```
	  
	  ```
	  Apple a = new() { Sliced = true };
	  _sides.Add(a);
	  ```
- ## Wednesday's Class
  collapsed:: true
	- Discussion of **testing** and **UML** for the milestone.
	  
	  ---