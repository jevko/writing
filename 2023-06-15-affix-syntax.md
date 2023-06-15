Capturing an idea with minimal involvement from the inner editor.

# Affix syntax

I want to shed light on some syntactic constructs in programming languages that work similarly to affixes.

## Prefixes

Decorators, tags, however you call them.

It's something you prepend to something else, usually to alter the meaning or otherwise change that. Example:

```
@decorator
fn my_function() ...
```

That would alter `my_function`. Another one:

```
#tag 1234
```

That would alter the value of `1234`. E.g. we could do:

```
#uint8 123
```

To tag `123` with a specific data type. Another one:

```
--- !!set
? red
? green
? blue
```

`!!set` -- that's YAML syntax that tags the value that follows as a set.

The important thing about these prefixes is that they end before the value they apply to begins. E.g.:

```
decorator(fn my_function()...)
```

could semantically be similar or the same as `@decorator` but this syntax requires that the value that the decorator is applied to is wrapped in parens. Applying multiple decorators like that would look like:

```
deco1(deco2(deco3(value)))
```

Whereas with the prefix syntax it would be:

```
@deco1 @deco2 @deco3 value
```

Which is much more pleasant to a human processor.

## Suffixes

Same idea can be applied in suffix form:

```
value | decorator
value_decorator
value |> decorator
```

The value goes first, then one or more decorators.

This order works better for some expressions.

E.g. units:

```
100 | characters_per_minute
```
