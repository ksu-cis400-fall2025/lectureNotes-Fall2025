## Next Week
	- **Two tutorials** (Monday and Tuesday)
	- **Milestone 6** will be smaller —
	  
	  → **Due next Thursday**
	  
	  → We’ll discuss it **in class on Monday and Wednesday**
	  
	  → The goal is to help everyone finish the milestone so you can **enjoy the 3-day weekend**
	  
	  **No class next Friday (October 17)**
	  
	  ---
- ## This Week
  
	- This **Friday:** Milestone 5 due
	  ---
- ## Today
	- ## Layouts
		- **StackPanel**
			- Arranges elements in a single line (vertical or horizontal)
		- **DockPanel**
			- Docks elements to the top, bottom, left, or right; the last added element fills the remaining space
		- **Grid**
			- Organizes elements in rows and columns
		-
		- **→ When should you use each?**
		  
		  ---
	- ## Creating the Menu Control
	  collapsed:: true
		- What kind of **layout** will you use?
		- What kinds of **controls** will you have?
		- Do you need to worry about **spacing** for other components?
		  
		  ---
	- ## Creating the Order Control
	  collapsed:: true
		- What kind of **layout** will you use?
		- What kinds of **controls** will you have?
		- This control should include a **ListView**
		  
		  ```
		  <ListView ItemsSource="{Binding}"/>
		  ```
		-
		- **Question:** What does the `"Binding"` mean?
		  
		  ---
	- ## Creating the Main Window
		- How should you lay out the **menu** and the **order summary**?
		- How can you place the **buttons at the bottom**?
		  
		  **Adding a custom control:**
		  
		  ```
		  <local:YourControlClass/>
		  ```
			-
			- **Remember:**
			- You can specify properties such as `Grid.Row`, `Grid.Column`, etc.
			  
			  ---
	- ## DataContext
		- What is `DataContext`?
			- `DataContext` is an **object that provides the data source for data binding** in WPF.
			  
			  It tells UI elements *where to look* for the properties or data they should display or bind to.
			-
		- How does it work?
			- #### **How does it work?**
			- When you set a `DataContext` on a control, **all its child elements automatically inherit** that same context (unless they have their own `DataContext`).
			- This allows you to bind UI elements to properties of the same object without having to specify the full path every time.
			  
			  **Example:**
			  
			  ```
			  // In code-behind
			  this.DataContext = new Person { Name = "Alice", Age = 25 };
			  ```
			  
			  Then, in XAML:
			  
			  ```
			  <TextBlock Text="{Binding Name}"/>
			  <TextBlock Text="{Binding Age}"/>
			  ```
			  
			  Both `TextBlock` elements automatically use the `Person` object as their data source because it’s set as the window’s `DataContext`.
		- Where do we set it?
			- We’ll use an **ObservableCollection<IMenuItem>**, typically set in the **MainWindow constructor**.
			- You can set the `DataContext` in several places:
			- **In XAML**, using a resource or ViewModel:
			  
			  ```
			  <Window.DataContext>
			    <local:MainViewModel/>
			  </Window.DataContext>
			  ```
			- **In the code-behind** (commonly in the constructor or `Loaded` event):
			  
			  ```
			  DataContext = new MainViewModel();
			  ```
			- **At the control level**, if only a part of the UI needs a different source:
			  
			  ```
			  <StackPanel DataContext="{Binding SelectedItem}">
			    <TextBlock Text="{Binding Name}"/>
			  </StackPanel>
			  ```
			  
			  ---
	- ## Handling Button Clicks
		- Assign **names** to all menu buttons in the XAML.
		- Use a single **event handler** for all button clicks.
		  
		  Example:
		  
		  ```
		  private void ClickEventHandler(object sender, RoutedEventArgs e)
		  {
		    // sender is the button that triggered the event
		    if (sender is Button b)
		    {
		        if (DataContext is ObservableCollection<IMenuItem> order)
		        {
		            if (b.Name == "CustomSandwichCtrl")
		            {
		                order.Add(new CustomSandwich());
		            }
		        }
		    }
		  }
		  ```
		-
		- How can we add items to the collection when a button is clicked?
		- ---
