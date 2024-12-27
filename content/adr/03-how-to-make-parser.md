---
date: 2024-11-13
title: 03 Parsing solution
---
- Status: approved.
- Deciders: Serggio Pizzella, Luuk Horsman.
- Informed: Erik Schriek.

---
## Context and Problem Statement
With the decision to build on top of an existing YAML parser, [[02-parsing-strategy]], the next step is to define how we are going to make the parser for the azure-specific contents.

---
## Decision Drivers
1. **Ease of implementation**: Must not require deep expertise to realize effectively.
2. **Tooling Integration**:  Must have strong support for debugging, allowing efficient troubleshooting.
1. **Performance**: Must provide efficient parsing suited for real-time feedback during editing.
3. **Documentation and Tutorials**: Should have comprehensive documentation and tutorials available to aid with setup, usage, and customization.
1. **Language Integration**: Should integrate well with multiple languages, to allow flexibility in development choices.

---
## Considered Options
1. [Tree-sitter](https://tree-sitter.github.io/tree-sitter/)
1. [ANTLR](https://www.antlr.org/)

### Other considered Options
1. [YACC](https://en.wikipedia.org/wiki/Yacc): Dismissed since it's a parser from the 1970, that was replaced by [GNU Bison](https://en.wikipedia.org/wiki/GNU_Bison). It lacks tooling integration features like a CLI to use the parser; generate bindings or test the grammar.
1. [Bison - GNU Project - Free Software Foundation](https://www.gnu.org/software/bison/): Dismissed as although it has greater capabilities than YACC, it has the same poor ergonomics and lack of tooling integration.
2. From scratch: Dismissed for the same reasons as it was dismissed in [[02-parsing-strategy#Creating a Parser from Scratch.]].

---
## Decision Outcome
**Chosen option: Tree-sitter**, because it offers an easier implementation process using JavaScript for grammar, aligns well with the need for real-time feedback, and supports integration with multiple programming languages. While its documentation is slightly less comprehensive than ANTLR, it meets all critical decision drivers, particularly ease of implementation, tooling integration, and performance for real-time editing.

ANTRL posses an extensive amount of [documentation](https://github.com/antlr/antlr4/blob/master/doc/index.md). This includes: books, articles and videos. Which can all aid in it's use. 
A place where the lack of documentation for Tree-sitter can be felt is when it comes to better error diagnostics. As can be seen from this [PR](https://github.com/tree-sitter/tree-sitter/pull/2324) which enables the functionality, it is yet to be mentioned anywhere in the documentation. This makes it hard to use, as the only way to understand the functionality, is by going trough the tests and source code. Additionally the third biggest contributor has left the project. 
### Consequences
- **Good**: Tree-sitter simplifies grammar creation by being in JavaScript, making it the more accessible option for developers without prior knowledge. Its design specifically supports real-time feedback, aligning with performance needs.
- **Bad**: Documentation, while extensive, is slightly less detailed than ANTLR's.

---
## Grammars
We can implement a simple Reverse Polish Notation calculator parser, to compare the grammars. The parser should accept inputs like:
- 4 9 +
- 3 7 + 3 4 5 *+-
- 3 7 + 3 4 5 * + - n
- 5 6 / 4 n +
- 3 4 ^
### Bison [^1][^2]
```c grammer.j
%{ // Prologue
  #include <stdio.h>
  #include <math.h>
  int yylex (void);
  void yyerror (char const *);
%}

// Bison declarations
%define api.value.type {double}
%token NUM

//% % // Grammar rules
// Match none or more lines
input:
  %empty
| input line
;

// a line can be empty or an expression followed by a new line.
line:
  '\n'
| exp '\n'      { printf ("%.10g\n", $1); }
;

// Expression can end with either +, -, *, / or 'n' for negating the number.
exp:
  NUM
| exp exp '+'   { $$ = $1 + $2;      }
| exp exp '-'   { $$ = $1 - $2;      }
| exp exp '*'   { $$ = $1 * $2;      }
| exp exp '/'   { $$ = $1 / $2;      }
| exp exp '^'   { $$ = pow ($1, $2); }  /* Exponentiation */
| exp 'n'       { $$ = -$1;          }  /* Unary minus   */
;
//% %

// Epilogue - any C code.
```
[^1]: This example can be found [here](https://www.gnu.org/software/bison/manual/bison.html#RPN-Calc).
[^2]: The `% %` are commented out and spaced apart as they interfere with the code being displayed.

It contains a non-trivial amount of Domain Specific Syntax. Note how the we need to import header files and define tokens and types; and how the `| input line` rule, obscurely allows for multiple lines by defining `input` recursively.

### Tree-sitter
```js grammmar.js
module.exports = grammar({
  name: 'reverse_polish_notation',

  rules: {
    input: $ => repeat($._line),

    _line: $ => choice(
      '\n',                      // Empty line
      seq($.expression, '\n')
    ),

    expression: $ => choice(
      $.number,
      seq($.expression, $.expression, '+'),
      seq($.expression, $.expression, '-'),
      seq($.expression, $.expression, '*'),
      seq($.expression, $.expression, '/'),
      seq($.expression, $.expression, '^'),  // Exponentiation
      seq($.expression, 'n')                 // Unary minus
    ),

    number: $ => /[0-9]+(\.[0-9]+)?/, // Matches integers and decimals
  }
});
```

The Tree-sitter code, is more verbose, as it explicitly mentions which items are repeated and which are a sequence.  From the perspective of someone that is not familiar with any grammar, this makes it easier to understand and work with.

### ANTLR
```js
grammar RPN;

// Parser Rules
input: (line NEWLINE)* EOF;

line: NEWLINE       // Empty line
    | expression NEWLINE;

expression: NUM                       
          | expression expression '+'
          | expression expression '-'
          | expression expression '*'
          | expression expression '/' 
          | expression expression '^'      # exponentiation
          | expression 'n'                 # unaryMinus
          ;

// Lexer Rules
NUM: [0-9]+ ('.' [0-9]+)?; 
NEWLINE: '\r'? '\n';        // Matches Unix and Windows newlines
WS: [ \t]+ -> skip;         // Skip whitespace
```

The ANTLR grammar is quite similar to bison, without the special sections and semi-embedded C code. It looks rather better/simpler than bison, albeit more proprietary than Tree-sitter.

