## Non-Functional Requirements
#### User-Friendliness
- **NFR-1**: **Seamless Integration**  
    The tool must require minimal setup and integrate naturally into the developer’s workflow. It should work immediately after installation, requiring minimal configuration. Where possible, configuration must be automated.

- **NFR-2**: **IDE Independence**  
	The tool must operate effectively regardless of the Integrated Development Environment (IDE) being used (e.g., Visual Studio Code, Neovim, or other IDEs). While IDE-specific bridges (e.g., a VS Code plugin or a Neovim configuration) may be required, these should be minimal, and as much functionality as possible must be implemented within the core library to ensure consistent behaviour across IDEs.

- **NFR-3**: **Intuitive Error Feedback**  
    The tool must provide detailed, actionable error messages and suggestions for resolving issues, supporting developers in understanding and addressing problems efficiently.
   
---
#### Performance
- **NFR-4**: **Real-Time Validation**
    The tool must validate Azure Pipelines YAML files in real time or with minimal delay, ensuring feedback is always faster than the current commit-to-Azure-DevOps workflow.

- **NFR-5**: **Scalability**  
    The tool must handle large and complex YAML files, with multiple nested templates, without catastrophic degradation in performance.
 
---
#### Code Quality and Maintainability
- **NFR-6**: **Code Quality Standards**  
    The codebase must adhere to [internal company coding standards](https://guidance.infosupport.com/) and industry best practices, including the use of tools like SonarQube to ensure high-quality code.
    
- **NFR-7**: **Automated Code Quality Monitoring**  
    SonarQube (or equivalent) scans must be performed regularly to monitor key metrics such as:
    - Code smells
    - Bugs
    - Vulnerabilities
    - Duplications  

---
#### Testing and Reliability
- **NFR-8**: **Test Coverage**  
    The tool must achieve at least 80% unit test coverage for all significant pieces of code.
    
- **NFR-9**: **Continuous Integration**  
    A Continuous Integration (CI) pipeline must be in place to:
    - Automatically build the tool.
    - Run all tests and perform code quality analysis.
	
- **NFR-10**: **Performance Testing**  
    Performance benchmarks (e.g., sub-second diagnostics) must be validated through regular performance testing, and code should be optimized if benchmarks are not met.

---
#### Documentation
- **NFR-11**: **Technical Documentation**  
    The tool must include clear, up-to-date documentation covering setup, usage, configuration, and troubleshooting.

---
#### Operation
- **NFR-12**: **Local Execution**  
	The tool must operate primarily on the local machine, achieving as much functionality as possible without relying on external services. Any external service calls (e.g., for fetching templates or credentials) should be minimal, and must not prevent the tool from operating.

---
## Functional Requirements
These are categorized by the recommendations made in the [[Survey#Survey Report - Azure Pipelines DX.pdf page=12 Recommendations |Survey Recommendations]]. For each category we determine it's `MoSCoW` requirements. Once a category meet's all it's `Must` requirements, we can fairly say that the tool supports the Category and has fulfilled the recommendation.
### Compile-Time Expressions

#### Must
- **FR-1: Syntax Validation Diagnostics**  
    _As a user, when I write an expression with missing or unbalanced brackets, I get a diagnostic message pointing out the syntax error and where it occurs, so I can correct it immediately._
    
- **FR-2: Invalid Function Diagnostics**  
    _As a user, when I use an undefined function in a compile-time expression, I get a diagnostic message identifying the invalid function, so I can replace it with a valid one._
    
- **FR-3: Autocomplete for Functions**  
    _As a user, when I type the beginning of a function name in a compile-time expression, I receive autocomplete suggestions for valid functions, so I can save time and avoid mistakes._

#### Should

- **FR-4: Argument Count Validation**  
    _As a user, when I call a function with an incorrect number of arguments, I get a diagnostic message detailing the required and provided argument counts, so I can fix the issue._
    
- **FR-5: Type Mismatch Diagnostics**  
    _As a user, when I use an incorrect type in a compile-time expression, I receive a diagnostic message describing the mismatch, so I can adjust it to the correct type._

#### Could
- **FR-6: Hover Documentation for Functions**  
    _As a user, when I hover over a function name in a compile-time expression, I see documentation about its purpose, expected arguments, and return type, so I can use it correctly._
    
- **FR-7: Error Recovery for Partial Input**  
    _As a user, when I write a partial or incomplete compile-time expression, I still receive diagnostic feedback for the complete portions, so I can iteratively refine the expression._

---
### Template Parameters
#### Must
- **FR-8: Missing Required Parameter Diagnostics**  
    _As a user, when I fail to provide a required parameter for a template, I get a diagnostic message indicating the missing parameter and where it is required, so I can add it._
	**Acceptance Criteria 1:**
	When the `parameters` key is missing, the diagnostics must be placed on the `template` key.

	**Acceptance Criteria 2:**
	When a parameter is missing, the diagnostics must be placed on the `parameters` key.

	**Acceptance Criteria 3:**
	When a parameter's value is missing, the diagnostics must be placed on the respective parameter's key.
   
* **FR-9: Undefined Parameter Diagnostics**  
    _As a user, when I include a parameter not defined in the template, I get a diagnostic message highlighting the undefined parameter, so I can correct the mistake._ 
 
- **FR-10: Local Template Support**  
    _As a user, when I use local template files, I receive diagnostics for missing or undefined parameters, ensuring the feature is fully functional for local templates._

#### Should
- **FR-11: Code Actions for Required Parameters**  
    _As a user, when I trigger a code action on a template, I receive an option to add all required parameters for that template, making the process more efficient._
    
- **FR-12: Parameters Completion**  
    _As a user, when I begin typing a parameter for a template, I get autocomplete suggestions for valid parameter names, so I can avoid errors and save time._
	
	**Acceptance Criteria 1:**
	I must only receive suggestion for variables that have not already been provided.
	
	**Acceptance Criteria 2:**
	I must receive suggestions even when I'm one line below the template parameters scope.
	
#### Could
- **FR-13: Wrong Type Parameter Diagnostics**  
    _As a user, when I provide a parameter with an incorrect type, I get a diagnostic message indicating the type mismatch, so I can adjust it._
    
- **FR-14: Hover Documentation for Parameters**  
    _As a user, when I hover over a template parameter, I see documentation about the parameter, including its expected type and usage, so I can use it correctly._
    
- **FR-15: Remote Template Support**  
    _As a user, when I use remote template files, I receive the same diagnostics for missing or undefined parameters, ensuring full support for remote templates._

---
### Variables

#### Must
- **FR-16: Scope Validation Diagnostics**  
    _As a user, when I reference a variable outside its valid scope, I receive a diagnostic message explaining why the variable is inaccessible, so I can make the necessary corrections._

- **FR-17: Variable Completion**  
    _As a user, when I begin typing a variable name, I get autocomplete suggestions for variables available in the current scope, so I can avoid errors and save time._

#### Should
- **FR-18.1: Variable Hover Information**  
    _As a user, when I hover over a variable, I see its source, type, and current value (if statically determinable), so I can better understand its usage._

	**Acceptance Criteria 1:**
	When hovering over the variable, I see where the variable has been specified, and if applicable, the template it comes from.
	
	**Acceptance Criteria 2:**
	When hovering over the variable, I see the type of the variable if it has been specified.
	
- **FR-19: Conflict Warnings**  
    _As a user, when I define a variable that conflicts with an existing one in the same scope, I receive a warning, so I can avoid unexpected behaviour._

#### Could
- **FR-20: Reference Tracking**  
    _As a user, when I view a variable, I can navigate to all its references throughout the pipeline, so I can easily track its usage._

	**Acceptance Criteria 1:**
	As a user, I can use `go to definition` to navigate to the line that adds the variable to the scope. 

	**Acceptance Criteria 2:**
	As a user, I can use `go to references`	to navigate to all the places where the variable is used.
	
- **FR-18.2: Variable Hover Information**  
	**Acceptance Criteria 3:**
	When hovering over the variable, I see the statically determined value, if it's been defined.

	**Acceptance Criteria 4:**
	When hovering over the variable, I see the statically determined value, if it's derivable from the context.

- **FR-21: Suggestions for Undefined Variables**  
    _As a user, when I reference an undefined variable, I receive suggestions for similarly named variables, so I can fix potential typos quickly._
 
---
### Conditions at Job and Stage Levels

#### Must
- **FR-22: Invalid Condition Syntax Diagnostics**  
    _As a user, when I write an invalid condition, I get a diagnostic message pinpointing the error, so I can correct it._
    
- **FR-23: Function Validation in Conditions**  
    _As a user, when I use an undefined or incorrect function in a condition, I receive a diagnostic message, so I can fix the function call._

#### Should
- **FR-24: Condition Expression Suggestions**  
    _As a user, when I begin writing a condition, I get suggestions for valid expressions and functions, so I can write correct conditions faster._
    
- **FR-25: Validation of Nested Conditions**  
    _As a user, when I write a nested condition, I receive diagnostics for errors in each part of the condition, so I can fix them comprehensively._
    

#### Could
- **FR-26: Condition Debugging Feedback**  
    _As a user, when a condition fails at runtime, I receive information about which part of the condition caused the failure, so I can debug effectively._
    
- **FR-27: Contextual Autocomplete for Conditions**  
    _As a user, when I write a condition in a specific context (job or stage level), I receive autocomplete suggestions for variables and expressions relevant to that context._