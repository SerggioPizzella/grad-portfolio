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

---
## C2
In order to meet **NFR-2: IDE Independence**, our design must be able to integrate with multiple editors. Generating separate solutions for each editor would be unmaintainable. Instead, we leverage the Language Server Protocol (LSP), an industry standard developed by Microsoft, supported by most modern editors, including VS Code, Neovim, and Visual Studio. LSP enables an editor to communicate with a centralized service providing language-specific features. Therefore, our solution will be a language server.[^1][^2] This inadvertently also complies with our [[User Requirements Specification#Operation |Operational]] requirements. 

[^1]: [Official page for Language Server Protocol](https://microsoft.github.io/language-server-protocol/)
[^2]: [LSP Explained (in 5 Minutes)](https://www.youtube.com/watch?v=LaS32vctfOY)

This approach does mean that our solution will not be able to communicate with a key editor: the Azure DevOps in-browser editor. Developers sometimes use this editor for debugging, as noted from the [[Survey#Follow-Up Interviews|Interviews]], since it provides additional diagnostics. However, due to the technical complexity and differing focus of a in-browser cloud-based editor, support for it has been ruled out as a priority. This compromise is deemed acceptable given the project's scope and objectives.

The primary editor at Info Support is Visual Studio Code (VS Code), and it will serve as our primary focus. The LSP integration in VS Code is facilitated by an extension, which acts as a bridge between the language server and the editor. This extension merely initializes the connection and can be published and installed easily, satisfying **NFR-1: Seamless Integration**.

The architecture is designed to accommodate additional editors and features with minimal changes, ensuring long-term flexibility. The following diagram illustrates this setup.
![[c2.svg]]

---
## C3 Language Server
Here we will take a closer look at the Language Server system. It is comprised of three primary packages:

- **Language Server (I/O Layer):** Acts as a thin interface implementing the Language Server Protocol (LSP), handling communication between the editor and the underlying logic.
- **Language Service:** Contains the core functionality and logic for processing, analysing, and providing language features.
- **Tree-sitter Parser:** A specialized parser designed to handle the expressions within Azure Pipelines YAML files.

### Parser
Azure pipelines allows the user to programmatically define their pipelines, by means of using compile-time and runtime expressions. The decision to modularize the **Parser** stems from a deliberate architectural choice to keep parsing responsibilities separate from the main service. This separation:

- Ensures the **Language Service** focuses on delivering language features without being burdened by parsing complexities.
- Enables the parser to evolve independently, accommodating updates or changes in Azure Pipelines’ syntax.

Parsing expressions involves generating Abstract Syntax Trees (ASTs) to facilitate reasoning and diagnostics. As this functionality goes beyond the scope of the main service, it has been designated as an **architectural boundary** and implemented as its own package.

### Inspiration
This design draws inspiration from Microsoft's own [Azure Pipelines Language Server](https://github.com/microsoft/azure-pipelines-language-server/tree/main?tab=readme-ov-file#developer-support), which separates the I/O server package from the service package containing the main functionality. As highlighted in this [video](https://youtu.be/p0Vlz66AFNw?feature=shared&t=187), a key advantage of this architecture is **code reuse**, enabling greater flexibility and scalability. 

By adopting this modular approach, the system can later support additional interfaces, such as:
- **Software SDK:** To integrate the functionality programmatically.
- **CLI Tool:** For automated error-checking in CI environments.

These potential extensions are depicted in **Pink**. 
![[c3.svg]]

## C4 Language Service
Here we take an in-dept look at the Language service package.

The package is designed for simplicity and efficiency, featuring a single entry point: the `LanguageService`. This entry point serves as the central hub, providing all functionality through a set of well-defined interfaces. The Language Server Protocol (LSP) defines numerous language features, and to maintain a clear separation of concerns, we considered using a distinct class for each feature. However, given the complexity of Azure Pipelines, where multiple LSP features intersect with various pipeline-specific functionalities, we adopted a more granular approach.

For each language feature defined by the LSP, such as `textDocument/completion`, we created a dedicated interface. This interface is then implemented by separate classes, each addressing a specific aspect of Azure Pipelines, such as template parameter completion, variable completion, or key completion. This modular structure ensures that each implementing class focuses on a single concern, making the system more maintainable and extensible.

The `LanguageService` acts as the orchestrator, combining the results from all these specialized classes into a cohesive response. This approach not only adheres to the principle of separation of concerns but also ensures that the package remains flexible and scalable.
![[c4 - language service.svg]]

### C4 Language Service - Extensions
Here we demonstrate how the architecture allows for further expansion.

In purple we depict how additional features could be added using existing interfaces, alongside existing features.

![[c4 - language service - extended.svg]]
### Generating the diagrams
In order to streamline C4 level diagram generation we use `tsuml2` to generate a complete diagram of the application; then we use an editor to select and extract the nodes we care about; and lastly import them into Excalidraw, where all diagrams are made.

- Generate using `npx tsuml2 --glob "./src/**/*.ts" --outMermaidDsl  "./docs/static/mermaid_diagram.dsl"` or `npm run diagrams`
- Grab the nodes with [live editor](https://mermaid-js.github.io/mermaid-live-editor).
- Import into Excalidraw.
	- Set background to light blue.
	- Set Sloppiness to architect.

# Technology
Using MS Test, cause that's what the guidelines say. [Unit testing | Guidance Framework](https://guidance.infosupport.com/04-technology-guidance/02-application-development/03-frameworks/01-microsoft/01-dotnetcore/unit-testing#test-framework)