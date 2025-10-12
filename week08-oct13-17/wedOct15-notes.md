## Announcements
collapsed:: true
	- **Milestone 6:** Due tomorrow **Thursday**
		- Let me know by Thursday 5:00pm if you need an extra day.
	- **Next week’s module:** Available tomorrow **Thursday**
		- Tutorials: Next **Monday** and **Tuesday**
- ## Updating the Order Summary
  collapsed:: true
	- The goal:
		- Update **Subtotal**, **Tax**, and **Total** automatically as items are **added** or **removed**.
	- #### Key Concept:  `INotifyPropertyChanged`
	  
	  The `Order` class implements the `INotifyPropertyChanged` interface:
	  
	  ```
	  public event PropertyChangedEventHandler? PropertyChanged;
	  ```
	  
	  
	  You need to **invoke** the `PropertyChanged` event whenever an action changes the value of a property:
	  
	  ```
	  PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(PropertyName)));
	  ```
	-
	- ### Why It Works
		- User controls are **subscribed** to the `PropertyChanged` event of their `DataContext`.
		- If a control uses **data binding** with the affected property, it will **automatically re-render** when the property changes.
	-
- ## When to Invoke  `PropertyChanged`
  collapsed:: true
	- You must raise `PropertyChanged` for any property whose value changes due to an operation:
	- |**Action** |  **Properties to Update** |
	  |**Add item**|  `Total`, `Subtotal`, `Tax` |
	  |**Remove item** | `Total`, `Subtotal`, `Tax`|
	  |**Clear order** | `Total`, `Subtotal`, `Tax`|
	  |**Change `TaxRate`** |`Tax`, `Total`, `TaxRate` |
	-
- ## Clarification: “Cancel Order” Button
  collapsed:: true
	- The **Cancel Order** button should **call `Clear()`** on the order.
	- The **order number does not change** when an order is cleared.