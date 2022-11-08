# The Twelve Programming Language

## About

Twelve is an easy to use C-like programming language based on excellent [Writing An Interpreter In Go](https://interpreterbook.com) book.

### Main goal of the repository

- To have fun 🐒
- Writing a tree-walking interpreter in go
- Learn by building and practice go

### Features

- Integers, booleans, strings, arrays, hash maps
- A REPL
- Arithmetic expressions
- Let statements
- First-class and higher-order functions
- Built-in functions
- Recursion
- Closures

### Major Parts

- the lexer
- the parser
- the Abstract Syntax Tree (AST)
- the internal object system
- the evaluator

---

## CHAPTER 1 - LEXING

### 1.1 Lexical Analysis

What we need to do is represent our source code in other forms that **are** easier to work with. We’re going to change the representation of our source code two times before we evaluate it:

```
+-------------+     +--------+     +----------------------+
| Source Code | --> | Tokens | --> | Abstract Syntax Tree |
+-------------+     +--------+     +----------------------+
```

The first transformation, from source code to tokens, is called “lexical analysis”, or “lexing” for
short. It’s done by a lexer (also called tokenizer or scanner – some use one word or the other
to denote subtle differences in behaviour).

Tokens themselves are small, easily categorizable data structures that are then fed to the parser,
which does the second transformation and turns the tokens into an “Abstract Syntax Tree”.

Here's an example. This is the input one gives a lexer:

```
"let answer = 41 + 1;"
```

And what comes out of the lexer looks kinda like this:

```
[
  LET,
  IDENTIFIER('answer'),
  EQUAL_SIGN,
  INTEGER(41),
  PLUS_SIGN,
  INTEGER(1),
  SEMICOLON,
]
```

All of these tokens have the original source code representation attached.

Whitespace only acts as a separator for other tokens. It doesn’t matter if we type this:

```
let x = 5;
```

Or if we type this:

```
let   x   =   5   ;
```

In other languages, like Python, the length of whitespace is significant.
