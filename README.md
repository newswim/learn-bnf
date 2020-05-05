# Bakus-Naur Form


BNF lets you write a grammar.

A grammar is a set of rules, also known as "production rules".

These rules determine which language the grammar recognizes.

Example of a rule:

```
<digit> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
```

This rule is called, "digit", although it could have been called anything.

The patterns following the `::=` are the patterns that this rule recognizes.

When patterns are joined with a `|`, this means the rule will recognize either one, in other words, `|` means "or".

A single rule can constitute a language.

We might say that we have just specified the grammer for the "language of single digits".

A language can be recognized by more than one grammar.

Here is another grammar that recognizes the single digit language.

```
<hi-digit> ::= "5" | "6" | "7" | "8" | "9"
<lo-digit> ::= "0" | "1" | "2" | "3" | "4"
<digit>    ::= <hi-digit> | <lo-digit>
```

These two grammars describe the *exact* same language.

It is the following language:

```
L = { "0", "1", "2", "3", "4", "5", "6", "7", "8", "9" }
```

We will now construct the grammar for the language of simple arithmetic expressions.

These will include, for example: `17*3+26`

Here's the grammar:

```raw
<expression> ::= <number> | <number> <operator> <expression>

<number> ::= <digit> | <leading-digit> <digits>

<digits> ::= <digit> | <digit> <digits>

<operator> ::= "+" | "*"

<digit> ::= "0" | <leading-digit>

<leading-digit>  ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
```

When a rule has two forms on the right, separated by a space, this represents concatenation.

For example, `<ten> ::= "1" "0"`

## A Recursive Descent Parser

```c
int digits (char* input) {
 if (digit(input) && input[1] == 0) {
    return 1;
  } else {
    return digit(input) && digits(input + 1); 
  }
}

int digit(char* input) {
  switch (input[0] {
    case '0':
      return 1;
    default:
      return leading_digit(input);
  }
}

int leading_digit(char* input) {
  switch (input[0]) {
    case '1':
      return 1;
    case '2':
      return 1;
    case '3':
      return 1;
    case '4':
      return 1;
    case '5':
      return 1;
    case '6':
      return 1;
    case '7':
      return 1;
    case '8':
      return 1;
    case '9':
      return 1;
    default:
      return 0;
  }
}

```

```raw
<expression> ::= <number>
               | <number> <operator> <expression>
               | <lparen> <number> <operator> <expression> <rparen>

<number> ::= <digit> | <leading-digit> <digits>

<digits> ::= <digit> | <digit> <digits>

<operator> ::= "+" | "*"

<digit> ::= "0" | <leading-digit>

<leading-digit>  ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

<lparen> ::= "("

<rparen> ::= ")"

```

This language is context-free, whereas the earlier language was simply regular.


# Resources

- https://baturin.org/tools/bnfgen
- https://tomcopeland.blogs.com/EcmaScript.html
- http://www.ccs.neu.edu/home/dherman/javascript
