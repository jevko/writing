# Draft: The Jevko document from heaven (Jevko compared to YAML)

A recent article [The yaml document from hell](https://ruudvanasseldonk.com/2023/01/11/the-yaml-document-from-hell) by [Ruud van Asseldonk](https://ruudvanasseldonk.com/) was linked by [Tim Bray](https://hachyderm.io/@timbray/109684432097093279) on Mastodon with the following comment:

> A lot of senior engineers loathe YAML. This piece describes a few pain points. (But skips the document-delimiter problem.)

What would happen if we translated the pieces of YAML in that article into Jevko and compared the result? Let's find out.

## The YAML document from hell, again

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

## The YAML document from hell translated to Jevko

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

This translation preserves the structure and formatting of the original as much as sensible and does not try to introduce anything extra to make this explicitly compatible with a specific Jevko format.

What is apparent at this stage is that the Jevko document makes heavy use of square brackets (indeed, this is the only kind of brackets that is structurally relevant in Jevko). We can guess that Jevko is not indentation-sensitive (in fact Jevko is distinguished grammatically by not having a special category for whitespace at all). 

When it comes to brackets, there are two important observations to make:

1. The document itself (equivalently the topmost value) is not enclosed in brackets, so you are free to append to it.

2. However all values nested within the document are (and must be) enclosed in brackets.

Being able to append to the document is useful when streaming and has the same advantage as JSON Lines and similar inventions, except here it's much simpler and no separate specification is required -- it all flows form Jevko's grammar.

On the other hand being required to enclose all nested values in brackets allows one to restrict a document to only a single value (or a finite number of values) enclosed in brackets, so that one will always be able to tell whether the value has been truncated or not by looking for the matching closing bracket.

YAML documents are similarly appendable (as opposed to e.g. JSON), but nested values don't have to be enclosed in brackets -- which creates a problem described by Tim Bray as "the document-delimiter problem" (not mentioned in the linked article). You can never be sure whether the trailing values in the document are truncated.

Because Jevko is based around brackets rather than whitespace, we can compact the above document by removing all comments and insignificant whitespace:

```
server_config[port_mapping[[22:22][80:80][443:443]]serve[[/robots.txt][/favicon.ico][*.html][*.png][!.git]]geoblock_regions[[dk][fi][is][no][se]]flush_cache[on[[push][memory_pressure]]priority[background]]allow_postgres_versions[[9.5.25][9.6.24][10.23][12.13]]]
```

Now, if we used a plain Jevko parser on any of the above documents we would not get a nice programming language structure with the appropriate (or not, as we see in YAML) data types figured out by the parser. Instead we would get a raw syntax tree which has the correct structure (defined by the brackets), but nothing in it is interpreted in any way -- the leaves of the tree are just text.

If we want to transform this tree into a sensible data structure we would need to process it further, according to chosen semantics. Only after combining pure syntax with semantics we would get to the same point as we get after parsing YAML.

This is the point of Jevko: it serves the role of the pure universal text-based syntax, completely separated from semantics. This gives us more power and flexibility and gets rid of the issues that come from premature entanglemet of syntax and semantics, as we see in YAML. That is, if we need that.

If we're not interested in that, as most users are not, we can still benefit from Jevko, by using a *Jevko format* -- which is a ready-made combination of syntax (Jevko) and semantics that does the right thing for us.