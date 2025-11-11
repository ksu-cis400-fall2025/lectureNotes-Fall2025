## Announcements
collapsed:: true
	- ### Milestone 8
	- **Extended deadline:** Sunday, October 27
	- **Reminder:** Milestones 7 and 8 are the two largest milestones of the course.
	  
	  ---
- ## Data Validation in WPF
  collapsed:: true
	- ### Example
	  
	  ```
	  <TextBox>
	    <TextBox.Text>
	        <Binding Path="SomePropertyName" Delay="500" UpdateSourceTrigger="PropertyChanged">
	            <Binding.ValidationRules>
	                <ExceptionValidationRule/>
	            </Binding.ValidationRules>
	        </Binding>
	    </TextBox.Text>
	  </TextBox>
	  ```
		- ### Explanation
		- The **`ExceptionValidationRule`** displays a red border around the `TextBox` if setting the bound property throws an exception.
		  
		  Note: It will not attempt to set the property if the entered value does not match the property’s expected type.
		- The default `UpdateSourceTrigger` for a `TextBox` is **`LostFocus`** (i.e., the binding updates only when the control loses focus).
		  
		  We can change it to **`PropertyChanged`** so that data validation occurs **as the user types**.
		- The **`Delay="500"`** attribute waits for 500 milliseconds before applying the update, allowing the user to finish typing.
		  
		  ---
		- ### Discussion
		- See a similar example in the tutorial.
		- **Question:** What if we wanted the cost to display as **`$0.00`** when the number of shirts is invalid?
		  
		  ---
- ## Printing the Receipt
  collapsed:: true
	- You can write a receipt to a text file using:
	  
	  ```
	  File.AppendAllText("receipts.txt", someGiantTextString);
	  ```
	- ### Question
	  
	  How can we **build** that text string?
	  
	  Think about including the order details, subtotal, tax, and total in a clear format.
	  
	  ---
- ## Hiding the “Make It a Combo” Button
  collapsed:: true
	- ### Goal
	  
	  Make the **“Make it a Combo”** button visible only when appropriate.
	- ### Behavior
	- **Visible:** when the entrée is **not part of a combo**
	- **Hidden:** when the entrée **is part of a combo**
	- ### Implementation Steps
	- Add a **property** to the `Entree` class to track whether it belongs to a combo.
	- Each time an entrée control becomes visible, check that property.
	- Set the button’s visibility based on the property’s value.
	  
	  ---
- ## Upcoming Topics and Deadlines
  collapsed:: true
	- **Next week:** Focus on documentation, UML, and testing related to Milestones 6–8.
	- **Tutorial:** One session—**UML considerations in WPF**.
	- **Exam 2:** Wednesday, **November 6**.
	- **Wednesday’s discussion:** Data validation examples and handling invalid user input.
	  
	  ---