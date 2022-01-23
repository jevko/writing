# Encoding hexadecimal numbers with 10 digits

Suppose we only have 10 digits: `0123456789`, ordinarily used to express decimal numbers, such as:

<table>
  <thead>
    <tr><th>decimal</th></tr>
  </thead>
  <tbody>
    <tr><td>1</td></tr>
    <tr><td>12</td></tr>
    <tr><td>57</td></tr>
    <tr><td>128</td></tr>
    <tr><td>1000</td></tr>
    <tr><td>5598</td></tr>
  </tbody>
</table>

Except we want to use them to express hexadecimal numbers which have 16 digits: `0123456789abcdef`. Hexadecimal equivalents of the above numbers would be:

<table>
  <thead>
    <tr><th>decimal</th><th>hexadecimal</th></tr>
  </thead>
  <tbody>
    <tr><td>1</td><td>1</td></tr>
    <tr><td>12</td><td>c</td></tr>
    <tr><td>57</td><td>20</td></tr>
    <tr><td>128</td><td>80</td></tr>
    <tr><td>1000</td><td>3e8</td></tr>
    <tr><td>5598</td><td>15de</td></tr>
  </tbody>
</table>

We can see that we are short by 6 digits: `abcdef`. We need some way to express these with the 10 digits that we do have, while still being able to express the original 10 digits.

One solution to this problem is to use digraphs.

For example, we can take `0` out of the pool of the available digits and use it as a mark to start a digraph. Once we do this, we can easily express the 16 digits as follows: digits `1` thru `9` stand for themselves. The remaining digits are expressed by digraphs:

<table>
  <thead>
    <tr><th>hexadecimal digit</th><th>decimal-encoded hexadecimal digit</th></tr>
  </thead>
  <tbody>
    <tr><td>0</td><td><code>00</code></td></tr>
    <tr><td>a</td><td><code>01</code></td></tr>
    <tr><td>b</td><td><code>02</code></td></tr>
    <tr><td>c</td><td><code>03</code></td></tr>
    <tr><td>d</td><td><code>04</code></td></tr>
    <tr><td>e</td><td><code>05</code></td></tr>
    <tr><td>f</td><td><code>06</code></td></tr>
  </tbody>
</table>

Using this system we can express the numbers above as follows:

<table>
  <thead>
    <tr><th>decimal</th><th>hexadecimal</th><th>decimal-encoded hexadecimal</th></tr>
  </thead>
  <tbody>
    <tr><td>1</td><td>1</td><td>1</td></tr>
    <tr><td>12</td><td>c</td><td><code>03</code></td></tr>
    <tr><td>57</td><td>20</td><td>2<code>00</code></td></tr>
    <tr><td>128</td><td>80</td><td>8<code>00</code></td></tr>
    <tr><td>1000</td><td>3e8</td><td>3<code>05</code>8</td></tr>
    <tr><td>5598</td><td>15de</td><td>15<code>04</code><code>05</code></td></tr>
  </tbody>
</table>

# Grammar patterns: escape

suppose we have the following grammar, which matches any string:

```abnf
text = *char
; char = any character
```

now we want to reserve a character to have special meaning,

```
text = *char
; char = any character except ,
```


 but we still want to allow a way to encode this character in the text

one way to do that is thru an escape mechanism

```
text = *(char / escape)
escape = "\" ("\" / ",")
; char = any character except ,
```

# Grammar patterns: interleaving

Say we want to have a grammar for comma-separated a-z letters.

```abnf
list = item *("," item)
item = *(escape / char)
escape = "\" ("\" / ",")
; char = any character except from "/" or ","
````