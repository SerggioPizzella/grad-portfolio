# Context
At the time of writing, it is the end of week 15. The first initial [[Revised Project Plan]] has proven to be too ambitious and require more technical expertise than I can acquire in the remaining time of the internship. Therefore a new more realistic and flexible plan is being made. This time with more room for error. 

# Sprints
The way of working in the sprints as well as the structure shall remain the same. However the priority of the features has been adjusted.

## Sprint Plan
### ~~Sprint 1 (Weeks 13-14): Compile-Time Expressions~~
- **Goal**: Implement diagnostics for compile-time expressions, focusing on syntax, variable misuse (type analysis), and invalid functions.
- **Tasks**:
    - Learn techniques for walking an AST and performing static analysis.
    - Develop core library functionality for syntax validation.
    - Integrate diagnostics into the LSP.
    - Write unit tests for the core library.
    - Update technical documentation and C4 diagrams.
    
	
### Sprint 2 (Weeks 15-16): Template Parameters
- **Goal**: Validate template parameter definitions and usage.
- **Tasks**:
    - Research templating mechanisms and parameter usage in Azure Pipelines.
    - Develop core library functionality for template parameter checks.
    - Integrate the feature with the LSP for inline feedback.
    - Test the feature and refine diagnostics.
    - Update documentation and diagrams.

- **Must**:
	- As a user, when I am missing a required parameter on a template, I get diagnostics, such that I can identify what is missing and where.
	- As a user, when I provide a parameter that is not defined for the template, I get diagnostics, such that I know the parameter does not belong.
	- The feature works for local template files.
- **Should**
	- As a user, when I trigger code actions on a template, I get an action to add all the required parameters for my template, such that I can work more effectively.
	- As a user, when I type a parameter for a template, I get autocomplete suggestions, such that I don't need to type the full name.
	- The feature works for remote template files.
- **Could**
	- As a user, when I provide a parameter of the wrong type, I get diagnostics, such that I can determine the correct type.
	- As a user, when I reference a template, I get a action to insert all the required parameters, such that I don't need to type them.
	- As a user, when I hover over a template parameter, I get documentation about the parameter.

- **Docs**
	* Create a structured research document.
	* Express why I didn't use the Microsoft SDK.
	* Express why I didn't fork the Microsoft LSP.
	* Express we can follow the structure from the MS service package.
	* Express the transition from C# to JS.
	
### Sprint 3 (Weeks 17-18): Variable Scope
- **Goal**: Provide diagnostics for variable suggestions and scope validation.
- **Tasks**:
    - Research how Azure Pipelines does variable resolution.
    - Implement core functionality to validate variable scope.
    - Extend LSP to highlight variable scope issues in the editor.
	- Implement core functionality to suggest variables within scope.
    - Write unit tests and refine error messages.
    - Update technical documentation and diagrams.
	
- **Docs**
	* Express things learned from the interview.
	* Express why the current extension from Microsoft isn't good enough.
	* Express why the current extension from Christopher isn't good enough.

### sprint 4 (week 19): Touch-ups
* **goal**: Review the structure and quality of the research.
* **tasks:**
	* Review reading guide.
	* Review C4 diagrams + explanation.
	* Express reflection points learned from this process.
	* Express how the project could be extended to include suggestions 1 and 4, as I did 2 and 3.