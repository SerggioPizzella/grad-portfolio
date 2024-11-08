---
status: proposed
date: 2024-10-23
decision-makers: Serggio Pizzella
consulted: Luuk Horsman
informed: Eric
---

# Custom Parser for Azure Pipelines

## Context and Problem Statement

## Decision Drivers

- Accurate validation for Azure-specific features such as:
    - compile-time expressions.
    - variable scope.
    - template parameters.
    - conditions at all levels.
- The need for real-time feedback to streamline pipeline development.

## Considered Options

- **Azure Pipelines Extension by Microsoft**: Uses the azure-pipelines-language-server, which is a fork of the YAML language server. This tool adds basic support for Azure pipeline files but does not handle deeper semantic validation of variables or compile-time expressions.
- **Mini-Parser for Compile-Time Expressions**: Build a small parser just for handling Azure compile-time expressions within `${{ }}` blocks, but this would require merging the AST from multiple places, leading to complexity and potentially limited flexibility.
- **Fork the YAML Library**: Extend the existing `eemeli/yaml` library used in the Azure Pipelines language server to include custom rules for Azure Pipelines. This could allow for deep integration but would involve significant effort and complexity to maintain.
- **Build a Custom Parser Using a Parser Generator**: Use a parser generator like ANTLR or PyParsing to create a full parser that understands Azure Pipelines' specific syntax, including compile-time expressions, variable scope, and template handling, from the ground up.

## Decision Outcome

**Chosen option**: "Build a custom parser using a parser generator," because this allows full control over the parsing process and provides the flexibility to add Azure-specific validation logic. This approach minimizes complexity compared to forking the YAML parser and provides a cleaner, more maintainable solution than trying to merge mini-parse trees.

### Consequences

- **Good**: Provides deep validation tailored to Azure Pipelines' unique syntax and features.
- **Good**: The custom parser can be extended to support additional Azure Pipelines features or company-specific requirements.
- **Bad**: Requires significant upfront development to implement the parser and its related validation rules, which in turn requires a high level of expertise.

### Confirmation

## Pros and Cons of the Options

### Azure Pipelines Extension by Microsoft

- **Good**: Already exists and integrates with VSCode for basic pipeline file support.
- **Bad**: Does not provide validation for deeper concepts like variable scoping or compile-time expressions, limiting its utility.

### Mini-Parser for Compile-Time Expressions

- **Good**: Requires less development effort upfront, as it only targets compile-time expressions.
- **Bad**: Merging ASTs from multiple occurrences adds complexity, and the approach might not scale well for full pipeline validation.

### Fork the YAML Library

- **Good**: Leverages an existing parser, allowing you to extend Azure-specific logic.
- **Bad**: Involves extensive work to modify and maintain the library, which could become more complex than building a new parser from scratch.

### Build a Custom Parser Using a Parser Generator

- **Good**: Offers full flexibility to define and validate Azure Pipelines syntax, with a single unified AST.
- **Good**: Easier to maintain and extend as new requirements emerge.
- **Bad**: Requires significant initial development effort and expertise in parser generation.

## More Information

