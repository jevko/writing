# Large numbers in JSON

In [a previous article](https://xtao.org/blog/json-semantics.html) I mentioned problems with the number type in JSON.

In this article I will examine one of these problems and discuss a way to fix it.

## The problem

When representing large numbers in JSON, and large integers particularly, there is a high chance that somewhere along the way there will be a parser which will truncate numbers outside of the `[-(2\*\*53)+1, (2\*\*53)-1]` range. 

In particular, this will happen when interacting with JavaScript. 

It may or may not happen in other languages, depending on the parser and its configuration.

Whenever it happens, it may lead to serious interoperability issues and bugs.

## The solution

Don't rely on JSON numbers. Use JSON strings instead and, if need be, explicitly tell your interchange parties what precision or data type they need to parse thus encoded numbers.

You can communicate this via documentation, schema, or any similar way suitable in your particular case.

## Why this is sensible

JSON numbers were designed to be minimal and independent of internal representation. They are just syntax, like strings. Implementations are free to attach their own semantics and use their own representations.

Those that choose the same representation as JavaScript suffer from the truncation problem described above. Those that recognize the issue may still choose a representation which works for larger numbers but fails for numbers over 64 bits or larger.

There is therefore no guarantee that your numbers will be encoded or decoded correctly and no way to tell when, where, and for whom this will cause problems.

This is a sufficient reason why it is better to simply use JSON strings to encode numbers and explicitly inform your interchange parties about their characteristics, in the same way that you would do for any data type not built into JSON, such as Date or Duration.

Agreement between interchange parties is essential to achieve meaningful data interchange, as highlighted by [ECMA-404](https://www.ecma-international.org/wp-content/uploads/ECMA-404_2nd_edition_december_2017.pdf), the official JSON standard:

> The JSON syntax is not a specification of a complete data interchange. Meaningful data interchange requires agreement between a producer and consumer on the semantics attached to a particular use of the JSON syntax.

Using JSON numbers makes this impossible in enough cases in practice that they become a hazard rather than an advantage.

Employing strings and explicit communication removes that hazard.

## Example #1: 7 different interpretations for the same number

[An Exploration of JSON Interoperability Vulnerabilities](https://bishopfox.com/blog/json-interoperability-vulnerabilities) by Jake Miller presents an interesting example of this problem.

The following input with an extremely large number:

```json
{"description": "Big float", "test": 1.0e4096}
```

is deserialized and/or reserialized into:

```json
{"description":"Big float","test":1.0e4096}
{"description":"Big float","test":Infinity}
{"description":"Big float","test":"+Infinity"}
{"description":"Big float","test":null}
{"description":"Big float","test":Inf}
{"description":"Big float","test":3.0e14159265358979323846}
{"description":"Big float","test":9.218868437227405E+18}
```

by different parsers. Only the first result is correct. 6 out of 7 break in different ways. 2 of those are not even valid JSON.

## Example #2: Twitter IDs

Another example is the problem of [Twitter IDs](https://developer.twitter.com/en/docs/twitter-ids).

Initially Twitter used sequential 32-bit numbers as unique identifiers for tweets, users, and various other entities. As it grew however, these IDs proved insufficient, and were switched to 64-bits.

This is when the truncation issue started causing problems.

The problem was remediated as follows:

> In order to provide a workaround for this, in the original designs of the Twitter API (v1/1.1), ID values were returned in two formats: both as integers, and as strings.

```json
{"id": 10765432100123456789, "id_str": "10765432100123456789"}
```

> [...]

> In Twitter APIs up to version 1.1, you should always use the string representation of the number to avoid losing accuracy.

> In newer versions of the API, all large integer values are represented as strings by default.

## Benefits of string-encoded numbers 

### There may be no need to interpret the strings

In the above Twitter example opting for strings is not only a better default, but there may be no need for the alternative.

In cases where we don't do arithmetic on the numbers, there may never be any need to convert the strings to numbers. If we only do comparisons, or process the data in a way which doesn't touch the numbers, strings will work even in an environment which does not support large intergers. We can be sure that they will be correctly interpreted and reserialized.

### Interpretation should be explicit

If we however need to perform operations on the numbers we can convert the strings to a suitable type in a separate step, after parsing JSON. This might work even in JavaScript and other environments which don't have native numbers with enough precision -- we can always use (or in extreme cases write) a bignum library^[N.b. nowadays [support for BigInts is built into JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt).].

### Special casing is unnecessary

Since strings are adequate either way and always work why complicate things and make them needlessly iffy by only representing *large* integers as strings? Instead, represent *all* integers as strings and treat them uniformly. No special cases or explanations needed.

And while we're at it, why not represent non-integers as numbers as well?

### Reverse engineering

For somebody reverse-engineering an API which uses strings to encode numbers explicit communication might not even be necessary. This practice is easy to identify and deal with for humans.

## See also

[Mangling JSON numbers](https://www.techempower.com/blog/2016/07/05/mangling-json-numbers/)

[[json-minefield]: Parsing JSON is a Minefield, Nicolas Seriot](https://seriot.ch/projects/parsing_json.html)
[[json-vulnerabilities]: An Exploration of JSON Interoperability Vulnerabilities, Jake Miller](https://bishopfox.com/blog/json-interoperability-vulnerabilities) 
