# Some semantic analogies to syntactic constructs in Jevko

The [Standard Jevko Grammar is specified](https://github.com/jevko/specifications/blob/master/draft-standard-grammar.md) in a way which is amenable to representation in terms of common programming language structures.

In particular:

```abnf
Jevko = *Subjevko Suffix
```

says that a `Jevko` is a sequence of zero or more `Subjevko`s followed by a `Suffix`.

Syntactic sequences usually convey collections of some sort.

A particular kind of collection is a collection of key-value *pairs*. Which brings us to the definition of `Subjevko`:

```abnf
Subjevko = Prefix "[" Jevko "]"
```

A `Subjevko` is a `Prefix` followed by an `[`, followed by a `Jevko`, followed by a `]`.

If we ignore the delimiting brackets, a Subjevko is then a Prefix-Jevko *pair*. A mapping from Subjevkos into key-value pairs is straightforward.

An example:

```
key1 [value1]
key2 [value2]
```

That's a Jevko made of 2 Subjevkos. That is analogous to a collection of 2 key-value pairs. From here, translating a Jevko parse tree to a proper collection is trivial.

Another basic kind of collection is an ordered collection of values. Which could be seen as a special case of a collection of key-value pairs, where keys are implied by the syntactic order of values.

This can be represented with Subjevkos with empty Prefixes:

```
[value1]
[value2]
```

would represent an orederd collection of 2 simple values.
