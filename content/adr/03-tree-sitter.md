---
date: 2024-11-13
title: 03 Tree-sitter
---
- Status: proposed
- Deciders: Serggio Pizzella, Luuk Horsman.
- Informed: Erik Schriek.
## Context and Problem Statement
With the decision to build on top of an existing YAML parser, [[02-create-a-custom-parser]], the next step is to select the most suitable parser generator for the azure-specific contents.
## Decision Drivers
1. **Ease of implementation**: Must not require deep expertise to use effectively.
2. **Language and Tooling Integration**: Should integrate well with multiple languages and offer strong support for debugging, allowing flexibility in development choices and efficient troubleshooting.
3. **Documentation and Tutorials**: Comprehensive documentation and tutorials should be available to aid with setup, usage, and customization.
1. **Performance**: Must provide efficient parsing suited for real-time feedback during editing.

## Considered Options
1. [Tree-sitter](https://tree-sitter.github.io/tree-sitter/)
1. [ANTLR](https://www.antlr.org/)

## Decision Outcome
**Chosen option: Tree-sitter**, because it offers an easier implementation process using JavaScript for grammar, aligns well with the need for real-time feedback, and supports integration with multiple programming languages. While its documentation is slightly less comprehensive than ANTLR, it meets all critical decision drivers, particularly ease of use and performance for real-time editing.

## Consequences
- **Good**: Tree-sitter simplifies grammar creation by being in JavaScript, making it accessible for developers without prior knowledge in ANTLR's DSL. Its design specifically supports real-time feedback, aligning with performance needs.
- **Bad**: Documentation, while extensive, is slightly less detailed than ANTLR's.