## Deadlines & Announcements
- **Milestone 0**: due **Sunday, August 31st**
	- M0 due date is and exception!
	- We will discuss it today.
	- You can get help in class today and Friday.
- **Week 2 Module**: automatically available on **Friday, August 29**
	- No clase on Monday September 1st (labor day).
	- Includes two tutorials (due Tuesday and Wednesday).
	- **Milestone 1**: due Friday, September 05.
	  
	  ---
- ## Today’s Agenda
- Quick C# review
- Using Git from the terminal
- Branches and merging
- Start **Milestone 0**
  
  ---
- ## C# Review
- ### Example:  `Person`  Class
  
  ```
  public class Person {
    public string Name { get; set; }
    public int Age { get; set; }
  }
  
  Person pers1 = Person(); // Default constructor
  Person pers2 = Person(); // Default constructor
  ```
- ### Creating Objects and Setting Properties
	- There are several ways to set values for object properties in C#.
	- ### 1.  **Object Initializer (most common in modern C#)**
	- ```
	  // Concise way to assign properties when creating the object.
	  Person pers1 = new Person() { Name = "John Doe", Age = 40 };
	  Person pers2 = new Person() { Name = "Maria Smith", Age = 20 };
	  ```
	  
	  ---
	- ### 2.  **Using Property Setters After Creation**
	- ```
	  // Create the object, then set properties one by one.
	  Person pers3 = new Person();
	  pers3.Name = "Alice Johnson";
	  pers3.Age = 30;
	  ```
	  
	  ---
	- ### 3.  **Using a Constructor**
	- ```
	  //Define a constructor in the class, then set values when calling it.
	  public class Person {
	    public string Name { get; set; }
	    public int Age { get; set; }
	  
	    // Constructor
	    public Person(string name, int age) {
	        Name = name;
	        Age = age;
	  }
	  ```
	  
	  Usage:
	  
	  ```
	  Person pers4 = new Person("Bob Williams", 25);
	  ```
	  ---
	- ### Summary
	- **Object Initializer**: most concise; commonly used.
	- **Setters after creation**: flexible if you don’t know values at creation.
	- **Constructor**: enforces that values must be provided when the object is created.
	  
	  ---
-
- ### What Happens If We Print?
  
  ```
  Console.WriteLine(pers1);
  ```
- This prints the class name (e.g., `Namespace.Person`), not the property values, unless `ToString()` is overridden..
- ### Reference Behavior
  
  ```
  pers1 = pers2;
  pers1.Age++;
  Console.WriteLine(pers1.Age);
  Console.WriteLine(pers2.Age);
  ```
- Print
	- 21
	- 21.
	  
	  ---
- ## Git Basics
- ### Overall Idea
- **Remote repository**: hosted copy (the URL you clone).
- **Local repositories**: one or more copies on different computers.
	- Each local repository connects to the remote (“origin”).
	- Each local repository has a pointer to an active branch (`HEAD`).
		- `HEAD` in Git is a pointer to the current commit you are working on. It can point to any branch, including the default branch (whether it's `master` or `main`),
- Local repositories may have different active branches.
- Checking out a branch changes the code on your computer — but your other branches are still there.
- Workflow:
	- Pull remote changes → **update** local copy.
	- Make changes → **commit** → **push** to remote.
	  
	  ---
- ## Git Commands
- ### Check Status
  
  ```
  git status
  ```
- Shows current branch.
- Shows local changes (commit them if you want to keep them).
- ### Pull Changes
  
  ```
  git pull
  ```
- Updates the current branch with remote changes.
- First time: may need
  
  ```
  git pull origin <branchName>
  ```
- ### Fetch Remote Branches
  
  ```
  git fetch origin
  ```
- Retrieves all remote branches.
- Then you can checkout and pull specific branches.
- ### Commit & Push
  
  ```
  git add .
  git commit -m "Descriptive coomet of the commit"
  git push 
  ```
- First time:
  
  ```
  git push -u origin
  ```
-
-
- ### Tips
- Commit and push often. **Make sure code is clean**.
- Stay on your milestone branch until you finish.
- Merge into `main` only when done. **Make sure testing is completed and clear ALL test cases**
  
  ---
- ## Milestone 0 Walkthrough
- **Clone the repository** into Visual Studio.
- In the terminal:
  
  ```
  git status
  git branch ms0
  git checkout ms0
  git status
  ```
- Make changes:
	- **Calories**: subtract off ingredient amounts (e.g., Chicken = 150 calories).
	- **PreparationInformation**: add `Hold <ToppingName>` for excluded toppings.
- Commit changes:
  
  ```
  git status
  git add .
  git commit -m "finished milestone 0"
  git push
  git status
  ```
	- May see upstream issues (set with `git push -u origin ms0`).
- **Merge into main**:
  
  ```
  git checkout main
  git status
  git merge ms0
  git push
  ```
- Verify updates in remote repository (`ms0` branch + `main`).
  
  ---
- ## Key Terms
  
  Some key terms to learn in this chapter are:
- ### OOP
	- Class
	- Object
	- Constructor
	- Getter
	- Setter
- ### Software Configuration Manager
	- Version Control
	- Git
	- GitHub
	- Repository
	- Commit
	- Branch
	- Remote
	- Clone
	- Origin
	- Push
	- Pull