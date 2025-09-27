- ---
- # Project Repository
  
  This repository currently contains only:
  
  README.md (this file)
  .gitignore
-
- No source code or other project files have been added yet.
- ## Important Note for Visual Studio Users
  When creating a new project in Visual Studio, make sure to:
  
  1. Select the correct repository folder, the locatin where you cloned the repo.
  
  2. Avoid letting Visual Studio create a nested repository (e.g., don’t create the project in a subfolder unless that is intentional).
  
  4. Verify that your .gitignore file is applied at the root level.
  
  This ensures that your project files are tracked correctly under version control.
- ### Correct Setup (all files in the repository root)  
  /MyRepo
  |-- .gitignore
  |-- README.md
  |-- MySolution.sln
  |-- Project1/
- ### Problematic Setup (nested repo inside a project folder)  
  /MyRepo
  |-- .gitignore
  |-- README.md
  |-- Project1/
  |-- .git/
  |-- MySolution.sln