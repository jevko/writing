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

It matches the same strings as the low-level grammar, except that it produces parse trees which have useful structure.

## Getting from the low level to the high level grammar

To get from the low-level grammar to the high-level one, first we extract the **`Escape`**, and **`Char`** rules from `Jevko`:

```abnf
Jevko = *("[" Jevko "]" / Escape / Char)
Escape = "`" ("`" / "[" / "]")
Char = %x0-5a / %x5c / %x5e-5f / %x61-10ffff
```

`Escape` is to make the brackets `[` and `]` function as part of `Text`. For this we use a special escape character `` ` `` which therefore needs to be escaped as well.

`Char` means any Unicode character except the three special characters: `` "`" / "[" / "]" ``.

We want to cluster consecutive `Char`s and `Escape`s together to form **`Text`**

```abnf
Text = *(Escape / Char)
```

However if we simply substitute `Escape / Char` with `Text`:

```abnf
Jevko = *("[" Jevko "]" / Text)
```

our grammar becomes ambiguous, unless we stipulate that the `Text` rule is greedy.

There are two ways to remove the ambiguity:

```abnf
Jevko = Text *("[" Jevko "]" Text)
```

or:

```abnf
Jevko = *(Text "[" Jevko "]") Text
```

The second way produces parse trees which are more convenient to process in most contexts, so we pick it and continue.

Now we extract the parenthesized part of the `Jevko` rule into the **`Subjevko`** rule:

```abnf
Jevko = *Subjevko Text
Subjevko = Text "[" Jevko "]"
```

next we alias `Text` in `Subjevko` to **`Prefix`**:

```abnf
Subjevko = Prefix "[" Jevko "]"
Prefix = Text
```

and we alias `Text` in the `Jevko` to **`Suffix`**:

```abnf
Jevko = *Subjevko Suffix
Suffix = Text
```

finally we alias `*Subjevko` to **`Subjevkos`**:

```
Jevko = Subjevkos Suffix
Subjevkos = *Subjevko
```

arriving at the final high-level grammar:

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

***

© 2022 Darius J Chuck