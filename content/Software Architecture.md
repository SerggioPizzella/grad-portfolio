---
date: 2024-12-02
title: Software Architecture
---
This page describes the architecture chosen for the project and the decisions that lead to it. We will use the [C4 model](https://c4model.com/) to capture the design of the application. This because it is a recognized form of documentation per the [Internal Guidance Framework](https://guidance.infosupport.com/03-architecture-guidance/51-architecture-definitions/architecture-building-blocks) and it is the model we have most experience with. 

> We forgo the use of the term `Containers` as a block type, as it can cause confusion, per the guidance framework. Instead we opt to be more descriptive where applicable and use the opportunity to describe the technology.

The primary guiding factors when designing the system are the non-functional requirements that were agreed upon. At each step I will state which requirement and research lead to the result.

## Overview C1
This diagram represents the highest-level overview of the application, focusing on its interaction with its primary user: the developer. Each developer operates within their own development environment, typically a text editor.

In alignment with our [[User Requirements Specification#User-Friendliness |User Friendliness]] requirements, the solution will integrate seamlessly into the existing development environments of users. Rather than introducing a standalone development environment, our approach emphasizes embedding functionality directly within the tools developers already use. This ensures minimal disruption to their workflows and adherence to **NFR-1: Seamless Integration**.

Developers interact with their editor of choice, which in turn connects to our solution. As Azure Pipelines often include references to external files; located either in the same repository or in external repositories; our architecture must facilitate communication with both local file systems and remote repositories.
![[c1.svg]]
## C2
In order to meet **NFR-2: IDE Independence**, our design must be able to integrate with multiple editors. Generating separate solutions for each editor would be unmaintainable. Instead, we leverage the Language Server Protocol (LSP), an industry standard developed by Microsoft, supported by most modern editors, including VS Code, Neovim, and Visual Studio. LSP enables an editor to communicate with a centralized service providing language-specific features. Therefore, our solution will be a language server.[^1]

[^1]: [Official page for Language Server Protocol](https://microsoft.github.io/language-server-protocol/)

This approach does mean that our solution will not be able to communicate with a key editor: the Azure DevOps in-browser editor. Developers sometimes use this editor for debugging, as noted from the [[Survey#Follow-Up Interviews|Interviews]], since it provides additional diagnostics. However, due to the technical complexity and differing focus of a in-browser cloud-based editor, support for it has been ruled out as a priority. This compromise is deemed acceptable given the project's scope and objectives.
> ==**Confirm if I can say that for real with Luuk.**==

The primary editor at Info Support is Visual Studio Code (VS Code), and it will serve as our primary focus. The LSP integration in VS Code is facilitated by an extension, which acts as a bridge between the language server and the editor. This extension merely initializes the connection and can be published and installed easily, satisfying **NFR-1: Seamless Integration**.

The architecture is designed to accommodate additional editors and features with minimal changes, ensuring long-term flexibility. The following diagram illustrates this setup.
![[c2.svg]]
## C3

![[c3.svg]]
![[diagnostics flow.excalidraw.svg]]
![[c4 - language service.svg]]
![[c4 - language service - extended.svg]]
### Generating the diagrams
In order to streamline C4 level diagram generation we use `tsuml2` to generate a complete diagram of the application; then we use an editor to select and extract the nodes we care about; and lastly import them into Excalidraw, where all diagrams are made.

- Generate using `npx tsuml2 --glob "./src/**/*.ts" --outMermaidDsl  "./docs/static/mermaid_diagram.dsl"` or `npm run diagrams`
- Grab the nodes with [live editor](https://mermaid-js.github.io/mermaid-live-editor).
- Import into Excalidraw.
	- Set background to light blue.
	- Set Sloppiness to architect.