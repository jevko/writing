# IEEE754 numbers in JSON: NaN or Infinity

In [a previous article](https://xtao.org/blog/json-semantics.html) I mentioned problems with the number type in JSON.

In [another article](https://github.com/xtao-org/loose-blog/blob/35b2b9220dd6f99a3b33628d143a30ffd82f953e/large-numbers-in-json.md) I expanded on the issue of large numbers.

In this article I will talk about the problem of representing Infinity and NaN.

[RFC 8259](https://datatracker.ietf.org/doc/html/rfc8259#section-6) says this:

> Since software that implements IEEE 754 binary64 (double precision) numbers [IEEE754] is generally available and widely used, good interoperability can be achieved by implementations that expect no more precision or range than these provide

Indeed, the IEEE754 standard offers interoperability across different environments. However JSON numbers are not fully compatible with it because they exclude the special IEEE754 values: +-Infinity and NaN.

This keeps causing problems in practice. [For example](https://bugs.python.org/issue40633#msg384059):

> Essentially, there's no good answer here: standard JSON simply can't encode infinities and NaNs. Absent a fix for the standard itself, both Python and ECMAScript end up papering over that fact. Unfortunately from an interoperability point of view, they do so in different ways - Python effectively extends the JSON spec in such a way that it produces invalid JSON by default; ECMAScript converts all of Infinity, -Infinity, NaN and null to the exact same JSON string, producing valid JSON but losing the ability to restore the original values from their JSON representations.

Depending on the parser or configuration we will see different workarounds used when serializing these values. The main solutions are:

* raise an error
* convert to null
* convert to strings "+Infinity", "-Infinity", "NaN", or other

The last workaround is compatible with the workaround for representing large numbers I described in the last article, i.e. to serialize the numbers to strings and tell your consumers.

And I mean all numbers, not just the special values. Reasons are the same as for large numbers:

* There may be no need to interpret the strings
* Interpretation should be explicit
* Special casing is unnecessary

Simply always use strings and explicitly inform your interchange parties instead of relying on JSON numbers.

## Related links

[golang/go: encoding/json: handle NaN and Inf #3480](https://github.com/golang/go/issues/3480)

[ECMA-262](https://262.ecma-international.org/#sec-json.stringify):

> Finite numbers are stringified as if by calling ToString(number). **NaN and Infinity regardless of sign are represented as the String "null".**

[NaN handling in JSON for Modern C++](https://json.nlohmann.me/features/types/number_handling/#nan-handling)

