## Example: Sending a Message Between Controls
- ### Scenario
  
  We have:
- A **ColorSelectorControl** (UserControl) with two buttons: Red and Blue.
- A **MainWindow** that displays the selected color’s name in a `TextBlock`.
  
  When a button is clicked inside the `ColorSelectorControl`, it raises a **custom event** that sends the selected color to the **MainWindow**.
  
  ---
- ### **Step 1: Define What Needs to Be Sent**
  
  We need to send the selected color’s name.
  
  So, we create a **custom event args** class that carries a `ColorName` property.
  
  ```
  // Custom EventArgs class
  public class ColorSelectedEventArgs : RoutedEventArgs
  {
    public string ColorName { get; }
  
    public ColorSelectedEventArgs(string colorName)
    {
        ColorName = colorName;
    }
  }
  ```
  
  ---
- ### **Step 2: Declare the Event (in the control that triggers it)**
  
  ```
  public partial class ColorSelectorControl : UserControl
  {
    // Declare the event
    public event EventHandler<ColorSelectedEventArgs>? ColorSelected;
  
    public ColorSelectorControl()
    {
        InitializeComponent();
    }
  
    private void RedButton_Click(object sender, RoutedEventArgs e)
    {
        ColorSelected?.Invoke(this, new ColorSelectedEventArgs("Red"));
    }
  
    private void BlueButton_Click(object sender, RoutedEventArgs e)
    {
        ColorSelected?.Invoke(this, new ColorSelectedEventArgs("Blue"));
    }
  }
  ```
  
  ---
- ### **Step 3: Raise the Event**
  
  This is done in the button click handlers above, using:
  
  ```
  ColorSelected?.Invoke(this, new ColorSelectedEventArgs("Red"));
  ```
  
  ---
- ### **Step 4: Handle the Event (in MainWindow)**
  
  In the class that wants to *respond* to the message (here, `MainWindow`):
  
  ```
  public partial class MainWindow : Window
  {
    public MainWindow()
    {
        InitializeComponent();
  
        // Attach the handler
        ColorSelector.ColorSelected += OnColorSelected;
    }
  
    private void OnColorSelected(object? sender, ColorSelectedEventArgs e)
    {
        ColorText.Text = $"You selected: {e.ColorName}";
    }
  }
  ```
  
  ---
- ### **Step 5: Attach the Handler (XAML setup)**
  
  `MainWindow.xaml`:
  
  ```
  <Window x:Class="EventExample.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:local="clr-namespace:EventExample"
        Title="Event Example" Height="200" Width="300">
    <StackPanel>
        <local:ColorSelectorControl x:Name="ColorSelector"/>
        <TextBlock x:Name="ColorText"
                   FontSize="18"
                   Margin="10"
                   Text="No color selected yet."/>
    </StackPanel>
  </Window>
  ```
  
  `ColorSelectorControl.xaml`:
  
  ```
  <UserControl x:Class="EventExample.ColorSelectorControl"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation">
    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
        <Button Content="Red" Click="RedButton_Click" Margin="5"/>
        <Button Content="Blue" Click="BlueButton_Click" Margin="5"/>
    </StackPanel>
  </UserControl>
  ```
  
  ---
- ## 🧠  **Concept Summary**
- The **UserControl (ColorSelectorControl)** sends a message (event).
- The **MainWindow** listens for that message and reacts.
- The **CustomEventArgs** carries the data.
  
  ---
- ## 📊  **Diagram Option 1: UML Sequence Diagram**
  
  A **sequence diagram** works beautifully here.
  
  It shows how the message flows from user → control → main window.
  
  ```
  User     -> ColorSelectorControl : Click RedButton()
  ColorSelectorControl -> MainWindow : ColorSelected event (ColorName = "Red")
  MainWindow -> MainWindow : OnColorSelected(e)
  MainWindow -> UI : Update TextBlock.Text = "You selected: Red"
  ```
  
  *(You can render this in PlantUML or draw it in PowerPoint/Canvas using arrows.)*
  
  ---
- ## 🧱  **Diagram Option 2: Component / Object Diagram**
  
  If you prefer a more structural view, you can show **object relationships**:
  
  ```
  +--------------------+        raises event        +-------------------+
  | ColorSelectorControl|-------------------------> | MainWindow         |
  |  - RedButton        |                          |  - ColorTextBlock  |
  |  - BlueButton       |                          |  + OnColorSelected()|
  +--------------------+        (Custom Event)     +-------------------+
        |                                          ^
        | uses                                    |
        +------> ColorSelectedEventArgs(ColorName) +
  ```
  
  ---
- ## 🧭 Teaching Tip
  
  Have students:
- Implement this exact example.
- Then modify it to send *different* data (e.g., a selected menu item object).
- Finally, apply the same pattern in Milestone 7 (menu → main window).
  
  This helps them connect **custom events** to **practical use** in WPF projects.
  
  ---
  
  Would you like me to generate an actual **PlantUML sequence diagram code block** (so you can paste it into a PlantUML viewer or use in slides)?