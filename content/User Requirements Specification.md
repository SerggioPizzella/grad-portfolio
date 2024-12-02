For the purposes of diagnostics, we recognise 4 levels as indicated by the [LSP Specification](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#diagnosticSeverity), namely:
- `Error`
- `Warning`
- `Information`
- `Hint`

# Rules
## Compile-Time Expressions
### Possible Problems

| Name                               | description                                                    | Level   |
| ---------------------------------- | -------------------------------------------------------------- | ------- |
| **Missing Closing Curly Brackets** | Enforce closing `}}` in the same line as `${{.                 | `Error` |
| **Balanced brackets**              | Enforce all opening parenthesis have a closing parenthesis.    | `Error` |
| **Undefined Variables**            | Disallow variables undefined variables.                        | `Error` |
| **Type Mismatches**<br>            | Disallow expression having invalid type.                       | `Error` |
| **Invalid Function**               | Disallow calling undefined functions                           | `Error` |
| **Invalid Function Arguments**     | Enforce correct numbers of arguments are passed to a function. | `Error` |
| **Arguments Separation**           | Enforce arguments in a function are separated with a comma.    | `Error` |
- [x] Setup Core Project structure
	- [x] Put all the projects in the same repo
	- [x] Make language service lib
	- [x] Make language server exec
- [x] Find LSP lib.
- [ ] Make localhost input in extension.
- [ ] Deserialize the YAML to objects I can work with.
- [ ] Parse out the directives.
- [ ] Implement AST traversal.
- [ ] Implement basic error system.
- [ ] Push error to IDE..
- [ ] Push errors from parser to collection.
- [ ] Implement type checking.
- [ ] Implement Function validation.
	- [ ] Make collection of valid functions.
- [ ] Implement Function Arguments Validation.
- [ ] Collect diagnostics and display them.

Using MSTest, cause that's what the guidelines say. [Unit testing | Guidance Framework](https://guidance.infosupport.com/04-technology-guidance/02-application-development/03-frameworks/01-microsoft/01-dotnetcore/unit-testing#test-framework)
