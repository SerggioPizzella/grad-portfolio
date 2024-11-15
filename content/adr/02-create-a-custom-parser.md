---
date: 2024-10-29
title: 02 Parser solution
---
## Context and Problem Statement
Current tools lack the capability to provide Azure-specific feedback. To achieve this we require a parser capable of understanding the Azure pipelines syntax, this goes beyond parsing YAML, as to give insightful feedback, we also need to need to understand the embedded expressions. These are denoted by using `${{ }}`, `$[ ]`  or simply as function calls in the shape `function()`. This ADR addresses the parsing method that will be used to achieve this.

## Decision Drivers
1. **Azure-specific**: Existing parsers do not recognize Azure-specific syntax and features.
1. **Resilient**: Must be able to handle partial/incomplete input, or input with errors.
2. **Ease of development**: Reducing the time and expertise required to implement the method.
4. **Precision in Error Reporting**: Delivering specific indicators of where issues occur.
3. **Maintainability**: Ensuring the solution can be adapted or updated as Azure Pipelines evolve.
5. **Performance**: Must re-parse efficiently to support real-time feedback during frequent edits.

## Considered Options
- Extending [eemeli/yaml](https://eemeli.org/yaml/) with [Custom Tags – YAML](https://eemeli.org/yaml/#writing-custom-tags).
- Extending [eemeli/yaml](https://eemeli.org/yaml/) with custom parser.
- Extending [js-yaml]([js-yaml - npm](https://www.npmjs.com/package/js-yaml)) with custom parser.
- Creating a parser from scratch, using a parser generator (ANTLR or Tree-sitter).
- Extending a grammar from a parser generator (ANTLR or Tree-sitter).
- Extending ESLint's [YAML Plugin](https://www.npmjs.com/package/eslint-plugin-yml).

## Decision Outcome

### Extending `eemeli/yaml` with Custom Parser on Top
`eemeli/yaml` is the self-proclaimed "[definitive library for YAML](https://www.npmjs.com/package/yaml) it provides most of what we are looking for.

 **Pros**:
 - Enables complete control over Azure-specific parsing.
 - Separates Azure-specific logic from general YAML parsing, improving maintainability if Azure or YAML specific requirements change.
 
 **Cons**:
 - Requires parsing both Azure-specific syntax and the output from `eemeli/yaml`, increasing the implementation complexity.

## Other Options

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

---

### Creating a Parser from Scratch, Using a Parser Generator (ANTLR or Tree-sitter)

 **Pros**:
 - Maximum flexibility for creating a fully custom Azure-specific parsing solution.
 - The Azure-syntax definition is separate from the parser implementation, which allows a more declarative approach.
 
 **Cons**:
 - High time and resource investment; building a reliable YAML parser from scratch is complex.
 - Performance risks due to the complexity and overhead of a fully custom parser.

This option certainly allows us to make an Azure-specific parser. It offers the most potential to meet all the criteria, dependant on implementation. However it also requires the most knowledge and expertise, as well as requiring the most time.
Additionally, YAML is a [Context-sensitive grammar](https://en.wikipedia.org/wiki/Context-sensitive_grammar), which results in it not being parse-able by a parser generator without additional help.

--- 

### Extending a Grammar from a Parser Generator (ANTLR or Tree-sitter)

 **Pros**:
 - Allows leveraging an existing YAML grammar and extending it with Azure-specific rules.
 - Balances flexibility and maintainability by building on a tested grammar, focusing effort on Azure-specific needs.
 
 **Cons**:
 - Requires understanding of the parser generator’s grammar syntax and existing YAML grammar.
 - Potentially impacts performance, especially if modifications lead to inefficiencies in parsing.

---

### Extending ESLint with a [YAML Plugin](https://www.npmjs.com/package/eslint-plugin-yml)

 **Pros**:
 - Integrates with existing linting infrastructure, simplifying setup for users already familiar with ESLint.
 
 **Cons**:
 - May be challenging to customize for Azure-specific syntax; YAML plugins for ESLint lack the depth needed for Azure Pipeline configurations.
 - ESLint was not build for being used as a parser, thus there will be many limitations and shortcomings.
