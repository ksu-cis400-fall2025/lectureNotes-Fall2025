## Announcements
collapsed:: true
	- ### Due Dates:
	- **Monday:** Swapping Controls and Custom Events Tutorial.
	- **Tuesday:** Custom Controls and Resources Tutorial.
	- **Friday:** Milestone 7.
	  
	  → A quick overview video of Milestone 7’s behavior is available in Canvas.
	  
	  ---
- ## Swapping Controls and Custom Events
  collapsed:: true
	- One of the tricky parts in this milestone is **swapping controls**.
	- You will have several controls pre-loaded into the area where the menu appears.
	- Different actions will update their **Visibility**—only one should be visible at a time.
	- When a user clicks a menu button (in the **Menu Selection Control**), it should display the **Customization Control** for that item (in the **Main Window**).
	- Essentially, this means you need to **send a message from the menu (where the action happens)** to the **MainWindow (where all the controls are stored).**
	  
	  ---
- ## Steps: Sending a Message Between Controls
	- ### Step 1: Define What Needs to Be Sent
		- Decide what information, if any, needs to be passed.
		- If information is needed:
			- Create a **custom event args class** that extends `RoutedEventArgs`.
			- Include the necessary info as a property.
	- ### Step 2: Declare the Event
		- In the class where the action occurs:
		- ```
		  public event EventHandler<CustomArgType>? EventName;
		  ```
		   
		  If no data is needed, use `RoutedEventArgs` as the type.
	- ### Step 3: Raise (Invoke) the Event
		- Whenever the action occurs:
		- ```
		  EventName?.Invoke(this, new CustomArgType(params));
		  ```
	- ### Step 4: Handle the Event
		- In the class where the result should occur:
		- ```
		  private void HandleCustomEvent(object? sender, CustomArgType e)
		  {
		    // respond to the event
		  }
		  ```
	- ### Step 5: Attach the Handler
		- In that same class, attach your event handler:
		- ```
		  ControlName.EventName += HandleCustomEvent;
		  ```
		  ---
- ## Example: Sending Data Between Controls
  collapsed:: true
	- `MainWindow` has a `TextBlock` named **ColorText** and a user-defined **ColorControl**.
	- `ColorControl` includes two buttons: **RedButton** and **BlueButton**.
		- Both have a Click handler called `ClickColor`.
		  
		  **Goal:** When the red button is clicked, display “Red” in the `TextBlock` in `MainWindow` (and similarly for blue).
		  
		  ---
- ## Milestone 7 Example: Menu → MainWindow Communication
  collapsed:: true
	- We need to send information about which menu item was selected so that the **MainWindow** can display the correct customization control.
	- ### **Custom Event Steps in Milestone 7**
	- **Create a Custom Event Args Class**
		- Extend `RoutedEventArgs`.
		- Include the info about the selected item (e.g., an `IMenuItem`).
	- **Declare the Event**
		- In the **Menu Selection Control**:
		  
		  ```
		  public event EventHandler<CustomEventArgs>? CustomEvent;
		  ```
	- **Invoke the Event**
		- In the Click event handler for each menu item:
		  
		  ```
		  if (buttonPressed == ChipsButton)
		  {
		   var chips = new Chips();
		   order.Add(chips);
		   CustomEvent?.Invoke(this, new CustomEventArgs(chips));
		  }
		  ```
		  
		  *(The same `Chips` instance should be used both in the order and the event.)*
	- **Handle the Event**
		- In **MainWindow**:
		  
		  ```
		  private void OnCustomize(object? sender, CustomEventArgs e)
		  {
		   // Display the corresponding customization control
		   // Retrieve the IMenuItem from e
		   // Use selection logic to make the correct control visible
		   // Set that control’s DataContext to the IMenuItem
		   // Hide all other controls (including the menu)
		  }
		  ```
	- **Attach the Handler**
		- In **MainWindow’s constructor**:
		  
		  ```
		  MenuSelectionControl.CustomEvent += OnCustomize;
		  ```
		  *(You’ll need to give the menu selection control a name in the XAML.)*
		  ---
- ## Recommended Order of Approach
  collapsed:: true
	- ### **In the Data Project**
	- Load enums as custom resources (sizes, soda flavors, chip flavors, breads).
	- Make sure `IMenuItem` implements **INotifyPropertyChanged**.
	- Declare the `PropertyChanged` event in all parent classes (`Entree`, `Drink`, `Side`, `Combo`).
	- Add a **protected helper method** in all abstract classes:
	  
	  ```
	  protected void OnPropertyChanged(string propertyName)
	  {
	    PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
	  }
	  ```
	- In each menu item class, call `OnPropertyChanged(nameof(Property))` whenever an action changes that property’s value.
	- ### **Examples**
	  
	  **Cookies**
	- Changing `CookieCount` should trigger updates to `CookieCount`, `Price`, `Calories`, and `PreparationInformation`.
	  
	  ```
	  _cookieCount = value;
	  OnPropertyChanged(nameof(Price));
	  OnPropertyChanged(nameof(Calories));
	  OnPropertyChanged(nameof(PreparationInformation));
	  ```
	- Changing `Flavor` should also update `Flavor`, `Calories`, and `PreparationInformation`.
	  
	  **Apple**
	- Property: `Sliced`
	  
	  ```
	  private bool sliced;
	  public bool Sliced
	  {
	    get => sliced;
	    set
	    {
	        sliced = value;
	        OnPropertyChanged(nameof(Sliced));
	        OnPropertyChanged(nameof(Price));
	        OnPropertyChanged(nameof(PreparationInformation));
	    }
	  }
	  ```
	  
	  ---
- ## In the PointOfSale Project
  collapsed:: true
	- Create a **helper control** with Name, Description, and Calories.
	- Pick a simple menu item to start with (e.g., **Apple**).
	- Design a **user control** for that item:
		- Include the helper control.
		- Add UI elements for customizable options.
	- Preload the new control in `MainWindow` (initially hidden).
	- Implement the custom event handling so that selecting a menu item triggers the correct customization control.
	- Display the appropriate control and set its `DataContext` to the corresponding item.
	- **Tip:**
	- Get this working for one control first. Then, handle property changes for the order when item properties change (see Data Binding tutorials).
	- Only **one Entree Control** is needed — do that part last.
	  
	  ---
- ## Wednesday Discussion Topics
  collapsed:: true
	- Entree Control:
		- Limiting size and bread choices in combo boxes.
	- Updating subtotal, tax, and total dynamically when items are customized.
	  
	  ---