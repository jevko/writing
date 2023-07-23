---
title: "Alternative useful grammar for Jevko"
---

*This is based on an unpublished article I wrote 2022-01-23 titled "Many ways to skin a cat" in which I tried to describe various grammars that match the same strings as the official Jevko grammar*

The standard Jevko grammar is defined something like this (ABNF):

```abnf
Jevko = *Subjevko Suffix
Subjevko = Prefix "[" Jevko "]"
```

(consult the [spec](https://jevko.org/spec.html) for details)

This produces Subjevkos which are pairs of Prefix + Jevko.

A Jevko in turn is a sequence of Subjevkos paired with a Suffix.

This grammar may be called "one suffix, many prefixes" to contrast it with the alternative I want to show here.

The alternative definition is this:

```abnf
Jevko = Prefix *Subjevko 
Subjevko = "[" Jevko "]" Suffix
```

This matches the same strings, but looks at them thru a different lens.

Here a Jevko is a Prefix + list of Subjevkos and a Subjevko is a pair of Jevko + Suffix.

This is generally less useful than the standard grammar, which models name-value structures (which are ubiquitous) very well. However it does come in handy sometimes, i.e. when value-name better fits our use case.

There are also other more or less interesting grammars that match the same strings, but that's it for this article.
