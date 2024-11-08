---
date: 2024-10-29
title: 02 Create a custom parser
---
- Status: proposed
- Deciders: Serggio Pizzella, Luuk Horsman
- Informed: Erik Schriek

## Context and Problem Statement
The goal is to develop a diagnostic tool that provides real-time feedback on Azure Pipeline YAML files, addressing specific developer frustrations. According to [[Survey]], the main challenges include:
- compile-time expressions.
- variable scope (at stage, job, and template level),
- template parameters.
- condition statements. 

Developers frequently encounter issues in these areas, leading to lengthy troubleshooting cycles and reduced productivity. Current tools lack the capability to provide Azure-specific feedback. This ADR addresses the parsing method that will be used to achieve this.

## Decision Drivers
1. **Need for Azure-specific feedback**: Existing parsers do not recognize Azure-specific syntax and features.
2. **Ease of development**: Reducing the time and expertise required to implement the method.
3. **Maintainability**: Ensuring the solution can be adapted or updated as Azure Pipelines evolve.
4. **Precision in Error Reporting**: Delivering specific indicators of where issues occur.
1. **Resilient**: Must be able to handle partial/incomplete input, or input with errors.
5. **Performance**: Must re-parse efficiently to support real-time feedback during frequent edits.

## Considered Options
- Extending `eemeli/yaml` with [Custom Tags – YAML](https://eemeli.org/yaml/#writing-custom-tags).
- Extending `eemeli/yaml` with custom parser on top.
- Creating a parser from Scratch, using a parser generator (ANTLR or Tree-sitter).
- Extending a grammar from a parser generator (ANTLR or Tree-sitter).
- Extending ESLint with a YAML Plugin.

## Decision Outcome
Chosen option: **Extending a grammar from a parser generator**, because this approach maximizes extendibility and provides the most control over performance by leveraging a mature YAML grammar as a foundation. By building on a tested grammar, we can focus on implementing Azure-specific syntax and error handling without re-implementing YAML parsing. This option also offers flexibility for future expansions or adjustments if Azure Pipelines requirements evolve.

### Consequences

- **Positive**: High control over performance, with flexibility to optimize parsing based on the chosen parser language.
- **Positive**: Strong extendibility, allowing precise Azure-specific diagnostics without needing to re-implement YAML parsing.
- **Positive**: Adaptability for future expansions, as grammar modifications can support new Azure Pipeline syntax.
- **Negative**: Initial setup complexity, requiring familiarity with the parser generator and grammar customization.

## Pros and Cons of the Options
### Extending `eemeli/yaml` with Custom Tags

**Pros** :
- Integrates Azure-specific syntax within YAML parsing, maintaining a single AST.
- Provides a well defined and unified API for walking the AST.
- Minimal additional code required for Azure-specific diagnostics, simplifying the setup.
- Maintains readability and ease of extension within JavaScript.

 **Cons**:
- Limited by the Custom Tags API, which may not handle all Azure-specific scenarios.
- Seems to be significantly more involved than writing a grammar.

**Neutral**:
- The additional types are defined as part of the program itself.
* It is the same parser used by Microsoft.


---

### Extending `eemeli/yaml` with Custom Parser on Top

 **Pros**:
 - Enables complete control over Azure-specific parsing.
 - Separates Azure-specific logic from general YAML parsing, improving maintainability if Azure or YAML specific requirements change.
 
 **Cons**:
 - Requires parsing both Azure-specific syntax and the output from `eemeli/yaml`, increasing the implementation complexity.

---

### Creating a Parser from Scratch, Using a Parser Generator (ANTLR or Tree-sitter)

 **Pros**:
 - Maximum flexibility for creating a fully custom Azure-specific parsing solution.
 - The Azure-syntax definition is separate from the parser implementation, which allows a more declarative approach.
 
 **Cons**:
 - High time and resource investment; building a reliable YAML parser from scratch is complex.
 - Performance risks due to the complexity and overhead of a fully custom parser.

---

### Extending a Grammar from a Parser Generator (ANTLR or Tree-sitter)

 **Pros**:
 - Allows leveraging an existing YAML grammar and extending it with Azure-specific rules.
 - Balances flexibility and maintainability by building on a tested grammar, focusing effort on Azure-specific needs.
 
 **Cons**:
 - Requires understanding of the parser generator’s grammar syntax and existing YAML grammar.
 - Potentially impacts performance, especially if modifications lead to inefficiencies in parsing.

---

### Extending ESLint with a YAML Plugin

 **Pros**:
 - Integrates with existing linting infrastructure, simplifying setup for users already familiar with ESLint.
 
 **Cons**:
 - May be challenging to customize for Azure-specific syntax; YAML plugins for ESLint lack the depth needed for Azure Pipeline configurations.
 - ESLint was not build for being used as a parser, thus there will be many limitations and shortcomings.
