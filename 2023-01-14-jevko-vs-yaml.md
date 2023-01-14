# The Jevko document from heaven (Jevko compared to YAML)

A recent article [The yaml document from hell](https://ruudvanasseldonk.com/2023/01/11/the-yaml-document-from-hell) by [Ruud van Asseldonk](https://ruudvanasseldonk.com/) was linked by [Tim Bray](https://hachyderm.io/@timbray/109684432097093279) on Mastodon with the following comment:

> A lot of senior engineers loathe YAML. This piece describes a few pain points. (But skips the document-delimiter problem.)

What if we translated the pieces of YAML in that article into Jevko and compared the result? Let's find out.

## The yaml document from hell, again

Let's quote the YAML document from the article for easy reference:

```
server_config:
  port_mapping:
    # Expose only ssh and http to the public internet.
    - 22:22
    - 80:80
    - 443:443

  serve:
    - /robots.txt
    - /favicon.ico
    - *.html
    - *.png
    - !.git  # Do not expose our Git repository to the entire world.

  geoblock_regions:
    # The legal team has not approved distribution in the Nordics yet.
    - dk
    - fi
    - is
    - no
    - se

  flush_cache:
    on: [push, memory_pressure]
    priority: background

  allow_postgres_versions:
    - 9.5.25
    - 9.6.24
    - 10.23
    - 12.13
```

## The yaml document from hell translated to Jevko

Now let's see how this document could be encoded with Jevko:

```
server_config [
  port_mapping [
    Expose only ssh and http to the public internet.
    [22:22]
    [80:80]
    [443:443]
  ]
  serve [
    [/robots.txt]
    [/favicon.ico]
    [*.html]
    [*.png]
    [!.git]  Do not expose our Git repository to the entire world.
  ]
  geoblock_regions [
    The legal team has not approved distribution in the Nordics yet.
    [dk]
    [fi]
    [is]
    [no]
    [se]
  ]
  flush_cache [
    on [[push] [memory_pressure]]
    priority [background]
  ]
  allow_postgres_versions [
    [9.5.25]
    [9.6.24]
    [10.23]
    [12.13]
  ]
]
```

This translation preserves the structure and formatting of the original as much as sensible and does not try to introduce anything extra that could be introduced to make this explicitly compatible with a specific Jevko format.

What is apparent at this stage is that the Jevko document makes heavy use of square brackets (indeed, this is the only kind of brackets that is structurally relevant in Jevko). We can guess that Jevko is not indentation-sensitive (in fact Jevko itself is distinguished grammatically by not having a special category for whitespace at all). 

The beginnings and ends of every value must be marked with brackets -- thus the Jevko document is 2 lines longer than the YAML equivalent.

The only exception to the above rule is the topmost value (or equivalently the entire document) -- it is not enclosed in brackets. All this gives Jevko two interesting properties:

1. It is closed under concatenation, so you can always append to the topmost value -- this is useful when streaming and has the same advantage as JSON Lines and similar inventions, except it's much simpler and no separate specification is required -- it all flows form the way Jevko's grammar is defined. 

2. However, you can still restrict your document to only a single value enclosed in brackets and you will always be able to tell whether it has been truncated or not by looking for the matching closing bracket.

YAML is has the property 1. (as opposed to e.g. JSON), but it doesn't have the property 2. -- which creates a problem described by Tim Bray as "the document-delimiter problem" (not mentioned in the linked article).

Removing all comments and insignificant whitespace the above document could be compacted into:

```
server_config[port_mapping[[22:22][80:80][443:443]]serve[[/robots.txt][/favicon.ico][*.html][*.png][!.git]]geoblock_regions[[dk][fi][is][no][se]]flush_cache[on[[push][memory_pressure]]priority[background]]allow_postgres_versions[[9.5.25][9.6.24][10.23][12.13]]]
```