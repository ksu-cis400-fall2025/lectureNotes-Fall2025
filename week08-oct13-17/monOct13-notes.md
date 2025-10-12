## Announcements
collapsed:: true
	- **Data Binding Part 1**: **Due tonight**
		- Note: There’s a mistake when handling *Remove* in the tutorial.
		  Please read the Canvas assignment for the correction.
	- **Data Binding Part 2**: **Due Tuesday**
	- **Milestone 6**: **Due Thursday**
		- If you need an extra day, let me know by Thursday and I’ll move your deadline to Friday.
	- **No class on Friday**
- ## Milestone 6 Overview
  collapsed:: true
	- **Demo:** Let's see Milestone 6 demo.
	- **Summary:**
	- Use **Order** as the `DataContext` (requires some modifications to the `Order` class).
	- Display the **name** and **price** of each menu item in the order summary.
	- **Subtotal**, **tax**, and **total** update automatically as items are added.
	- **Cancel Order** button is implemented.
	- **Remove Item** functionality is implemented.
- ## Data Binding
  collapsed:: true
	- **Idea:** The front-end display is *bound* to back-end data — changing one automatically updates the other.
	- #### How It Works
		- Each **control** has a `DataContext`.
		- An attribute of a control can be *bound* to a property within that control’s `DataContext`.
		  
		  Examples:
		  
		  ```
		  Text="{Binding PropertyName}"
		  ///or
		  Text="{Binding Path=PropertyName}"
		  //or
		  if DataContext is IEnumerable:
		     ItemsSource="{Binding}"
		  ```
		-
		- Behavior:
		- The control looks for `PropertyName` in its `DataContext`.
			- If found → displays its value.
			- If not found → displays nothing (no error).
		- **Note:**
			- Different controls *can* have different `DataContexts`.
			- If a control doesn’t define its own, it *inherits* the `DataContext` of its parent container.
- ## Order Properties
  collapsed:: true
	- ### Number Property
		- Goal:
			- First order → 1
			- Next order → 2, and so on
			- Posile Solution:
			- ```
			  private static uint _nextOrderNum = 1;
			  private uint _number = _nextOrderNum++; // ++ happens after initialization
			  //In Number property
			  public uint Number => _number;
			  ```
	- ### PlacedAt Property
		- Type: `DateTime`
		- Get-only
		- Initialized to the current time
		- ```
		  public DateTime PlacedAt { get; } = DateTime.Now;
		  ```
- ## INotifyCollectionChanged
	- ```
	  //from INotifyCollectionChanged interface
	  public event NotifyCollectionChangedEventHandler? CollectionChanged;
	  ```
	-
	- This is an **event handler**.
	-
	- When a collection is bound to a `ListView`, WPF automatically listens for `CollectionChanged` events.
	- It attaches its own handler to redraw the GUI when the collection changes.
	  
	  You must invoke:
	  
	  ```
	  CollectionChanged?.Invoke(...)
	  ```
	  
	  **In the `Order` class:**
	  
	  Call `CollectionChanged` in the following methods:
	- `Add()`
	- `Remove()`
	- `Clear()`
	  
	  (See **Data Binding Tutorial 1** for examples.)
	  
	  ---
- ## Implementation Summary
  collapsed:: true
	- ### In  `Order` :
	- Add the `Number` and `PlacedAt` properties.
	- Implement `INotifyCollectionChanged`.
	- Invoke `CollectionChanged` in `Add`, `Remove`, and `Clear`.
	- ### In  `MainWindow` :
		- Set the `DataContext` to a new instance of `Order`.
	- ### In Order Summary XAML:
	  
	  Bind elements like this:
	  
	  ```
	  <TextBlock Text="{Binding Number, StringFormat='Order number: {0}'}" />
	  <TextBlock Text="{Binding PlacedAt, StringFormat='Placed at: {0}'}" />
	  <TextBlock Text="{Binding Subtotal, StringFormat='Subtotal: {0:C}'}" />
	  <TextBlock Text="{Binding Tax, StringFormat='Tax: {0:C}'}" />
	  <TextBlock Text="{Binding Total, StringFormat='Total: {0:C}'}" />
	  ```
	  
	  **In Menu Selection Code-Behind:**
	- Treat the `DataContext` as an `Order` object.
	- When done, you’ll have the same behavior as Milestone 5, but now **Order number**, **date**, and **subtotal/tax/total** come directly from `Order`.
	- Note: Subtotal, tax, and total will initially show `$0.00` until `Order` also implements `INotifyPropertyChanged`.
	  
	  ---
- ## Cancel Order Button
  collapsed:: true
	- ### How to Implement
	  
	  In XAML:
	  
	  ```
	  <Button Click="CancelOrderClick" Content="Cancel Order" />
	  ```
	  
	  In code-behind:
	  
	  ```
	  private void CancelOrderClick(object sender, RoutedEventArgs e)
	  {
	    if (DataContext is Order o)
	        o.Clear();
	  }
	  ```
	  
	  ---
- ## Displaying Items in Order Summary
  collapsed:: true
	- Example layout:
	  
	  ```
	  <ListView HorizontalContentAlignment="Stretch" ItemsSource="{Binding}">
	    <ListView.ItemTemplate>
	        <DataTemplate>
	            <StackPanel Orientation="Horizontal" HorizontalAlignment="Stretch">
	                <TextBlock Text="{Binding Name}" Width="100"/>
	                <TextBlock Text="{Binding Price, StringFormat={}{0:C}}" Width="80"/>
	                <Button Content="Remove" Click="RemoveItemClick"/>
	            </StackPanel>
	        </DataTemplate>
	    </ListView.ItemTemplate>
	  </ListView>
	  ```
	- ### Remove Button Event
	  
	  In code-behind:
	  
	  ```
	  private void RemoveItemClick(object sender, RoutedEventArgs e)
	  {
	    if (DataContext is Order o && sender is Button b && b.DataContext is IMenuItem item)
	        o.Remove(item);
	  }
	  ```
	  
	  ---
- ## Coming Next
  collapsed:: true
	- **Wednesday:** Implementing `INotifyPropertyChanged`
	- In `Add`, `Remove`, and `Clear`, you’ll invoke` PropertyChanged` to notify that` Subtotal`, `Tax`, and `Total` might have changed.
	  ---