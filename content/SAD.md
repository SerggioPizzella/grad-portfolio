---
date: 2024-12-02
title: Software Architecture
---
![[c1.svg|]]![[c2.svg]]![[c3.svg]]

# Testing
Using MS Test, cause that's what the guidelines say. [Unit testing | Guidance Framework](https://guidance.infosupport.com/04-technology-guidance/02-application-development/03-frameworks/01-microsoft/01-dotnetcore/unit-testing#test-framework)

# Rules
For the purposes of diagnostics, we recognise 4 levels as indicated by the [LSP Specification](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#diagnosticSeverity), namely:
- `Error`
- `Warning`
- `Information`
- `Hint`
## Compile-Time Expressions

| Name                               | description                                                    | Level   |
| ---------------------------------- | -------------------------------------------------------------- | ------- |
| **Missing Closing Curly Brackets** | Enforce closing `}}` in the same line as `${{.                 | `Error` |
| **Balanced brackets**              | Enforce all opening parenthesis have a closing parenthesis.    | `Error` |
| **Undefined Variables**            | Disallow variables undefined variables.                        | `Error` |
| **Type Mismatches**<br>            | Disallow expression having invalid type.                       | `Error` |
| **Invalid Function**               | Disallow calling undefined functions                           | `Error` |
| **Invalid Function Arguments**     | Enforce correct numbers of arguments are passed to a function. | `Error` |
| **Arguments Separation**           | Enforce arguments in a function are separated with a comma.    | `Error` |
