## Meaningful data interchange in JSON

[ECMA-404](https://www.ecma-international.org/wp-content/uploads/ECMA-404_2nd_edition_december_2017.pdf), the official JSON standard keeps repeating the following point:

> The JSON syntax is not a specification of a complete data interchange. Meaningful data interchange requires agreement between a producer and consumer on the semantics attached to a particular use of the JSON syntax.

In practice this means that the meaning of data encoded and exchanged via JSON should be specified somehow, so that the data can be interpreted according to this meaning. This means specifying data types with specific shape and constraints which can be used when validating, deserializing, or otherwise mapping the JSON data for further processing.

Such specification can be encoded less formally in documentation and more formally in application code or in a [schema](https://json-schema.org/).

To illustrate the point, take the following piece of JSON data:

```json
{
  "id": "10765432100123456789",
  "validity": {
    "from": "2021-12-26",
    "thru": "2022-12-26"
  },
  "emails": [
    "one@example.com",
    "zwei@example.com",
    "three@example.com"
  ]
}
```

It might be accompanied by a specification which defines the following semantics and constraints:

* "id" -- a unique identifier; a 64-bit integer, 
* "validity" -- range of dates when this data is valid; an object with two properties:
  * "from" -- start of the range, inclusive; ISO 8601 date (YYYY-MM-DD), 
  * "thru" -- end of the range, inclusive; ISO 8601 date (YYYY-MM-DD),
* "emails" -- e-mail addresses associated with the id; an array of strings, each of which conforms to the Mailbox grammar defined in [RFC 5321, section 4.1.2](https://datatracker.ietf.org/doc/html/rfc5321#section-4.1.2)

We haven't defined the semantics for the entire object itself, so we don't know what it means. This is illustrates the point in a negative way: no defined semantics or constraints means we can only guess what the object represents or whether the properties included are mandatory or whether there are any unspecified optional properties. Just encoding the data in syntax is not enough for successful interchange.

Another thing we see here is that we used JSON strings to represent data types which are not built into JSON such as dates ("from", "thru") and e-mail addresses ("emails").

We also chose to represent a 64-bit integer ("id") with a string rather than a JSON number, because JSON numbers can cause interoperability problems, [especially in this case](https://github.com/xtao-org/loose-blog/blob/82b5f677d2c84a3a20ee9d76534b68aa9c1649f0/large-numbers-in-json.md).

