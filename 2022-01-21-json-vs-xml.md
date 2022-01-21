# Some differences between XML and JSON

Let's consider the following JSON sample from [Wikipedia](https://en.wikipedia.org/wiki/JSON#Syntax):

```json
{
  "first name": "John",
  "last name": "Smith",
  "is alive": true,
  "age": 27,
  "address": {
    "street address": "21 2nd Street",
    "city": "New York",
    "state": "NY",
    "postal code": "10021-3100"
  },
  "phone numbers": [
    {
      "type": "home",
      "number": "212 555-1234"
    },
    {
      "type": "office",
      "number": "646 555-4567"
    }
  ],
  "children": [],
  "spouse": null
}
```

and contrast it with a similar XML sample:

```xml
<person
  first-name="John"
  last-name="Smith"
  is-alive="true"
  age="27"
>
  <address
    street-address="21 2nd Street"
    city="New York"
    state="NY"
    postal-code="10021-3100"
  />
  <phone-numbers>
    <phone-number
      type="home"
      number="212 555-1234"
    />
    <phone-number
      type="office"
      number="646 555-4567"
    />
  </phone-numbers>
  <children />
  <spouse />
</person>
```

## JSON object properties vs XML elements and attributes

### Whitespace

Keys in a JSON object can contain whitespace, so we can write `first name` and `phone numbers`.

Element and attribute names in XML cannot contain whitespace, so we must write `first-name` and `phone-numbers` rather than `first name` and `phone numbers`.

### Semantics

According to [ECMA-404](https://www.ecma-international.org/wp-content/uploads/ECMA-404_2nd_edition_december_2017.pdf) keys within a JSON object need not be unique and their ordering has no significance. [RFC8259](https://datatracker.ietf.org/doc/html/rfc8259#section-4) on the other hand recommends that they are unique and unordered in the interest of interoperability. [JSON.org](https://www.json.org) defines an object as "an *unordered* set of name/value pairs".

In XML attributes and elements have differing semantics: attributes are simple name-value pairs with names unique within an element, whereas there can be multiple elements with the same name within a parent element. 

<!-- Attributes are then specialized and restricted. -->

<!-- compactness? -->
### Extensibility

<!-- * in contrast with XML attributes,  -->

JSON object properties can have simple or complex values. Every value in a JSON object can be swapped with any other JSON value, including a nested JSON object. In this way, JSON object properties are flexible and extensible.

XML attributes are more compact than XML elements, but they are not extensible like JSON properties: their values are limited to text. It is not possible to put XML trees inside an attribute value.

Due to their different roles and semantics, XML elements and attributes are not interchangeable. Using XML attributes for modeling data makes future extension in backwards-compatible manner a serious issue.

For example going from this JSON:

```json
{
  "id": "123"
}
```

into this JSON:

```json
{
  "id": {
    "provider": "SomeProvider",
    "value": "123"
  }
}
```

is relatively straightforward.

These two objects are compatible as to property names -- only the values are of different types. If in the initial design we assumed the `id` property to have a string value, we can simply relax this constraint to "string or object" to preserve backwards-compatibility.

Since there is no way to assign an XML structure to an XML attribute, we might do something like this:

```xml
<element id="123" />
```

```xml
<element>
  <id provider="SomeProvider">123</id>
</element>
```

which is a significant syntactic and structural change and makes the two elements incompatible without employing more advanced mechanisms.

And we are back to the same problem if we a need arises to add structure to the `provider` attribute.

Because of this and because of the verbosity of XML, workarounds like the following are often employed instead:

```xml
<element id="SomeProvider,123" />
<element id="SomeProvider 123" />
<element id="provider=SomeProvider,value=123" />
```

i.e. the attribute's value is changed to a string which contains a structure expressed in a specialized syntax, which has to be parsed separately.

If the syntax is similarly not extensible, this may lead to a more messy version of the same problem.

In any case, the inextensibility of XML attributes may lead to unnecessary complexity, compatibility, and maintainability issues, compared to JSON properties.

This is why a lot of XML used for data interchange uses attributes very sparingly or not at all. This unfortunately leads to verbosity which often has to be somehow dealt with. From the point of view of JSON this is an entirely unnecessary problem.

## Data types

JSON has a few built-in data types: objects, arrays, strings, `null`, `true`, and `false`. The last two are implicitly introduced as booleans by RFC8259, but ECMA-404 only names them along with `null` as "literal name tokens", ascribing no meaning. In the sample the value of the `"is alive"` property is a boolean or a `true`, the value of `"age"` is a number, the value of `"spouse"` is a `null`, the values of `"phone numbers"` and `"children"` are arrays, all the values enclosed in `""` are strings, and all the values enclosed in `{}` are objects. No external schema is required to recognize these types -- they are distinguished by syntax alone.

In pure XML, without XML schema, all attribute values are text. Particularly in the sample the values of the `is-alive` and `age` attributes are text. It is assumed that conversions from text to specific types, such as numbers or booleans are performed when processing XML, based on a formal or an informal schema.

If we wanted to make the JSON sample more equivalent to XML, we might replace `true` with `"true"`, `27` with `"27"`, `[]` with `""`, and `null` with `""`; this would effectively make the JSON larger than the XML and lose possibly useful type information.

If we wanted to make the XML example more equivalent to JSON in terms of types, we would have to introduce significant complication and give up a lot of compactness. For example, instead of `<spouse />` we would use `<spouse xsi:nil="true" />` which is a standard way of assigning a null value to an element in XML. This however requires opting into XML namespaces and XML schema by, at a minimum, adding a `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"` attribute in an appropriate place in our data in order for an XML parser to consider it well-formed. Therefore where simplicity and compactness are considered, JSON still comes out ahead of XML.

On the other hand JSON types are not a replacement for XML schema. The fact that values have certain types in a given JSON sample does not tell us whether and what constraints are implicitly placed on these values. Two JSON samples from the same source might produce objects with identical property names, but values of different types and we have no way of knowing, without using a schema, whether that is correct and if not what type is right for the value.

***

© 2022 Darius J Chuck