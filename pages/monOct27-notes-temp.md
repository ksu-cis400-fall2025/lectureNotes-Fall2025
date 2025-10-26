### **Due Dates**
- **Programmatic Controls Tutorial:** Monday
- **MVVM Tutorial:** Tuesday
- **Milestone 8:** Friday
  
  ---
- ## **Milestone 8 Overview**
  
  **See the Milestone 8 demo before starting.**
- ### **Summary of Requirements**
- Add ingredient customization for side salads and entrees
- Add “Make it a Combo” functionality
- Implement “Complete Order”
  
  ---
- ## **Ingredient Customization**
- ### **General Structure**
- Continue using **one Entree control** for all sandwiches.
- Store ingredients as either:
	- `List<IngredientItem>`
	- `Dictionary<Ingredient, IngredientItem>` — this contains only the ingredients allowed for that entree.
	  
	  If you use a dictionary, expose a list of ingredient items through a property in your `Entree` class:
	  
	  ```
	  public List<IngredientItem> AllIngredients => ingredientDictionary.Values.ToList();
	  ```
	  
	  (You can use a similar approach in your `SideSalad` control.)
	  
	  ---
- ### **Displaying Ingredients**
  
  For entrees and salads, display **all possible ingredients**, each with:
- A checkbox
- The ingredient name
- #### **Two Implementation Options**
- **Programmatic Approach**
	- Use the same strategy as in the *Programmatic Controls* tutorial.
	- Dynamically add checkboxes in the Entree control’s code-behind.
	- Call this setup method whenever you display the control.
	- Remember to **clear the checkboxes** before displaying the control again.
- **XAML + Data Binding Approach**
	- In the Entree control’s XAML, create a `ListView` bound to your list of `IngredientItems`:
	  
	  ```
	  <ListView ItemsSource="{Binding IngredientItemListName}">
	  ```
	- Use a **custom data template** (like in the Order Summary) to show:
		- A `CheckBox` (bound to `Included`)
		- A `TextBlock` (bound to `Name`)
		  
		  **Notes:**
	- The `DataContext` for each list item is an `IngredientItem`.
	- Bindings:
		- `CheckBox.IsChecked` → `Included`
		- `TextBlock.Text` → `Name`
		  
		  (Apply a similar setup for the Side Salad control.)
		  
		  ---
- ## **Handling PropertyChanged**
- ### **IngredientItem**
- Implements `INotifyPropertyChanged`.
- Invoke `PropertyChanged` inside the `Included` property’s setter when its value changes.
- ### **Entree**
  
  To ensure Entree updates when an ingredient changes:
- Subscribe to each ingredient’s `PropertyChanged` event:
  
  ```
  ingredientItem.PropertyChanged += HandleIngredientChange;
  ```
- In `HandleIngredientChange`, invoke `PropertyChanged` for:
	- `PreparationInformation`
	- `Calories`
	- `Price`
	  
	  This mirrors what we did for the `Order` class when items were added:
	  
	  ```
	  item.PropertyChanged += HandleOrderChanges;
	  ```
	  
	  ---
- ## **“Make It a Combo” Functionality**
- ### **Button Behavior**
- Add a **“Make It a Combo”** button to the Entree control.
- When clicked:
	- Remove the entree from the `Order`
	- Add a new `Combo`, using that entree as the `SandwichChoice`
	- Hide the Entree customization screen
	- Display the Combo customization screen
	  
	  You’ll need to send a message from the **Combo control** to **MainWindow** — use a **custom event** (similar to the one used in the Menu control).
	  
	  > 
	  
	  *(Later, you can make the “Make It a Combo” button invisible if the entree is already part of a combo.)*
	  
	  ---
- ## **Combo Customization**
- ### **PropertyChanged**
  
  Make sure the Combo properly handles `PropertyChanged` events.
- ### **Display Requirements**
- **Selected Entree:** Show name, option to edit or pick a new one
- **Selected Side:** Option to edit or pick new
- **Selected Drink:** Option to edit or pick new
  
  ---
- ### **Handling Entree Selection**
  
  In `Combo`, create a property:
  
  ```
  public List<Entree> EntreeTypes { get; }
  ```
  
  Populate it with:
- The current `SandwichChoice`
- Instances of every other entree type (excluding the current one)
  
  Then update the `SandwichChoice` property:
  
  ```
  public Entree SandwichChoice {
    get => _sandwichChoice;
    set {
        if (_sandwichChoice != null)
            _sandwichChoice.PropertyChanged -= HandleSandwichChange;
  
        _sandwichChoice = value;
        _sandwichChoice.PropertyChanged += HandleSandwichChange;
  
        OnPropertyChanged(nameof(Price));
        OnPropertyChanged(nameof(Calories));
        OnPropertyChanged(nameof(PreparationInformation));
        OnPropertyChanged(nameof(SandwichChoice));
        OnPropertyChanged(nameof(EntreeTypes));
    }
  }
  ```
  
  `HandleSandwichChange` should invoke `PropertyChanged` for `Price`, `Calories`, and `PreparationInformation`.
- ### **ComboBox Binding**
  
  In the Combo’s XAML:
- `ItemsSource="{Binding EntreeTypes}"`
- `SelectedItem="{Binding SandwichChoice}"`
- ### **Edit Buttons**
  
  Each “Edit” button (for entree, side, and drink) should:
- Display the customization screen for that item.
- Use a **custom event** to notify `MainWindow`.
  
  ---
- ## **MVVM Pattern (Model–View–ViewModel)**
- ### **Overview**
  
  A common architectural pattern (especially in mobile, web, and desktop applications) similar to **MVC**.
- **Model:** Holds the data.
- **View:** The XAML UI (ideally minimal code-behind).
- **ViewModel:** The “go-between” that contains logic for the View.
	- Holds an instance of the Model.
	- Exposes Model properties or adds logic-specific properties.
	- Acts as the **DataContext** for the View.
	  
	  In full MVVM:
- Each control would have its own ViewModel.
- Instead of event handlers (e.g., `Click`), you’d use **Commands** that trigger methods in the ViewModel, which then update bound properties.
  
  ---
- ## **Payment Control**
- ### **Purpose**
  
  Display final costs and allow the user to enter payment information.
  
  (*We’ll discuss data validation on Wednesday.*)
- ### **PaymentViewModel**
- Holds an instance of `Order`
- Serves as the **DataContext** for `PaymentControl`
- Exposes:
- #### **Pass-Through Properties**
  
  ```
  public decimal Subtotal => _order.Subtotal;
  ```
- #### **New Properties**
- `PaymentAmount`
- `Change`
- `EnoughFunds` (bool)
- `ErrorMessage` (string)
  
  Bind these in XAML:
  
  ```
  IsEnabled="{Binding EnoughFunds}"
  ```
  
  `ErrorMessage` should return an empty string if payment is valid, or the specific message otherwise.
  
  Because the ViewModel properties change dynamically, it must implement **INotifyPropertyChanged**.
  
  In the setter for `PaymentAmount`, invoke `PropertyChanged` for:
- `Change`
- `ErrorMessage`
- `EnoughFunds`
- `PaymentAmount`
  
  ---
- ### **Next Session**
  
  **Wednesday:** Data validation in WPF.
  
  ---