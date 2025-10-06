# Exam 1 Discussion

**Across both sections:**
- Average: 84.5/100
- High: 100/100
  
  **Grades:**
- A (90–100): 23 students
- B (80–89): 13 students
- C (70–79): 5 students
- Below C: 6 students
  
  **Discussion:**
	- We will go over some of the problems from the exam to clarify common mistakes and important concepts.
- ---
- # Reminders
- **Tuesday – WPF Tutorial**
	- Build a GUI
	- Work with various controls
- **Wednesday – Resources and Styles Tutorial**
	- Add customization to all controls of a specific type
	- Similar concept to CSS styling
- **Milestone 5**
	- Build the shell of the "Point of Sale" GUI for Sub Hero
	- Clicking menu items should add them to the order display
	  
	  ---
- # WPF Applications Overview
  
  **Structure:**
	- **MainWindow**: Launches when the program starts
	- **UserControls**: Can be placed on the MainWindow or inside another UserControl
-
- **Layouts:** Controls are organized using layout containers.
	- Most common layout containers:
		- **Grid** – flexible arrangement of rows and columns
		- **StackPanel** – vertical or horizontal stacking
		- **DockPanel** – dock controls to top, bottom, left, right, or fill
	- Question: When would you choose each layout?
- **Common Controls:**
	- Button
	- TextBlock (display text)
	- TextBox (user input)
	- ListView (display collections)
	- Later: CheckBox, RadioButton, etc.
-
- **Customization:**
	- Control appearance can be modified using Styles and Templates
-
- **Resources for Learning:**
  
  [WPF: How to create and apply a style](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/controls/how-to-create-apply-style?view=netdesktop-8.0)
  
  ---
- # Starting Milestone 5
  
  **Project Setup:**
	- How to add a new project?
	- How to change the startup project?
- **Sample GUI Review:**
	- Examine the sample GUI
	- Predict what it will do when it runs
- Note missing functionality for now:
	- Correct display of order subtotal, total, and tax
	- Editing menu items
	- Showing additional information about items
	- Back to Menu / Cancel Order / Complete Order buttons
	  
	  ---
- # Building the Menu Control
  
  **Considerations:**
	- What layout should you use?
	- What controls are needed?
	- How will this affect spacing of other components?
- ---
- # Building the Order Control
  
  **Considerations:**
	- What layout should you use?
	- What controls are needed?
- ---
- # MainWindow Layout
  
  **Tasks:**
	- How to position the menu and order summary
	- How to place buttons at the bottom
	  
	  **Adding a Custom Control:**
	  
	  ```
	  <local:YourControlClass/>
	  ```
-
	- Can specify layout properties such as `Grid.Row`, etc.
	  
	  ---
- # Understanding DataContext
  
  **Concept:**
	- DataContext provides the source for data binding
	- Example: `ObservableCollection<IMenuItem>`
	- **Order Control:**
	- Should contain a `ListView`
	- Questions to consider:
		- What should the DataContext be?
		- Where should it be set?
		  
		  ```
		  <ListView ItemsSource="{Binding}"/>
		  ```
-
	- What does `{Binding}` mean?
- ---