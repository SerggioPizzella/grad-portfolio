---
date: 2024-12-02
title: Software Architecture
---

![[c1.svg]]![[c2.svg]]![[c3.svg]]
![[diagnostics flow.excalidraw.svg]]
![[c4 - language service.svg]]
![[c4 - language service - extended.svg]]
## Generating the diagrams
- Generate using `npx tsuml2 --glob "./src/**/*.ts" --outMermaidDsl  "./docs/static/mermaid_diagram.dsl"`
- Grab the nodes with [live editor](https://mermaid-js.github.io/mermaid-live-editor).
- Import into Excalidraw.
	- Set background to light blue.
	- Set Sloppiness to architect.
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
| **Missing Closing Curly Brackets** | Enforce closing `}}` in the same line as `${{`.                | `Error` |
| **Balanced brackets**              | Enforce all opening parenthesis have a closing parenthesis.    | `Error` |
| **Undefined Variables**            | Disallow variables undefined variables.                        | `Error` |
| **Type Mismatches**<br>            | Disallow expression having invalid type.                       | `Error` |
| **Invalid Function**               | Disallow calling undefined functions                           | `Error` |
| **Invalid Function Arguments**     | Enforce correct numbers of arguments are passed to a function. | `Error` |
| **Arguments Separation**           | Enforce arguments in a function are separated with a comma.    | `Error` |
