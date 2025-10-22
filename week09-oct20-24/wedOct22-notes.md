## Announcements
collapsed:: true
	- ### Milestone 7 – Due Friday
	  
	  See **Monday’s notes** for a suggested order of approach.
	  ---
- ## Updating the Order When Items Are Customized
  collapsed:: true
	- ### Problem
	- How can the **Order** properties (Subtotal, Tax, Total) automatically update when an item is customized?
	- ### Step 1: Attach a PropertyChanged Handler
	  
	  In Add, attach to item's PropertyChanged:
	  
	  ```
	  item.PropertyChanged += HandleOrderChanges;
	  ```
	- ### Step 2: Implement the Event Handler
	  
	  Then, write the `HandleOrderChanges` method:
	  
	  ```
	  private void HandleOrderChanges(object sender, PropertyChangedEventArgs e)
	  {
	    if (e.PropertyName == "Price")
	    {
	        // Order should raise PropertyChanged for:
	        // Subtotal, Tax, and Total
	    }
	  }
	  ```
	- ### Step 3: Detach the Handler When Items Are Removed
	  
	  When items are removed or cleared from the order, remove the event handler:
	  
	  ```
	  item.PropertyChanged -= HandleOrderChanges;
	  ```
	  
	  ---
- ## Entree – Custom Bread and Size Options
	- ### Goal
		- Allow each entrée to define which **breads** and **sizes** are available.
	- ### Step 1: Define Dictionaries
	  
	  Add two private fields in your `Entree` class:
	  
	  ```
	  private Dictionary<BreadType, List<SizeType>> _sizesByBreadChoice = new();
	  private Dictionary<SizeType, List<BreadType>> _breadsBySizeChoice = new();
	  ```
	- ### Step 2: Populate in the Constructor
	  
	  Example: add entries for sourdough bread.
	  
	  ```
	  _sizesByBreadChoice.Add(BreadType.Sourdough, new List<SizeType>
	  {
	    SizeType.Small,
	    SizeType.Medium
	  });
	  ```
	  
	  Repeat for other bread types and for all sizes.
	  
	  ---
	- ### Step 3: Define Properties
	  
	  ```
	  public IEnumerable<BreadType> BreadOptions => _breadsBySizeChoice[CurrentSize];
	  public IEnumerable<SizeType> SizeOptions => _sizesByBreadChoice[CurrentBread];
	  ```
	  
	  (You should implement these using the dictionaries above.)
	  
	  ---
- ## Using These Options in the Point of Sale
	- ### In the Entree Customization Control
	- Add **ComboBoxes** for bread and size selections.
	- Set:
		- `ItemsSource` → `BreadOptions` (or `SizeOptions`)
		- `SelectedItem` → the current property (`CurrentBread` or `CurrentSize`)
	- ### Updating Current Choices
	  
	  When either the **bread** or **size** changes:
	- Raise a `PropertyChanged` event to indicate that the corresponding options have been updated.
		- If `Size` changes → `BreadOptions` have changed.
		- If `Bread` changes → `SizeOptions` have changed.
		  
		  ---