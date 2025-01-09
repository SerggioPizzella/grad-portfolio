---
date: 2024-12-02
title: Software Architecture
---
This page describes the architecture chosen for the project and the decisions that lead to it. We will use the [C4 model](https://c4model.com/) to capture the design of the application. This because it is a recognized form of documentation per the [Internal Guidance Framework](https://guidance.infosupport.com/03-architecture-guidance/51-architecture-definitions/architecture-building-blocks) and it is the model we have most experience with. 

> We forgo the use of the term `Containers` as a block type, as it can cause confusion, per the guidance framework. Instead we opt to be more descriptive where applicable and use the opportunity to describe the technology.

The primary guiding factors when designing the system are the non-functional requirements that were agreed upon. At each step I will state which requirement and research lead to the result.

## Overview C1
This diagram depicts the most global view of the application. We only have one kind of user, the developer. Developers all have their own development environment, a text editor. The primary editor at Info Support is Visual Studio Code, thus it will be the primary focus of the following diagrams. 

As to follow our [[User Requirements Specification#User-Friendliness |User Friendliness]] requirements, our solution will not provide a separate development environment, but will instead aim to integrate with the users'.

Users will interact with their editor of choice, which will in turn interact with our solution. The users pipeline can have references to external files, these files could be in the same repository or part of an external repository, therefore our solution must communicate with the file system and with remote repositories. 
![[c1.svg]]
## C2
![[c2.svg]]
![[c3.svg]]
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
