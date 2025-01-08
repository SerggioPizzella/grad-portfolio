- Status: Superseded by [[Approach]]
# Context
At the time of writing, it is the end of week 15. The first initial [[Revised Project Plan]] has proven to be too ambitious and require more technical expertise than I can acquire in the remaining time of the internship. Therefore a new more realistic and flexible plan is being made. This time with more room for error. 

# Sprints
The way of working in the sprints as well as the structure shall remain the same. However the priority of the features has been adjusted.

## Sprint Plan

_Sprint 1 has been removed._
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

#### Must
- **Missing Required Parameter Diagnostics**  
    _As a user, when I fail to provide a required parameter for a template, I get a diagnostic message indicating the missing parameter and where it is required, so I can add it._
    
- **Undefined Parameter Diagnostics**  
    _As a user, when I include a parameter not defined in the template, I get a diagnostic message highlighting the undefined parameter, so I can correct the mistake._
    
- **Local Template Support**  
    _As a user, when I use local template files, I receive diagnostics for missing or undefined parameters, ensuring the feature is fully functional for local templates._
    

#### Should
- **Code Actions for Required Parameters**  
    _As a user, when I trigger a code action on a template, I receive an option to add all required parameters for that template, making the process more efficient._
    
- **Autocomplete for Parameters**  
    _As a user, when I begin typing a parameter for a template, I get autocomplete suggestions for valid parameter names, so I can avoid errors and save time._
    

#### Could

- **Wrong Type Parameter Diagnostics**  
    _As a user, when I provide a parameter with an incorrect type, I get a diagnostic message indicating the type mismatch, so I can adjust it._
    
- **Hover Documentation for Parameters**  
    _As a user, when I hover over a template parameter, I see documentation about the parameter, including its expected type and usage, so I can use it correctly._
    
- **Remote Template Support**  
    _As a user, when I use remote template files, I receive the same diagnostics for missing or undefined parameters, ensuring full support for remote templates._

#### Docs
* Create a structured research document.
* Express why I didn't use the Microsoft SDK.
* Express why I didn't fork the Microsoft LSP.
* Express we can follow the structure from the MS service package.
* Express the transition from C# to JS.

### Sprint 3 (Weeks 17-18): Variables
- **Goal**: Provide diagnostics for variable suggestions and scope validation.
- **Tasks**:
    - Research how Azure Pipelines does variable resolution.
    - Implement core functionality to validate variable scope.
    - Extend LSP to highlight variable scope issues in the editor.
	- Implement core functionality to suggest variables within scope.
    - Write unit tests and refine error messages.
    - Update technical documentation and diagrams.

#### Must
- **Diagnostics for Undefined Variables**  
    _As a user, when I reference a variable that is not defined in the current scope, I get a diagnostic message identifying the undefined variable and its location, so I can correct it._
    
- **Variable Completion**  
    _As a user, when I begin typing a variable name, I get autocomplete suggestions for variables available in the current scope, so I can avoid errors and save time._

#### Should
- **Scope Enforcement**  
    _As a user, when I define variables in a scope where they are inaccessible, I get a diagnostic message to understand where and why the variable is inaccessible._
    
- **Documentation on Hover**  
    _As a user, when I hover over a variable, I see documentation about its scope and definition, so I can confirm its proper use._
	
#### Could
- **Misused Variable Type Detection**  
    _As a user, when I assign or use a variable in a way that is incompatible with its type, I get a diagnostic message, so I can address the type mismatch._
    
- **Scope-Specific Warnings**  
    _As a user, when I attempt to override a variable in a child scope, I receive a warning, helping me avoid unexpected behaviours._
	
#### Docs
* Express things learned from the interview.
* Express why the current extension from Microsoft isn't good enough.
* Express why the current extension from Christopher isn't good enough.

### sprint 4 (week 19): Touch-ups
* **goal**: Review the structure and quality of the research.
* **tasks:**
	- Review the reading guide and technical documents.
	- Refine C4 diagrams and their explanations.
	- Document reflections and potential future extensions for the tool.

### Sprint 5 (Weeks 20-21): Overtime
By the start of Week 20, all project documentation, including the final project report, C4 diagrams, and graduation portfolio, must be delivered. Week 19 is dedicated to ensuring that all documentation is complete and ready for submission. After submission, Week 20 allows for additional coding efforts to address any features or enhancements not completed in their respective sprints.
    
- **Goal:** Use the remaining time to implement and test any **should** or **could** features that were deprioritized or not completed during earlier sprints.
- **Tasks:**
	- Review the backlog to identify unimplemented features.
	- Select tasks based on feasibility and their potential to improve the tool's functionality.
	- Implement selected features and write tests to ensure quality.
	- Update technical documentation to reflect any changes or additions.

This sprint ensures no time is wasted after documentation submission and allows for further refinement of the tool; alleviating pressure from the preceding sprints. Features that remain unimplemented by the end of Week 21 will be documented as potential extensions.