# Hacking XML attributes with Jevko

Caution: madness ahead!

In this article I will show how to combine Jevko with XML in a hack which will get us out of a pickle caused by inextensibility of XML attributes. All this without changes to the structure of the XML. No meddling with mappings or schemas, no breaking of compatibility. Better yet: thanks to using Jevko, this hack is recursively extensible as opposed to space or comma separated values or similar inextensible syntax.

## The problem with XML attributes

In this section I will recap the issue from [the previous article](2022-01-21-json-vs-xml.md).

In XML attributes and elements have differing semantics: attributes are simple name-value pairs with names unique within an element, whereas there can be multiple elements with the same name within a parent element. 

XML attributes are more compact than XML elements, but they are not extensible: their values are limited to text. It is not possible to put XML trees inside an attribute value.

Due to their different roles and semantics, XML elements and attributes are not interchangeable. Using XML attributes for modeling data makes future extension in backwards-compatible manner a serious issue.

For example if we start like this:

```xml
<element id="123" />
```

and then need to extend the value of the `id` attribute with a `provider`, we have a problem.

We can't assign an XML structure to the attribute. Instead we might do something like this:

```xml
<element>
  <id provider="SomeProvider">123</id>
</element>
```

which is a significant syntactic and structural change and makes the two elements incompatible without employing more advanced mechanisms.

And we are back to the same problem if a need arises to add structure to the `provider` attribute.

Because of this and because of the verbosity of XML, workarounds like the following are often employed instead:

```xml
<element id="SomeProvider,123" />
<element id="SomeProvider 123" />
<element id="provider=SomeProvider,value=123" />
```

i.e. the attribute's value is changed to a string which contains a structure expressed in a specialized syntax, which has to be parsed separately.

If the syntax is similarly not extensible, this may lead to a more messy version of the same problem.

In any case, the inextensibility of XML attributes may lead to unnecessary complexity, compatibility, and maintainability issues. This is why a lot of XML used for data interchange uses attributes very sparingly or not at all. This unfortunately leads to verbosity which often has to be somehow dealt with.

## Jevko to the rescue

To keep ourselves from having to worry about our clever workaround breaking when the problem gets recursive on us, we can make it even more clever and immune to that. How? By using Jevko! How? Like this:

```xml
<element id="provider[SomeProvider]123" />
```

One neat thing about it is that if we have a Jevko parser which produces parse trees consistent with the [high-level Jevko grammar](2022-01-20-jevko-grammar.md), we will get a compatible result for both:

```xml
<element id="123" />
<element id="provider[SomeProvider]123" />
```

i.e. the old and the extended version. From the point of view of the parse tree, as long as it comes last in the string, the `123` here is always a `suffix`, even if we add more "properties":

```xml
<element id="123" />
<element id="worker[32]provider[SomeProvider]123" />
```

and we can extend this recursively:

```xml
<element id="123" />
<element id="worker[32]provider[group[5]SomeProvider]123" />
```

Now the only thing which stands between us and implementing this workaround is the lack of available Jevko parsers. Fortunately, this is not difficult to overcome. A Jevko parser can be written by hand in a few lines. For example here is a complete program in JavaScript which implements this hack in the browser:

```js
// say whaaat?
const parseJevko=e=>{const s=[];let r={subjevkos:[]},l="",t=!1;for(let o=0;o<e.length;++o){const f=e[o];if(t){if("`"!==f&&"["!==f&&"]"!==f)throw Error("Invalid escape!");l+=f,t=!1}else if("`"===f)t=!0;else if("["===f){const e={subjevkos:[]};r.subjevkos.push({prefix:l,jevko:e}),s.push(r),r=e,l=""}else if("]"===f){if(r.suffix=l,l="",s.length<1)throw Error("Unexpected close!");r=s.pop()}else l+=f}if(t||s.length>0)throw Error("Unexpected end!");return r.suffix=l,r};

const parser = new DOMParser();

const doc1 = parser.parseFromString(`
<element id="123" />
`, "application/xml")

const jevko1 = parseJevko(doc1.documentElement.getAttribute('id'))

console.log(jevko1.suffix) // 123

const doc2 = parser.parseFromString(`
<element id="worker[32]provider[group[5]SomeProvider]123" />
`, "application/xml");

const jevko2 = parseJevko(doc2.documentElement.getAttribute('id'))

console.log(jevko2.suffix) // 123

const jevkoToJsonObject = (jevko) => {
  const {subjevkos, suffix} = jevko
  const ret = {value: suffix}
  for (const {prefix, jevko} of subjevkos) {
    ret[prefix] = jevkoToJsonObject(jevko)
  }
  return ret
}

console.log(jevkoToJsonObject(jevko2))
```

The last `console.log` prints something like this:

```json
{
  "value": "123",
  "worker": {
    "value": "32"
  },
  "provider": {
    "value": "SomeProvider",
    "group": {
      "value": "5"
    }
  }
}
```

Take that, XML attributes!

:D

***

© 2022 Darius J Chuck