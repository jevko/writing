# Restrictions of JSON numbers

As described previously, there are some practical interoperability issues associated with JSON numbers which can lead to serious bugs ([[1]](https://xtao.org/blog/json-semantics.html), [[2]](https://github.com/xtao-org/loose-blog/blob/35b2b9220dd6f99a3b33628d143a30ffd82f953e/large-numbers-in-json.md), [[3]](https://github.com/xtao-org/writing/blob/c6b2bd614b6868cd81f9df2070a4f5fb7b76e47d/2022-01-07-infinity-nan-json.md)).

One of these issues, i.e. inability to express Infinity and NaN, stems from the extreme restrictiveness of the JSON number grammar.

Let's see what other common number encodings are also restricted by it and how to alleviate that.

## JSON number definition

[ECMA-404](https://www.ecma-international.org/wp-content/uploads/ECMA-404_2nd_edition_december_2017.pdf) defines a number strictly as:

> a sequence of decimal digits with no superfluous leading zero

An equivalent definition is provided by [RFC8259](https://datatracker.ietf.org/doc/html/rfc8259#section-6):

> A number is represented in base 10 using decimal digits.

This definition is however preceded by the following statement:

> The representation of numbers is similar to that used in most programming languages. 

which is somewhat similar to the description used at [JSON.org](https://www.json.org):

> A number is very much like a C or Java number, except that the octal and hexadecimal formats are not used.

Framing the definintion like this is akin to saying that a set of sequences of lowercase letters is very much like the set of C or Java identifiers, except that it does not include a significant subset of identifiers.

Let's examine some common numeric values and formats used in programming languages like C, Java, or JavaScript which are impossible to represent in JSON.

## Infinity and NaN

Whether flawless or not, the IEEE754 standard for floating-point numbers is currently the most interoperable.

Most programming languages, including C or Java support it.

JSON numbers however are explicitly incompatible with it, by [excluding any representation for the standard special values Infinity and NaN](https://github.com/xtao-org/writing/blob/c6b2bd614b6868cd81f9df2070a4f5fb7b76e47d/2022-01-07-infinity-nan-json.md).

## Nondecimal number formats

Most programming languages have syntax for representing nondecimal numbers, particularly any subset of hexadecimal, binary, octal. For example JavaScript can represent all of these.

The support for nondecimal bases is included in programming languages because in certain contexts it is more human-readable to represent numbers this way.

JSON explicitly excludes them.

## Numeric separators

[An old](http://archive.adaic.com/standards/83lrm/html/lrm-02-04.html#2.4) readability-improving facility which is being adopted by more and more languages, is the [numeric separator syntax](https://www.rosettacode.org/wiki/Numeric_separator_syntax).

[Java supported it since 2011 (Java SE 7)](https://docs.oracle.com/javase/7/docs/technotes/guides/language/underscores-literals.html). [JavaScript introduced it in ES2021](https://github.com/tc39/proposal-numeric-separator). It is even included in an [upcoming C standard revision](https://en.wikipedia.org/wiki/C2x)

JSON, being derived from JavaScript's syntax as it was around the year 2000, naturally does not include this facility.

## Solution

What then to do if we need to use any of the above in JSON?

The answer is always the same for every data type and format not built into JSON: use strings. And [inform your interchange parties how to parse them correctly](https://github.com/xtao-org/writing/blob/main/2022-01-07-meaningful-json.md).

## Appendix: number grammars vs Infinity and NaN

The lack of Infinity or NaN in JavaScript is [sometimes justified](https://stackoverflow.com/a/1424034/7379821) by observing the fact that these values are not part of JavaScript number grammar and/or that they can be altered. This is not a valid justification.

If it were valid, then by the same logic, JSON should forbid the leading minus sign, effectively forbiding negative numbers. Why? Because the [JavaScript number grammar](https://tc39.es/ecma262/#prod-NumericLiteral) does not include the minus sign outside of the `ExponentPart`. Instead, it's an operator, defined separately.

From this point of view JSON number grammar is not a subset of JavaScript number grammar. Additionally, the result of the operator's application can be altered by a custom implementation of the `valueOf` method.

The fact that JavaScript allows doing dangerous things like these is an issue with JavaScript, and should not be relevant from the perspective of JSON which is supposed to be a *language-independent* syntax.

In fact Infinity and NaN are not part of the number grammar not only in JavaScript but in other programming languages as well, in particular C or Java. Instead these special values can be accessed via a variable or a macro. This is however a technicality irrelevant from the point of view of syntax which would remain identical if the variable/macro identifiers were made part of the number grammar.

