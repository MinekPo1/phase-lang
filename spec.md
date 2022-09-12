# Phase spec

The key words "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL NOT**", "**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**NOT RECOMMENDED**", "**MAY**", and "**OPTIONAL**" in this document are to be interpreted as described in [BCP 14](https://www.rfc-editor.org/bcp/bcp14) [[RFC2119](https://www.rfc-editor.org/rfc/rfc2119)] [[RFC8174](https://www.rfc-editor.org/rfc/rfc8174)] when, and only when, they appear in all capitals, as shown here.

This document has not yet been finalised, thus change **MAY** occur and contend missing from this document **SHOULD** be expected.

## Basic syntax

- instructions **MUST** placed on separate lines or split with semicolons
- blocks of code are placed within curly brackets
- instructions **SHALL NOT** be placed outside [tasks](#tasks) or [functions](#functions)
- All literals valid as mlog literals are valid

### Tasks

Tasks are the basic building blocks of a phase lang program. They **MUST** started by other tasks or started implicitly, which happens for the task named `main`.

- tasks **MUST** be defined using the following construct:
  - a `task` keyword
  - the name of the task
  - a block of instructions

### Functions

Functions **SHOULD** be used to avoid repeating the same code or to allow an easier interface for other developers.
See [function calls](#function-calls) for a description on how functions are called.

- functions **MUST** be defined using the following construct:
  - an optional `inline` keyword
  - a `func` keyword
  - the name of the function
  - a pair of parenthesises, which **MAY** contain [arguments](#arguments)
  - an optional arrow (`->`) followed by the return type
  - a block of instructions

#### Arguments

Arguments **SHOULD** be used to pass in values into the function or to influence its behaviour.

- arguments are defined by placing the argument name, which **MAY** be followed by a colon and type
- arguments **MUST** be split with commas
- an argument name **MAY** be prefixed with a exclamation mark (`!`), which turns it into a bang argument. Bang arguments **MUST NOT** have a type declaration

### Statements

#### Function Calls

- a function call **MUST** be constructed of, in order:
  - the name of the function and the optional access path before it
  - parenthesises, which:
    - **MUST** contain one value per each non bang argument defined in the function definition
    - **MAY** contain any number of bang arguments defined in the function definition
    - arguments **MUST** be split with commas
    - bang arguments **MUST NOT** be repeated

#### Flow control

##### if statements

- if statements **MUST** consist of the following construct:
  - a `if` keyword
  - the condition, which **MAY** be wrapped in parenthesises
  - a block of instructions
- the block inside will and execute if and only if the condition is evaluated as truthful
- an if statement **MAY** be followed by a `else` keyword followed by another `if` statement or a block of instructions
- the if statement or block of instructions placed after the `else` keyword, along with any chained `else` keywords will not be executed if the condition is evaluated as truthful

##### while loops

- while loops **MUST** consist of the following construct:
  - a `while` keyword
  - the condition, which **MAY** be wrapped in parenthesises
  - a block of instructions
- the block inside will execute until and if the condition is evaluated as truthful

##### for loops

- for loops **MUST** consist of the following construct:
  - a `for` keyword
  - the name of the iteration variable
  - a `in` keyword
  - two values in parenthesises split by a comma:
    - the first being the starting value
    - the second being the ending value
  - a block of instructions
- the block of instructions will be executed with the iteration variable set to each value between the starting and ending value **inclusive**

### Naming

- names **MUST** contain:
  - alpha-numeric characters
  - underscores
  - question marks
- names **MUST NOT** repeat, in other words **MUST** be unique, within a code base
