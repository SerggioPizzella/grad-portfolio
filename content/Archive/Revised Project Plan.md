- Status: Superseded by [[Revised Project Plan v2]]
# Context
At the time of writing, the project is in Week 12 and Sub-question 3 from the original [[Project Plan.pdf]] has not been finalized, therefore a new plan is being instated to ensure the project meets Info Support's and Fontys' requirements within the remaining time.

# Sprints
The revised plan uses a sprint-based approach where research and development progress concurrently, focusing on vertical slices to deliver a functional tool with Language Server Protocol (LSP) integration. Each sprint will tackle a complete feature, from implementing core library functionality to integrating it with the LSP for real-time diagnostics. Research will be conducted on-demand, addressing specific techniques needed for the feature in focus during that sprint. Throughout the process, technical documentation and C4 diagrams will be incrementally updated to reflect new components and interactions, ensuring the deliverables remain up-to-date.

This approach will allows for more flexibility and ensures that by the end of the project a subset of the original goals are reached.

## Sprint Structure
Each sprint will include the following steps:
1. **Planning**:
    - Define research needs for implementing the feature.
    - Create specific tasks for core functionality, testing, integration and documentation.
2. **Research & Development**:
    - Research the technique or method required for the feature.
    - Implement the feature in the core library.
    - Integrate the feature with the LSP.
3. **Testing**:
    - Write tests for the implemented feature.
    - Validate performance and reliability within the LSP context.
4. **Documentation**:
    - Update C4 diagrams with new components and interactions.
    - Document technical details and implementation choices.
5. **Review**:
    - Assess progress and refine the backlog for the next sprint.
6. **Delivery**: 
	- The updated documentation as well as a short clip demonstrating the feature, will be delivered at the end of the sprint.
## Sprint Plan
### Sprint 1 (Weeks 13-14): Compile-Time Expressions
- **Goal**: Implement diagnostics for compile-time expressions, focusing on syntax, variable misuse (type analysis), and invalid functions.
- **Tasks**:
    - Learn techniques for walking an AST and performing static analysis.
    - Develop core library functionality for syntax validation.
    - Integrate diagnostics into the LSP.
    - Write unit tests for the core library.
    - Update technical documentation and C4 diagrams.

### Sprint 2 (Weeks 15-16): Variable Scope
- **Goal**: Provide diagnostics for variable suggestions and scope validation.
- **Tasks**:
    - Research how Azure Pipelines does variable resolution.
    - Implement core functionality to validate variable scope.
	- Implement core functionality to suggest variables within scope.
    - Extend LSP to highlight variable scope issues in the editor.
    - Write unit tests and refine error messages.
    - Update technical documentation and diagrams.

### Sprint 3 (Weeks 17-18): Template Parameters
- **Goal**: Validate template parameter definitions and usage.
- **Tasks**:
    - Research templating mechanisms and parameter usage in Azure Pipelines.
    - Develop core library functionality for template parameter checks.
    - Integrate the feature with the LSP for inline feedback.
    - Test the feature and refine diagnostics.
    - Update documentation and diagrams.

# Info Support - Feedback point 
During sprint 1, on Wednesday 4th December, a feedback point with be held. The material for this meeting must be delivered by Friday 29th November. 
- **Deliverables**:
	- [[Project Plan.pdf]]
	- [[Survey Report - Azure Pipelines DX .pdf]]
	- [[01-use-markdown-architectural-decision-records]]
	- [[02-parsing-strategy]]
	- [[03-how-to-make-parser]]
	- 04-going-trough-the-AST
	- Code capable of creating and navigating an AST, with tests.
