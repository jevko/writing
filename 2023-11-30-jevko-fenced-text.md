# A simple backwards-compatible Jevko extension to support fenced blocks of arbitrary text

I've been thinking about Jevko again recently and I had an idea how to backport Djevko's major convenience into Jevko in a way that:

* is aesthetically-pleasing 
* is backwards compatible
* is minimal
* is extensible
* feels somewhat familiar (Markdown-like)
* preserves Jevko's whitespace-agnosticism
* preserves Jevko's losslessness without needing to add much information to the parse tree
* adds minimal complexity for parser implementers

The convenience is the ability to paste blocks of arbitrary text without escaping AKA heredocs or, as I sometimes call them, [multistrings](https://djedr.github.io/posts/multistrings-2023-05-25.html).

Overall seems like an idea good enough to write down, so here we go.

We will add a minimal extension to the syntax to support Markdown-like fenced blocks of text. We will use plain ABNF to describe it formally.

Vanilla Jevko defines Text as follows:

```abnf
Text = *Symbol
```

(See [the spec](https://jevko.org/spec.html) for details)

To add the feature, we extend the definition like so:

```abnf
Text = Fenced / *Symbol
```

Where `Fenced` is:

```abnf
Fenced = Fenced_0 / Fenced_1 / ... / Fenced_255
Fenced_0 = "`'" *Codepoint "'`"
Fenced_1 = "``" "`'" *Codepoint "'`" "``"
Fenced_2 = "````" "`'" *Codepoint "'`" "````"
Fenced_3 = "``````" "`'" *Codepoint "'`" "``````"
...
Fenced_255 = "``````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````" "`'" *Codepoint "'`" "``````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````"
```

`Codepoint` is any unicode codepoint and we read these codepoints lazily, stopping as soon as we get to the other side of the fence.

That's basically it. We can always use a different limit than 255 for the maximum length of the fence, but that would be a sensible default I think.

Note that effectively the number of backticks that makes up one side of the fence has to always be odd, to maintain compatibility with Jevko.

This is however not a big problem, as the cases where we'd need more than one backtick should be rare indeed, because the way Jevko is defined requires that the end of the fence must always be followed by `[`, `]`, or the end of the document. There is no such thing as two `Text`s next to each other in Jevko, and so there is no such thing as two `Fenced` `Text`s next to each other.

Anyway, now we can have documents like:

```
json in jevko [`'
{ 
  "first name": "John",
  "last name": "Smith",
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
'`]

toml in jevko [`'
# last modified 1 April 2001 by John Doe
[owner]
name = "John Doe"
organization = "Acme Widgets Inc."

[database]
# use IP if name resolution is not working
server = "192.0.2.62"
port = 143
file = "payroll.dat"
"select columns" = [
  "name", 
  "address", 
  "phone number"
]
'`]
```

We can paste documents in other formats into Jevko without worrying about escaping brackets. That in itself is a significant feature for frictionless human-friendly editing which is what I always wanted Jevko to be good at.

Eventually I should get to a proper spec and implementation. For now this is it.

***

Comments welcome [on Mastodon](https://layer8.space/@jevko/111500756700128689).