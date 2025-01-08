## Methodology
The project follows an agile methodology using [Kanban](https://www.atlassian.com/agile/kanban) **with sprints**. Kanban is well-suited for individual work due to its flexibility and simplicity. It allows for continuous task management and adaptation to changing priorities without the need for formal iterations or roles, which would mostly be taken by the student. Throughout the project, the approach shifted to emphasize **vertical slices** within sprints, delivering incremental functionality.

## Evolution of the Approach
**[[Project Plan.pdf#page=12 |Version 1: Initial Plan:]]**
- The initial approach divided the project into distinct phases, including planning, research, development, and documentation. Each phase had specific objectives, such as defining project goals, researching Azure Pipelines, and implementing features in iterative 2-week sprints.
- This version aimed for a comprehensive execution but lacked room for concurrent progress in research and development, leading to delays in resolving complex sub-questions.

**[[Revised Project Plan| Version 2: Revised Plan]]**
- By Week 12, the project had fallen behind schedule. A revised plan introduced concurrent research and development within sprints to better align with deliverables and ensure progress. The focus shifted to delivering vertical slices, emphasizing functionality rather than sequential phases.
- The updated sprint structure integrated research into development, addressing techniques as needed for each feature.
- New priorities were introduced for features, starting with diagnostics for compile-time expressions, followed by variable scope and template parameters.

**[[Revised Project Plan v2| Version 3: Final Plan]]**
- At the end of Week 15, the revised plan proved too ambitious. A further adjustment removed compile-time expressions from the sprint plan to focus on template parameters and variables, which offered more achievable goals given the remaining time, or lack thereof.
- This version included a smaller scope and wiggle room, allowing more flexibility and accommodating potential setbacks. The emphasis was on delivering core features with realistic scopes.

## Final Sprint Plan
Each sprint addresses a complete feature or aspect of the tool:

### **Sprint 2 (Weeks 15-16): Template Parameters**

- **Goal:** Validate and provide diagnostics for template parameter definitions and usage.
- **Tasks:**

- Research templating mechanisms.
- Implement core library functionality for parameter validation.
- Integrate diagnostics into the language server for real-time feedback.
- Test and refine diagnostics.
- Update technical documentation and C4 diagrams.

- **Priorities:**

- **Substitute for references to the URS.**
- Must: Missing/undefined parameters, local template support.
- Should: Autocomplete for parameters, remote template support.
- Could: Type mismatch diagnostics, hover documentation.

### 1.3.2       **Sprint 3 (Weeks 17-18): Variables**

- **Goal:** Provide diagnostics for variable suggestions and scope validation.
- **Tasks:**

- Research Azure Pipelines variable resolution.
- Implement core functionality for validating scope and suggesting variables.
- Extend LSP for scope-related diagnostics.
- Write unit tests and refine error messages.
- Update technical documentation and diagrams.

- **Priorities:**

- **Substitute for references to the URS.**
- Must: Undefined variable diagnostics, variable suggestions.
- Should: Scope enforcement and documentation on hover.
- Could: Type mismatch detection, scope-specific warnings.

### 1.3.3       **Sprint 4 (Week 19): Touch-Ups**

- **Goal:** Finalize documentation and ensure deliverable quality.
- **Tasks:**

- Review the reading guide and technical documents.
- Refine C4 diagrams and their explanations.
- Document reflections and potential future extensions for the tool.

### 1.3.4       Sprint 5 (Weeks 20-21): Overtime

By the start of Week 20, all project documentation, including the final project report, C4 diagrams, and graduation portfolio, must be delivered. Week 19 is dedicated to ensuring that all documentation is complete and ready for submission. After submission, Week 20 allows for additional coding efforts to address any features or enhancements not completed in their respective sprints.

- **Goal:** **Use the remaining time to implement and test any** **should** **or** **could** **features that were deprioritized or not completed during earlier sprints.**
- **Tasks:**

- **Review the backlog to identify unimplemented features.**
- **Select tasks based on feasibility and their potential to improve the tool's functionality.**
- **Implement selected features and write tests to ensure quality.**
- **Update technical documentation to reflect any changes or additions.**

This sprint ensures no time is wasted after documentation submission and allows for further refinement of the tool; alleviating pressure from the preceding sprints. Features that remain unimplemented by the end of Week 21 will be documented as potential extensions.

### 1.3.5       3.4 Key Changes Across Versions

1.      **Integration of Research and Development:** The initial plan had separate phases for research and implementation. This was revised to combine them within sprints, improving flexibility and alignment with project goals.

2.      **Adjusted Priorities:** The focus narrowed from tackling all major pain points to a subset with the most significant impact, ensuring realistic deliverables.

3.      **Room for Error:** The final version added contingency measures, removing overly ambitious goals like compile-time expressions, to focus on achievable outcomes within the remaining time.