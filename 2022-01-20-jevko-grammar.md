# The low and high level Jevko grammars

The simplest grammar able to match [Jevko](https://jevko.org) can fit into one line of [ABNF](https://en.wikipedia.org/wiki/Augmented_Backus-Naur_form):

```abnf
Jevko = *("[" Jevko "]" / "`" ("`" / "[" / "]") / %x0-5a / %x5c / %x5e-5f / %x61-10ffff)
```

This **low-level grammar** is enough to build a Jevko validator. It may also be useful for building low-level or streaming parsers which signal parse events without building a parse tree, instead optionally delegating this work to higher levels.

To implement a higher-level parser which does construct useful parse trees, the following **high-level grammar** is more suitable:

```abnf
; basic structures
Jevko = Subjevkos Suffix
Subjevko = Prefix "[" Jevko "]"

; aliases
Subjevkos = *Subjevko
Suffix = Text
Prefix = Text

; text
Text = *(Escape / Char)
Escape = "`" ("`" / "[" / "]")
; Char is any Unicode character except the three special characters: "`" / "[" / "]"
Char = %x0-5a / %x5c / %x5e-5f / %x61-10ffff
```

It matches the same strings as the low-level grammar, except that it produces useful parse trees.

## Getting from the low level to the high level grammar

To get from the low-level grammar to the high-level one, first we fold it into a clearer form by extracting the `Text` rule:

```abnf
Jevko = *("[" Jevko "]" / Text)
Text = *("`" ("`" / "[" / "]") / %x0-5a / %x5c / %x5e-5f / %x61-10ffff)
```

This grammar is however only unambiguous if the `Text` rule is greedy.

There are two ways to remove the ambiguity:

```abnf
Jevko = Text *("[" Jevko "]" Text)
```

or:

```abnf
Jevko = *(Text "[" Jevko "]") Text
```

The second way produces parse trees which are more convenient to process in most contexts, so it is be used as a basis for the high-level grammar which is built from it as follows.

First we extract the parenthesized part of the `Jevko` rule into the **`Subjevko`** rule:

```abnf
Jevko = *Subjevko Text
Subjevko = Text "[" Jevko "]"
```

next we alias `Text` in the `Jevko` rule to **`Suffix`**:

```abnf
Jevko = *Subjevko Suffix
Suffix = Text
```

and we alias `Text` in `Subjevko` to **`Prefix`**:

```abnf
Subjevko = Prefix "[" Jevko "]"
Prefix = Text
```

arriving at a grammar which looks like this:

```abnf
Jevko = *Subjevko Suffix
Suffix = Text
Subjevko = Prefix "[" Jevko "]"
Prefix = Text
Text = *("`" ("`" / "[" / "]") / %x0-5a / %x5c / %x5e-5f / %x61-10ffff)
```

From there we extract the **`Escape`** rule from `Text`:

```abnf
Text = *(Escape / %x0-5a / %x5c / %x5e-5f / %x61-10ffff)
Escape = "`" ("`" / "[" / "]")
```

then we extract the **`Char`** rule, also from `Text`:

```abnf
Text = *(Escape / Char)
Char = %x0-5a / %x5c / %x5e-5f / %x61-10ffff
```

`Char` then means any Unicode character except the three special characters: `` `[] ``.

This way we arrive at the final grammar:

```abnf
; basic structures
Jevko = Subjevkos Suffix
Subjevko = Prefix "[" Jevko "]"

; aliases
Subjevkos = *Subjevko
Suffix = Text
Prefix = Text

; text
Text = *(Escape / Char)
Escape = "`" ("`" / "[" / "]")
; Char is any Unicode character except the three special characters: "`" / "[" / "]"
Char = %x0-5a / %x5c / %x5e-5f / %x61-10ffff
```