# Draft: Explicit decoding of syntax trees into specific types

Jevko is pure syntax separated from semantics.

This separation of concerns allows for fine-grained control over how individual parts of a syntax tree are interpreted.

One way to realize this control is to explicitly extract different parts of a Jevko syntax tree as specific types.

Say we have a Jevko document like this:

```
last modified 1 April 2001 by John Doe
[owner]
name [John Doe]
organization [Acme Widgets Inc.]

[database]
use IP if name resolution is not working
server [192.0.2.62]
port [143]
file [payroll.dat]
select columns [
  [name]
  [address]
  [phone number]
]
```

We parse it into a syntax tree:

```
tree = parse(document)
```

We interpret the tree as a map with sections:

```
map = asMapWithSections(tree)
```

Say now we want to extract the port as an integer:

```
port = asInteger(atPath(map, ['database', 'port']))
```