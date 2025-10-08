## Next Week
- **Two tutorials** (Monday and Tuesday)
- **Milestone 6** will be smaller — no UML or testing
  
  → **Due next Thursday**
  
  → We’ll walk through most of it **in class on Monday and Wednesday**
  
  → The goal is to help everyone finish the milestone so you can **enjoy the 3-day weekend**
  
  **No class next Friday (October 17)**
  
  ---
- ## This Week
  
  **Friday:** Milestone 5 due
  ---
- ## Types of Layouts
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
- What kind of **layout** will you use?
- What kinds of **controls** will you have?
- Do you need to worry about **spacing** for other components?
  
  ---
- ## Creating the Order Control
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
- How does it work?
- Where do we set it?
  
  We’ll use an **ObservableCollection<IMenuItem>**, typically set in the **MainWindow constructor**.
  
  ---
- ## Handling Button Clicks
  
  How can we add items to the collection when a button is clicked?
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
  
  ---