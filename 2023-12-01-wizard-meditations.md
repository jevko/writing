---
title: "Meditating on the Wizard Book for language design: Snippets"
date: 2023-12-01
author: Darius J Chuck
---

Here I have translated all code snippets from the Wizard Book aka SICP (specifically "Structure and Interpretation of Computer Programs", Second Edition, 1996, by Harold Abelson and Gerald Jay Sussman with Julie Sussman.) to a semi-imaginary programming language based on Jevko.

The basis for the language was [Jevkalk](https://github.com/jevko/jevkalk), a little prototype I played around with some time earlier. As I went along with the translation, I designed/sketched out the necessary syntax and features, adding comments where appropriate.

This was an exercise in programming language design and a daily meditative practice for me. It took me just over half a year, starting in February 2023, ending in August. I have translated page-by-page, aiming for at least one page per day.

All sections in this document correspond exactly to the numbered pages in the book.

## page 6

```
+ [[137][349]]
- [[1000][334]]
* [[5][99]]
/ [[10][5]]
+ [[2.7][10]]

+ [[21][35][2][7]]
* [[25][4][12]]

+ [* [[3][5]] - [[10][6]]]
```

## page 7

```
+ [* [[3] + [* [[2][4]] + [[3][5]]]] + [- [[10][7]] [6]]]

+ [
  * [
    [3] 
    + [
      * [[2][4]] 
      + [[3][5]]
    ]
  ] 
  + [
    - [[10][7]]
    [6]
  ]
]

define [[size][2]]
```

## page 8

```
[size]

* [[5][size]]

define [[pi][3.14159]]

define [[radius][10]]

* [[pi] * [[radius][radius]]]

define [[circumference] * [[2][pi][radius]]]

[circumference]
```

## page 9

```
* [
  + [[2] * [[4][6]]]
  + [[3][5][7]]
]
```

## page 12

```
define [[square] fun [[x] * [[x][x]]]]
```

## page 13

```
square [21]

square [+ [[2][5]]]

square [square [3]]

+ [square [x] square [y]]

define [[sum of squares] fun [[[x][y]]
  + [square [x] square [y]]
]]

sum of squares [[3][4]]

define [[f] fun [[a]
  sum of squares [+ [[a][1]] * [[a][2]]]
]]

f [5]
```

## page 14

```
f [5]

sum of squares [+ [[a][1]] * [[a][2]]]

sum of squares [+ [[5][1]] * [[5][2]]]

+ [square [6] square [10]]

+ [* [[6][6]] * [[10][10]]]

+ [[36][100]]
```

## page 16

```
f [5]

sum of squares [+ [[5][1]] * [[5][2]]]

+ [square [+ [[5][1]]] square [* [[5][2]]]]

+ [* [+ [[5][1]] + [[5][1]]] * [* [[5][2]]] * [[5][2]]]

+ [* [[6][6]] * [[10][10]]]

+ [[36][100]]

* [[x][x]]
```

## page 17

```
define [[abs] fun [[x]
  ? [
    > [[x][0]] [x]
    = [[x][0]] [0]
    < [[x][0]] - [x]
  ]
]]
```

```
? [
  <p_1> <e_1>
  <p_2> <e_2>
  .
  .
  .
  <p_n> <e_n>
]
```

## page 18

```
define [[abs] fun [[x]
  ? [
    < [[x][0]] - [x]
    [x]
  ]
]]
```

## page 19

```
and [[e_1] ... [e_n]]

or [[e_1] ... [e_n]]

not [e]

and [> [[x][5]] < [[x][10]]]
```

## page 20

```
define [[>=] fun [[[x][y]]
  or [> [[x][y]] = [[x][y]]]
]]

define [[>=] fun [[[x][y]]
  not [< [[x][y]]]
]]
```

<!-- exercise 1.1 -->

```
[10]

+ [[5][3][4]]

- [[9][1]]

/ [[6][2]]

+ [* [[2][4]] - [[4][6]]]

define [[a][3]]

define [[b] + [[a][1]]]

+ [[a][b] * [[a][b]]]

= [[a][b]]

? [
  and [> [[b][a]] < [[b] * [[a][b]]]] [b]
  [a]
]

? [
  = [[a][4]] [6]
  = [[b][4]] + [[6][7][a]]
  [25]
]

+ [[2] ? [> [[b][a]] [b] [a]]]

* [? [
  > [[a][b]] [a]
  < [[a][b]] [b]
  [-1]
] + [[a][1]]]
```

## page 21

<!-- ex. 1.4 -->

```
define [[a plus abs b] fun [[[a][b]] 
  apply [
    ? [
      > [[b][0]] [+]
      [-]
    ]
    [a]
    [b]
  ]
]]
```

<!-- ex. 1.5 -->

```
define [[p] p []]

define [[test] fun [[[x][y]]
  ? [
    = [[x][0]] [0]
    [y]
  ]
]]

test [[0] p []]
```

## page 23

```
define [[sqrt iter] fun [[[guess][x]]
  ? [
    good enough? [[guess][x]] [guess]
    sqrt iter [improve [[guess][x]] [x]]
  ]
]]

define [[improve] fun [[[guess][x]]
  average [[guess] / [[x][guess]]]
]]

define [[average] fun [[[x][y]]
  / [+ [[x][y]] [2]]
]]
```

## page 24

```
define [[good enough?] fun [[[guess][x]]
  < [abs [- [square [guess] [x]]] [0.001]]
]]

define [[sqrt] fun [[x]
  sqrt iter [[1.0][x]]
]]

sqrt [9]

sqrt [+ [[100][37]]]

sqrt [+ [sqrt [2] sqrt [3]]]

square [sqrt [1000]]
```

## page 25

```
define [[new if] fun [[
  [predicate]
  [then clause]
  [else clause]
]
  ? [
    [predicate] [then clause]
    [else clause]
  ]
]]

new if [= [[2][3]] [0] [5]]

new if [= [[1][1]] [0] [5]]

define [[sqrt iter] fun [[[guess][x]]
  new if [good enough? [[guess][x]]
    [guess]
    sqrt iter [improve [[guess][x]] [x]]
  ]
]]
```

## page 27

```
define [[square] fun [[x]
  * [[x][x]]
]]

define [[square] fun [[x]
  exp [double [log [x]]]
]]

define [[double] fun [[x]
  + [[x][x]]
]]
```

## page 28

```
define [[square] fun [[x]
  * [[x][x]]
]]

define [[square] fun [[y]
  * [[y][y]]
]]

define [[good enough?] fun [[[guess][x]]
  < [abs [- [square [guess] [x]]] [0.001]]
]]
```

## page 29

```
define [[sqrt] fun [[x]
  sqrt iter [[1.0][x]]
]]
```

```
define [sqrt iter [[guess][x]]
  ? [
    good enough? [[guess][x]] [guess]
    sqrt iter [improve [[guess][x]] [x]]
  ]
]

define [good enough? [[guess][x]]
  < [abs [- [square [guess] [x]]] [0.001]]
]

define [improve [[guess][x]]
  average [[guess] / [[x][guess]]]
]
```

## page 30

```
define [sqrt [x]
  define [good enough? [[guess][x]]
    < [abs [- [square [guess] [x]]] [0.001]]
  ]
  define [improve [[guess][x]]
    average [[guess] / [[x][guess]]]
  ]
  define [sqrt iter [[guess][x]]
    ? [
      good enough? [[guess][x]] [guess]
      sqrt iter [improve [[guess][x]] [x]]
    ]
  ]
  sqrt iter [[1.0][x]]
]

define [sqrt [x]
  define [good enough? [guess]
    < [abs [- [square [guess] [x]]] [0.001]]
  ]
  define [improve [guess]
    average [[guess] / [[x][guess]]]
  ]
  define [sqrt iter [guess]
    ? [
      good enough? [guess] [guess]
      sqrt iter [improve [guess]]
    ]
  ]
  sqrt iter [1.0]
]
```

## page 32

```
factorial [6]

* [[6] factorial [5]]

* [[6] * [[5] factorial [4]]]

* [[6] * [[5] * [[4] factorial [3]]]]

* [[6] * [[5] * [[4] * [[3] factorial [2]]]]]

* [[6] * [[5] * [[4] * [[3] * [[2] factorial [1]]]]]]

define [factorial [n]
  ? [
    = [[n][1]] [1]
    * [[n] factorial [- [[n][1]]]]
  ]
]
```

## 33

```
factorial [6]
fact iter [[1][1][6]]
fact iter [[1][2][6]]
fact iter [[2][3][6]]
fact iter [[6][4][6]]
fact iter [[24][5][6]]
fact iter [[120][6][6]]
fact iter [[720][7][6]]

define [factorial [n]
  define [iter [[product][counter]]
    ? [
      > [[counter][n]] [product]
      fact iter [
        * [[counter][product]]
        + [[counter][1]]
      ]
    ]
  ]
  iter [[1][1]]
]
```

## 34

```
define [factorial [n]
  fact iter [[1][1][n]]
]

define [fact iter [[product][counter][max count]]
  ? [
    > [[counter][max count]] [product]
    fact iter [
      * [[counter][product]]
      + [[counter][1]]
      [max count]
    ]
  ]
]
```

## 36

```
define [+ [[a][b]]
  ? [
    = [[a][0]] [b]
    inc [+ [dec [a] [b]]]
  ]
]

define [+ [[a][b]]
  ? [
    = [[a][0]] [b]
    + [dec [a] inc [b]]
  ]
]

define [A [[x][y]]
  ? [
    = [[y][0]] [0]
    = [[x][0]] * [[2][y]]
    = [[y][1]] [2]
    A [
      - [[x][1]] 
      A [[x] - [[y][1]]]
    ]
  ]
]

A [[1][10]]

A [[2][4]]

A [[3][3]]
```

## 37

```
define [f [n] A [[0][n]]]

define [g [n] A [[1][n]]]

define [h [n] A [[2][n]]]

define [k [n] * [[5][n][n]]]

define [fib [n]
  ? [
    = [[n][0]] [0]
    = [[n][1]] [1]
    + [
      fib [- [[n][1]]]
      fib [- [[n][2]]]
    ]
  ]
]
```

## 39

```
define [fib [n]
  fib iter [[1][0][n]]
]

define [fib iter [[a][b][count]]
  ? [
    = [[count][0]] [b]
    fib iter [+ [[a][b]] [a] - [[count][1]]]
  ]
]
```

## 40

```
define [count change [amount]
  cc [[amount][5]]
]
```

## 41

```
define [cc [[amount][kinds of coins]]
  ? [
    = [[amount][0]] [1]
    or [< [[amount][0]] = [[kinds of coins][0]]] [0]
    + [
      cc [
        [amount]
        - [[kinds of coins][1]]
      ]
      cc [
        - [
          [amount]
          first denomination [kinds of coins]
        ]
        [kinds of coins]
      ]
    ]
  ]
]

define [first denomination [kinds of coins]
  ? [
    = [[kinds of coins][1]] [1]
    = [[kinds of coins][2]] [5]
    = [[kinds of coins][3]] [10]
    = [[kinds of coins][4]] [25]
    = [[kinds of coins][5]] [50]
  ]
]

count change [100]
```

## 44

```
define [cube [x]
  * [[x][x][x]]
]

define [p [x]
  - [* [[3][x]] * [[4] cube [x]]]
]

define [sine [angle]
  ? [
    not [> [abs [angle] [0.1]]]
    [angle]
    p [sine [/ [[angle][3.0]]]]
  ]
]

define [expt [[b][n]]
  ? [
    = [[n][0]] [1]
    * [[b] expt [[b] - [[n][1]]]]
  ]
]
```

## 45

```
define [expt [[b][n]]
  expt iter [[b][n][1]]
]

define [expt iter [[b][counter][product]]
  ? [
    = [[counter][0]] [product]
    expt iter [
      [b]
      - [[counter][1]]
      * [[b][product]]
    ]
  ]
]

define [fast expt [[b][n]]
  ? [
    = [[n][0]] [1]
    even? [n] square [fast expt [[b] / [[n][2]]]]
    * [[b] fast expt [[b] - [[n][1]]]]
  ]
]

define [even? [n]
  = [remainder [[n][2]] [0]]
]
```

## 46

```
define [* [[a][b]]
  ? [
    = [[b][0]] [0]
    + [[a] * [[a] - [[b][1]]]]
  ]
]
```

## 47

```
define [fib [n]
  fib iter [[1][0][0][1][n]]
]

define [fib iter [[a][b][p][q][count]]
  ? [
    = [[count][0]] [b]
    even? [count] fib iter [
      [a]
      [b]
      [??]    compute p'
      [??]    compute q'
      / [[count][2]]
    ]
    fib iter [
      + [* [[b][q]] * [[a][q]] * [[a][p]]]
      + [* [[b][p]] * [[a][q]]]
      [p]
      [q]
      - [[count][1]]
    ]
  ]
]
```

## 49

```
define [gcd [[a][b]]
  ? [
    = [[b][0]] [a]
    gcd [[b] remainder [[a][b]]]
  ]
]
```

## 50

```
define [smallest divisor [n]
  find divisor [[n][2]]
]

define [find divisor [[n][test divisor]]
  ? [
    > [square [test divisor] [n]] [n]
    divides? [[test divisor] [n]] [test divisor]
    find divisor [[n] + [[test divisor] [1]]]
  ]
]

define [divides? [[a][b]]
  = [remainder [[b][a]] [0]]
]

define [prime? [n]
  = [[n] smallest divisor [n]]
]
```

## 51

```
define [expmod [[base][exp][m]]
  ? [
    = [[exp][0]] [1]
    even? [exp] remainder [
      square [expmod [[base] / [[exp][2]] [m]]]
      [m]
    ]
    remainder [
      * [[base] expmod [[base] - [[exp][1]] [m]]]
      [m]
    ]
  ]
]
```

## 52

```
define [fermat test [n]
  define [try it [a]
    = [expmod [[a][n][n]] [a]]
  ]
  try it [+ [[1] random [- [[n][1]]]]]
]

define [fast prime? [[n][times]]
  ? [
    = [[times][0]] [true]
    fermat test [n] fast prime? [[n] - [[times][1]]]
    [false]
  ]
]
```

## 54

Note: at this point I am introducing string syntax not implemented in current (2023-03-13) Jevkalk -- `` display [`***`] ``. This is based on Djevko. To implement that, Jevkalk would need to be ported into Djevko (perhaps resulting in Djevkalk).

As I am porting these snippets, likely more and more novel syntax will be introduced. I will try to always include a note when this happens.

At some point, if the gods decide it good, I shall implement all these noveltes into the language.

```
define [timed prime test [n]
  newline []
  display [n]
  start prime test [[n] runtime []]
]

define [start prime test [[n][start time]]
  ? [
    prime? [n] report prime [- [runtime [] [start time]]]
  ]
]

define [report prime [elapsed time]
  display [`***`]
  display [elapsed time]
]
```

## 55

```
define [expmod [[base][exp][m]]
  ? [
    = [[exp][0]] [1]
    even? [exp] remainder [
      * [
        expmod [[base] / [[exp][2]] [m]]
        expmod [[base] / [[exp][2]] [m]]
      ]
      [m]
    ]
    remainder [
      * [[base] expmod [[base] - [[exp][1]] [m]]]
      [m]
    ]
  ]
]
```

## 56

```
define [cube [x]
  * [[x][x][x]]
]

* [[3][3][3]]
* [[x][x][x]]
* [[y][y][y]]
```

## 57

```
define [sum integers [[a][b]]
  ? [
    > [[a][b]] [0]
    + [[a] sum integers [+ [[a][1]] [b]]]
  ]
]

define [sum cubes [[a][b]]
  ? [
    > [[a][b]] [0]
    + [cube [a] sum cubes [+ [[a][1]] [b]]]
  ]
]

define [pi sum [[a][b]]
  ? [
    > [[a][b]] [0]
    + [
      / [[1.0] * [[a] + [[a][2]]]]
      pi sum [+ [[a][4]] [b]]
    ]
  ]
]
```

## 58

```
define [<name> [[a][b]]
  ? [
    > [[a][b]] [0]
    + [
      <term> [a]
      <name> [<next> [a] [b]]
    ]
  ]
]

define [sum [[term][a][next][b]]
  ? [
    > [[a][b]] [0]
    + [term [a] sum [[term] next [a] [next] [b]]]
  ]
]

define [inc [n]
  + [[n][1]]
]
```

## 59

```
define [sum cubes [[a][b]]
  sum [[cube][a][inc][b]]
]

sum cubes [[1][10]]

define [identity [x] [x]]

define [sum integers [[a][b]]
  sum [[identity][a][inc][b]]
]

sum integers [[1][10]]

define [pi sum [[a][b]]
  define [pi term [x]
    / [[1.0] * [[x] + [[x][2]]]]
  ]
  define [pi next [x]
    + [[x][4]]
  ]
  sum [[pi term][a][pi next][b]]
]

* [[8] pi sum [[1][1000]]]
```

## 60

```
define [integral [[f][a][b][dx]]
  define [add dx [x] + [[x][dx]]]
  * [
    sum [[f] + [[a] / [[dx][2.0]]] [add dx] [b]]
    [dx]
  ]
]

integral [[cube][0][1][0.01]]

integral [[cube][0][1][0.001]]

define [sum [[term][a][next][b]]
  define [iter [[a][result]]
    ? [
      [??] [??]
      iter [[??][??]]
    ]
  ]
  iter [[??][??]]
]
```

## 61

```
accumulate [[combiner][null value][term][a][next][b]]
```

## 62

```
fun [[x] + [[x][4]]]

fun [[x] / [[1.0] * [[x] + [[x][2]]]]]

define [pi sum [[a][b]]
  sum [
    fun [[x] / [[1.0] * [[x] + [[x][2]]]]]
    [a]
    fun [[x] + [[x][4]]]
    [b]
  ]
]

define [integral [[f][a][b][dx]]
  * [
    sum [
      [f]
      + [[a] / [[dx][2.0]]]
      fun [[x] + [[x][dx]]]
      [b]
    ]
    [dx]
  ]
]

fun [[<formal parameters>] <body>]

define [plus4 [x] + [[x][4]]]
```

## 63

Note: this uses `.` to invoke the value of the previous expression which is a function.

```
define [[plus4] fun [[x] + [[x][4]]]]

fun [[x] + [[x][4]]]

fun [[[x][y][z]]
  + [[x][y] square [z]]
]
.[[1][2][3]]
```

## 64

Let's see what happens if I change the style a bit in terms of spaces.

```
define[f[[x] [y]]
  define[f helper[[a] [b]]
    +[
      *[[x] square[a]]
      *[[y] [b]]
      *[[a] [b]]
    ]
  ]
  f helper[
    +[[1] *[[x] [y]]]
    -[[1] [y]]
  ]
]

define[f[[x] [y]]
  fun[[[a] [b]]
    +[
      *[[x] square[a]]
      *[[y] [b]]
      *[[a] [b]]
    ]
  ]
  .[
    +[[1] *[[x] [y]]]
    -[[1] [y]]
  ]
]
```

Introducing `let` (not in Jevkalk as of 2023-03-22).

```
define[f[[x] [y]]
  let[
    [
      [a] +[[1] *[[x] [y]]]
      [b] -[[1] [y]]
    ]
    +[
      *[[x] square[a]]
      *[[y] [b]]
      *[[a] [b]]
    ]
  ]
]
```

Note: decided to remove the brackets around var-exp pairs from the original Scheme syntax.

```
let [
  [
    <var 1> <exp 1>
    <var 2> <exp 2>
    .
    .
    .
    <var n> <exp n>
  ]
  <body>
]
```

Note: this is not in SICP, but the above code could also be written as:

```
define[f[[x] [y]]
  define[[a] +[[1] *[[x] [y]]]]
  define[[b] -[[1] [y]]]
  +[
    *[[x] square[a]]
    *[[y] [b]]
    *[[a] [b]]
  ]
]
```

## 65

```
fun[
  [[<var 1>]...[<var n>]]
  <body>
]
.[
  [<exp 1>]
  .
  .
  .
  [<exp n>]
]

+[
  let[
    [[x] [3]]
    +[[x] *[[x] [10]]]
  ]
  [x]
]

let[
  [
    [x] [3]
    [y] +[[x] [2]]
  ]
  *[[x] [y]]
]
```

The first expression could also be written in Jevkalk using `ap`:

```
ap[
  fun[
    [[<var 1>]...[<var n>]]
    <body>
  ][
    [<exp 1>]
    .
    .
    .
    [<exp n>]
  ]
]
```

Perhaps there is a better name for that construct.

## 66

Turns out this is in SICP after all. :D

```
define[f[[x] [y]]
  define[[a] +[[1] *[[x] [y]]]]
  define[[b] -[[1] [y]]]
  +[
    *[[x] square[a]]
    *[[y] [b]]
    *[[a] [b]]
  ]
]
```

```
define[f[g]
  g[2]
]

f[square]

f[fun[[z] *[[z] +[[z][1]]]]]
```

## 67

```
define[
  search[
    [[f] [neg point] [pos point]]
    let[
      [
        [midpoint] average[[neg point] [pos point]]
      ]
      ?[
        close enough?[[neg point] [pos point]] [midpoint]
        let[
          [
            [test value] f[midpoint]
          ]
          ?[
            positive?[test value] search[[f] [neg point] [midpoint]]
            negative?[test value] search[[f] [midpoint] [pos point]]
            [midpoint]
          ]
        ]
      ]
    ]
  ]
]
```

## 68

```
define[close enough?[[x] [y]]
  <[abs[-[[x] [y]]] [0.001]]
]
```

Seeing what happens if I introduce more spacing inside brackets.

```
define[ half interval method[ [f] [a] [b] ]
  let[
    [
      [a value] f[a]
      [b value] f[b]
    ]
    ?[
      and[
        negative?[a value]
        positive?[b value]
      ] 
      search[ [f] [a] [b] ]
      
      and[
        negative?[b value]
        positive?[a value]
      ] 
      search[ [f] [b] [a] ]
      
      error[ ['Values are not of opposite sign'] [a] [b] ]
    ]
  ]
]

half interval method[ [sin] [2.0] [4.0] ]

half interval method[ 
  fun[ [x] -[ *[ [x] [x] [x] ] ] *[ [2] [x] ] [3] ]
  [1.0]
  [2.0]
]
```

## 69

A little more vertical and horizontal spacing.

```
define[ [tolerance] [0.00001] ]

define[ 
  fixed point[ [f] [first guess] ]
  define[ 
    close enough?[ [v1] [v2] ]
    <[   abs[  -[ [v1] [v2] ]  ]   [tolerance]   ]
  ]
  define[ 
    try[guess]
    let[
      [
        [next] f[guess]
      ]
      ?[
        close enough?[ [guess] [next] ]   [next]
        try[next]
      ]
    ]
  ]
  try[first guess]
]
```

```
fixed point[ [cos] [1.0] ]

fixed point[ 
  fun[  [y]  +[ sin[y] cos[y] ]  ]
  [1.0] 
]

define[
  sqrt[x]
  fixed point[
    fun[  [y]  /[ [x] [y] ]  ]
    [1.0]
  ]
]
```

## 70

```
define [
  sqrt[x]
  fixed point [
    fun [
      [x] 
      average[ 
        [y] 
        /[ [x] [y] ] 
      ] 
    ]
    [1.0]
  ]
]
```

## 71

```
cont frac[
  fun[ [i] [1.0] ]
  fun[ [i] [1.0] ]
  [k]
]
```

## 72

```
define[
  average damp[f]
  fun [
    [x]
    average[ [x] f[x] ]
  ]
]
```

## 73

```
ap[ average damp[square][10] ]

define[
  sqrt[x]
  fixed point[
    average damp[
      fun[  [y]  /[ [x] [y] ]  ]
    ]
    [1.0]
  ]
]

define[
  cube root[x]
  fixed point[
    average damp[
      fun[  [y]  /[ [x] square[y] ]  ]
    ]
    [1.0]
  ]
]
```

## 74

```
define[
  deriv[g]
  fun[
    [x]
    /[
      -[  g[+[ [x] [dx] ]]  g[x]  ]
      [dx]
    ]
  ]
]

define[ [dx] [0.00001] ]

define[
  cube[x]
  *[ [x] [x] [x] ]
]

ap[ deriv[cube][x] ]

define[
  newton transform[g]
  fun[
    [x]
    -[ 
      [x]
      /[ g[x] ap[deriv[g][x]] ]
    ]
  ]
]
```

## 75

```
define[
  newton's method[ [g] [guess] ]
  fixed point[ newton transform[g] [guess] ]
]

define [
  sqrt[x]
  newton's method[
    fun[  [y]  -[ square[y] [x] ]  ]
    [1.0]
  ]
]

define[
  fixed point of transform[ [g] [transform] [guess] ]
  fixed point[ transform[g] [guess] ]
]

define[
  sqrt[x]
  fixed point of transform[
    fun[  [y]  /[ [x] [y] ]  ]
    [average damp]
    [1.0]
  ]
]
```

Alternative syntax for lambdas I've been thinking about:

```
define[
  deriv[g]
  [
    fun[x]
    /[
      -[  g[+[ [x] [dx] ]]  g[x]  ]
      [dx]
    ]
  ]
]

define[
  newton transform[g]
  [
    fun[x]
    -[ 
      [x]
      /[ g[x] ap[deriv[g][x]] ]
    ]
  ]
]

define [
  sqrt[x]
  newton's method[
    [  fun[y]  -[ square[y] [x] ]  ]
    [1.0]
  ]
]

define[
  sqrt[x]
  fixed point of transform[
    [  fun[y]  /[ [x] [y] ]  ]
    [average damp]
    [1.0]
  ]
]
```

So:

```
fun[  [y]  -[ square[y] [x] ]  ]
```

would become:

```
[  fun[y]  -[ square[y] [x] ]  ]
```

this could technically become:

```
[  [y]  -[ square[y] [x] ]  ]
```

dropping the `fun` "keyword" completely.

Fun to think about.

## 76

Note: using the proposed new syntax for lambdas.

```
define[
  sqrt[x]
  fixed point of transform[
    [  fun[y]  -[ square[y] [x] ]  ]
    [newton transform]
    [1.0]
  ]
]
```

## 77

```
newton's method[  cubic[ [a] [b] [c] ]  [1]  ]

ap[ double[double[double]][inc][5] ]

ap[  compose[ [square] [inc] ][5]  ]

ap[  repeated[ [square] [2] ][5]  ]
```

Technically, could get rid of the `ap` "keyword" as well:

```
[ double[double[double]][inc][5] ]

[  compose[ [square] [inc] ][5]  ]

[  repeated[ [square] [2] ][5]  ]
```

But that feels like going too far.

## 81

```
define[
  linear combination[ [a] [b] [x] [y] ]
  +[  *[ [a] [x] ]  *[ [b] [y] ]  ]
]

define[
  linear combination[ [a] [b] [x] [y] ]
  add[  mul[ [a] [x] ]  mul[ [b] [y] ]  ]
]
```

## 84

```
define[
  add rat[ [x] [y] ]
  make rat[
    +[
      *[ numer[x] denom[y] ]
      *[ numer[y] denom[x] ]
    ]
    *[ denom[x] denom[y] ]
  ]
]

define[
  sub rat[ [x] [y] ]
  make rat[
    -[
      *[ numer[x] denom[y] ]
      *[ numer[y] denom[x] ]
    ]
    *[ denom[x] denom[y] ]
  ]
]

define[
  mul rat[ [x] [y] ]
  make rat[
    *[ numer[x] numer[y] ]
    *[ denom[x] denom[y] ]
  ]
]

define[
  div rat[ [x] [y] ]
  make rat[
    *[ numer[x] denom[y] ]
    *[ denom[x] numer[y] ]
  ]
]

define[
  equal rat?[ [x] [y] ]
  =[
    *[ numer[x] denom[y] ]
    *[ numer[y] denom[x] ]
  ]
]
```

## 85

Classic Lisp pairs (cons, car, cdr).

```
define[  [x]  cons[ [1] [2] ]  ]

car[x]

cdr[x]

define[  [x]  cons[ [1] [2] ]  ]

define[  [y]  cons[ [3] [4] ]  ]

define[  [z]  cons[ [x] [y] ]  ]

car[ car[z] ]

car[ cdr[z] ]
```

Less classic aliases (pair, fst, snd).

```
define[  [x]  pair[ [1] [2] ]  ]

fst[x]

snd[x]

define[  [x]  pair[ [1] [2] ]  ]

define[  [y]  pair[ [3] [4] ]  ]

define[  [z]  pair[ [x] [y] ]  ]

fst[ fst[z] ]

snd[ snd[z] ]
```

## 86

```
define[
  make rat[ [n] [d] ]
  cons[ [n] [d] ]
]

define[ numer[x] car[x] ]

define[ denom[x] cdr[x] ]

define[
  print rat[x]
  newline[]
  display[ numer[x] ]
  display['/']
  display[ denom[x] ]
]

define[  [one half]  make rat[ [1] [2] ]  ]

print rat[one half]

define[  [one third]  make rat[ [1] [3] ]  ]

define[ [make rat] [cons] ]
define[ [numer] [car] ]
define[ [denom] [cdr] ]
```

## 87

```
print rat[  add rat[ [one half] [one third] ]  ]

print rat[  mul rat[ [one half] [one third] ]  ]

print rat[  add rat[ [one third] [one third] ]  ]

define[
  make rat[ [n] [d] ]
  let[
    [  [g]  gcd[ [n] [d] ]  ]
    cons[  /[ [n] [g] ]  /[ [d] [g] ]  ]
  ]
]

print rat[  add rat[ [one thrid] [one third] ]  ]
```

## 89

```
define[
  make rat[ [n] [d] ]
  cons[ [n] [d] ]
]

define[
  numer[x]
  let[
    [  [g]  gcd[ car[x] cdr[x] ]  ]
    /[ car[x] [g] ]
  ]
]

define[
  denom[x]
  let[
    [  [g]  gcd[ car[x] cdr[x] ]  ]
    /[ cdr[x] [g] ]
  ]
]
```

## 90

```
define[
  print point[p]
  newline[]
  display['(']
  display[ x point[p] ]
  display[',']
  display[ y point[p] ]
  display[')']
]
```

## 91

```
define[
  cons[ [x] [y] ]
  define[
    dispatch[m]
    ?[
      =[ [m] [0] ] [x]
      =[ [m] [1] ] [y]
      error[ ['Argument not 0 or 1 -- CONS'] [m] ]
    ]
  ]
  [dispatch]
]

define[ car[z] z[0] ]

define[ cdr[z] z[1] ]
```

## 92

```
define[
  cons[ [x] [y] ]
  fun[  [m]  m[ [x] [y] ]  ]
]

define[
  car[z]
  z[
    fun[  [ [p] [q] ]  [p]  ]
  ]
]
```

## 93

```
define[  [zero]  fun[ [f] fun[ [x] [x] ] ]  ]

define [ 
  add 1[n]
  fun[  [f]  fun[ [x] f[ ap[n[f][x]] ] ]  ]
]
```

## 94

```
define[
  add interval[ [x] [y] ]
  make interval[
    +[ lower bound[x] lower bound[y] ]
    +[ upper bound[x] upper bound[y] ]
  ]
]
```

Another take on `let`. Losing a pair of brackets in exchange for only one expression in body.

```
define[
  mul interval[ [x] [y] ]
  let[
    [p1]  *[ lower bound[x] lower bound[y] ]
    [p2]  *[ lower bound[x] upper bound[y] ]
    [p3]  *[ upper bound[x] lower bound[y] ]
    [p4]  *[ upper bound[x] upper bound[y] ]
    make interval[
      min[ [p1] [p2] [p3] [p4] ]
      max[ [p1] [p2] [p3] [p4] ]
    ]
  ]
]

define[
  div interval[ [x] [y] ]
  mul interval[
    [x]
    make interval[
      /[ [1.0] upper bound[y] ]
      /[ [1.0] lower bound[y] ]
    ]
  ]
]

define[
  make interval[ [a] [b] ]
  cons[ [a] [b] ]
]
```

## 95

```
define[
  make center width[ [c] [w] ]
  make interval[
    -[ [c] [w] ]
    +[ [c] [w] ]
  ]
]

define[
  center[i]
  /[  +[ lower bound[i] upper bound[i] ]  [2]  ]
]

define[
  width[i]
  /[  -[ upper bound[i] lower bound[i] ]  [2]  ]
]
```

## 96

```
define[
  par1[ [r1] [r2] ]
  div interval[
    mul interval[ [r1] [r2] ]
    add interval[ [r1] [r2] ]
  ]
]

define[
  par2[ [r1] [r2] ]
  let[
    [one]  make interval[ [1] [1] ]
    div interval[
      [one]
      add interval[
        div interval[ [one] [r1] ]
        div interval[ [one] [r2] ]
      ]
    ]
  ]
]
```

## 98

```
cons[
  cons[ [1] [2] ]
  cons[ [3] [4] ]
]

cons[
  cons[
    [1]
    cons[ [2] [3] ]
  ]
  [4]
]
```

## 99

```
cons[
  [1]
  cons[
    [2]
    cons[
      [3]
      cons[ [4] [nil] ]
    ]
  ]
]
```

## 100

```
list[ [<a_1>] [<a_2>] ... [<a_n>] ]

cons[
  [<a_1>]
  cons[
    [<a_2>]
    cons[
      ...
      cons[
        [<a_n>]
        [nil]
      ]
      ...
    ]
  ]
]

define[
  [one through four]
  list[ [1] [2] [3] [4] ]
]

[one through four]

car[one through four]

cdr[one through four]
```

```
cadr[<arg>] = car[ cdr[<arg>] ]
```

## 101

```
car[ cdr[one through four] ]

cons[ [10] [one through four] ]

cons[ [5] [one through four] ]

define[
  list ref[ [items] [n] ]
  ?[
    =[ [n] [0] ]  car[items]
    list ref[
      cdr[items]
      -[ [n] [1] ]
    ]
  ]
]

define[
  [squares]
  list[ [1] [4] [9] [16] [25] ]
]

list ref[ [squares] [3] ]
```

## 102

```
define[
  length[items]
  ?[
    null?[items] [0]
    +[  [1]  length[ cdr[items] ]  ]
  ]
]

define[
  [odds]
  list[ [1] [3] [5] [7] ]
]

length[odds]

define[
  length[items]
  define[
    length iter[ [a] [count] ]
    ?[
      null?[a] [count]
      length iter[
        cdr[a]
        +[ [1] [count] ]
      ]
    ]
  ]
  length iter[ [items] [0] ]
]

append[ [squares] [odds] ]

append[ [odds] [squares] ]
```

## 103

```
define[
  append[ [list1] [list2] ]
  ?[
    null?[list1] [list2]
    cons[
      car[list1]
      append[ cdr[list1] [list2] ]
    ]
  ]
]

last pair[  list[ [23] [72] [149] [34] ]  ]

reverse[  list[ [1] [4] [9] [16] [25] ] ]

define[
  [us coins]
  list[ [50] [25] [10] [5] [1] ]
]

define[
  [uk coins]
  list[ [100] [50] [20] [10] [5] [2] [1] [0.5] ]
]

cc[ [100] [us coins] ]
```

## 104

```
define[
  cc[ [amount] [coin value] ]
  ?[
    =[ [amount] [0] ]  [1]
    or[  <[ [amount] [0] ]  no more?[coin values]  ]   [0]
    +[
      cc[
        [amount]
        except first denomination[coin values]
      ]
      cc[
        -[
          [amount]
          first denomination[coin values]
        ]
        [coin values]
      ]
    ]
  ]
]
```

Figuring out the equivalent of the dotted-tail notation. Using a JavaScript-style rest parameter syntax.

```
define[
  f[ [x] [y] ...[z] ]
  <body>
]

f[ [1] [2] [3] [4] [5] [6] ]

define[
  g[ ...[w] ]
  <body>
]

g[ [1] [2] [3] [4] [5] [6] ]

same parity[ [1] [2] [3] [4] [5] [6] [7] ]

same parity[ [2] [3] [4] [5] [6] [7] ]

define[
  [f]
  fun[
    [ [x] [y] ...[z] ]
    <body>
  ]
]

define[
  [g]
  fun[
    [ ...[w] ]
    <body>
  ]
]
```

## 105

```
define[
  scale list[ [items] [factor] ]
  ?[
    null?[items] [nil]
    cons[
      *[ car[items] [factor] ]
      scale list[ cdr[items] [factor] ]
    ]
  ]
]

scale list[
  list[ [1] [2] [3] [4] [5] [6] ]
  [10]
]

define[
  map[ [proc] [items] ]
  ?[
    null?[items] [nil]
    cons[
      proc[ car[items] ]
      map[ [proc] cdr[items] ]
    ]
  ]
]

map[  [abs]  list[ [-10] [2.5] [-11.6] [17] ]  ]

map[
  fun[  [x]  *[ [x] [x] ]  ]
  list[ [1] [2] [3] [4] ]
]

map[
  [+]
  list[ [1] [2] [3] ]
  list[ [40] [50] [60] ]
  list[ [700] [800] [900] ]
]

map[
  fun[
    [ [x] [y] ]
    +[  [x]  *[ [2] [y] ]  ]
  ]
  list[ [1] [2] [3] ]
  list[ [4] [5] [6] ]
]
```

## 106

```
define[
  scale list[ [items] [factor] ]
  map[
    fun[  [x]  *[ [x] [factor] ]  ]
    [items]
  ]
]

square list[  list[ [1] [2] [3] [4] ]  ]

define[
  square list[items]
  ?[
    null?[items] [nil]
    cons[ [??] [??] ]
  ]
]

define[
  square list[items]
  map[ [??] [??] ]
]
```

## 107

```
define[
  square list[items]
  define[
    iter[ [things] [answer] ]
    ?[
      null?[things] [answer]
      iter[
        cdr[things]
        cons[
          square[ car[things] ]
          [answer]
        ]
      ]
    ]
  ]
  iter[ [items] [nil] ]
]

define[
  square list[items]
  define[
    iter[ [things] [answer] ]
    ?[
      null?[things] [answer]
      iter[
        cdr[things]
        cons[
          [answer]
          square[ car[things] ]
        ]
      ]
    ]
  ]
  iter[ [items] [nil] ]
]

for each[
  fun[ [x] newline[] display[x] ]
  list[ [57] [321] [88] ]
]

cons[
  list[ [1] [2] ]
  list[ [3] [4] ]
]
```

## 108

```
define[
  [x]
  cons[
    list[ [1] [2] ]
    list[ [3] [4] ]
  ]
]

length[x]
```

## 109

```
count leaves[x]

list[ [x] [x] ]

length[
  list[ [x] [x] ]
]

count leaves[
  list[ [x] [x] ]
]

define[
  count leaves[x]
  ?[
    null?[x] [0]
    not[ pair?[x] ]  [1]
    +[
      count leaves[ car[x] ]
      count leaves[ cdr[x] ]
    ]
  ]
]
```

## 110

I'm thinking maybe representations of lists/jevkos as data should have `'` in front, to be valid also as code.

```
'[  [1]  [3]  [ [5] [7] ]  [9]  ]

'[ [7] ]

'[[1] [[2] [[3] [[4] [[5] [[6] [7]]]]]]]
```

```
define[
  [x]
  list[ [1] [2] [3] ]
]

define[
  [y]
  list[ [4] [5] [6] ]
]

append[ [x] [y] ]

cons[ [x] [y] ]

list[ [x] [y] ]

define[
  [x]
  list[  list[ [1] [2] ]  list[ [3] [4] ]  ]
]

[x]

reverse[x]

deep reverse[x]
```

NB there should be native functions like:

```
jevko[ [subjevkos] [suffix] ]
subjevko[ [prefix] [jevko] ]
```

where `subjevkos` is a list, not necessarily a linked list (TBD).

## 111

```
define[
  [x]
  list[  list[ [1] [2] ]  list[ [3] [4] ]  ]
]

fringe[x]

fringe[  list[ [x] [x] ]  ]

define[
  make mobile[ [left] [right] ]
  list[ [left] [right] ]
]

define[
  make branch[ [length] [structure] ]
  list[ [length] [structure] ]
]

define[
  make mobile[ [left] [right] ]
  cons[ [left] [right] ]
]

define[
  make branch[ [length] [structure] ]
  cons[ [length] [structure] ]
]
```

## 112

Going a little wild with the formatting.

```
define[
  scale tree[ [tree] [factor] ]
  ?[
    null?[tree] [nil]
    not[pair?[tree]]  *[ [tree] [factor] ]
    cons[
      scale tree[ car[tree] [factor] ]
      scale tree[ cdr[tree] [factor] ]
    ]
  ]
]

scale tree[
  list[
    [1] list[
      [2] list[
        [3] [4]
      ]
      [5]
    ] list[
      [6] [7]
    ]
  ]
  [10]
]

define[
  scale tree[ [tree] [factor] ]
  map[
    fun[ [sub tree]
      ?[
        pair?[sub tree]  scale tree[ [sub tree] [factor] ]
        *[ [sub tree] [factor] ]
      ]
    ]
    [tree]
  ]
]

square tree[
  list[ [1]
    list[ [2]
      list[ [3] [4] ]
      [5]
    ] list[
      [6] [7]
    ]
  ]
]
```

## 113

```
define[  square tree[tree]  tree map[ [square] [tree] ]  ]

define[
  subsets[s]
  ?[
    null?[s]  list[nil]
    let[
      [rest]  subsets[cdr[s]]
      append[
        [rest]
        map[ [??] [rest] ]
      ]
    ]
  ]
]

define[
  sum odd squares[tree]
  ?[
    null?[tree]  [0]
    not[pair?[tree]] ?[
      odd?[tree] square[tree]
      [0]
    ]
    +[
      sum odd squares[ car[tree] ]
      sum odd squares[ cdr[tree] ]
    ]
  ]
]
```

## 114

```
define[
  even fibs[n]
  define[
    next[k]
    ?[
      >[ [k] [n] ]  [nil]
      let[
        [f]  fib[k]
        ?[
          even?[f]  cons[
            [f]
            next[  +[ [k] [1] ]  ]
          ]
          next[  +[ [k] [1] ]  ]
        ]
      ]
    ]
  ]
  next[0]
]
```

## 115

```
map[
  [square]
  list[ [1] [2] [3] [4] [5] ]
]

define[
  filter[ [predicate] [sequence] ]
  ?[
    null?[sequence] [nil]
    predicate[ car[sequence] ]  cons[
      car[sequence]
      filter[
        [predicate]
        cdr[sequence]
      ]
    ]
    filter[
      [predicate]
      cdr[sequence]
    ]
  ]
]
```

## 116

```
filter[
  [odd?]
  list[ [1] [2] [3] [4] ]
]

define[
  accumulate[ [op] [initial] [sequence] ]
  ?[
    null?[sequence] [initial]
    op[
      car[sequence]
      accumulate[
        [op]
        [initial]
        cdr[sequence]
      ]
    ]
  ]
]

accumulate[
  [+]
  [0]
  list[ [1] [2] [3] [4] [5] ]
]

accumulate[
  [*]
  [1]
  list[ [1] [2] [3] [4] [5] ]
]

accumulate[
  [cons]
  [nil]
  list[ [1] [2] [3] [4] [5] ]
]

define[
  enumerate interval[ [low] [high] ]
  ?[
    >[ [low] [high] ]  [nil]
    cons[
      [low]
      enumerate interval[
        +[ [low] [1] ]
        [high]
      ]
    ]
  ]
]

enumerate interval[ [2] [7] ]

define[
  enumerate tree[tree]
  ?[
    null?[tree] [nil]
    not[pair?[tree]]  list[tree]
    append[
      enumerate tree[ car[tree] ]
      enumerate tree[ cdr[tree] ]
    ]
  ]
]

enumerate tree[
  list[ [1] list[ [2] list[ [3] [4] ]] [5] ]
]
```

## 117

```
define[
  sum odd squares[tree]
  accumulate[
    [+]
    [0]
    map[
      [square]
      filter[
        [odd?]
        enumerate tree[tree]
      ]
    ]
  ]
]

define[
  even fibs[n]
  accumulate[
    [cons]
    [nil]
    filter[
      [even?]
      map[
        [fib]
        enumerate interval[ [0] [n] ]
      ]
    ]
  ]
]

define[
  list fib squares[n]
  accumulate[
    [cons]
    [nil]
    map[
      [square]
      map[
        [fib]
        enumerate interval[ [0] [n] ]
      ]
    ]
  ]
]

list fib squares[10]
```

## 118

```
define[
  product of squares of odd elements[sequence]
  accumulate[
    [*]
    [1]
    map[
      [square]
      filter[ [odd?] [sequence] ]
    ]
  ]
]

product of squares of odd elements[
  list[ [1] [2] [3] [4] [5] ]
]

define[
  salary of highest paid programmer[records]
  accumulate[
    [max]
    [0]
    map[
      [salary]
      filter[
        [programmer?]
        [records]
      ]
    ]
  ]
]
```

## 119

```
define[
  map[ [p] [sequence] ]
  accumulate[
    fun[  [ [x] [y] ]  [??]  ]
    [nil]
    [sequence]
  ]
]

define[
  append[ [seq1] [seq2] ]
  accumulate[ [cons] [??] [??] ]
]

define[
  length[sequence]
  accumulate[ [??] [0] [sequence] ]
]

define[
  horner eval[ [x] [coefficient sequence] ]
  accumulate[
    fun[  [ [this coeff] [higher terms] ]  [??]  ]
    [0]
    [coefficient sequence]
  ]
]

horner eval[
  [2]
  list[ [1] [3] [0] [5] [0] [1] ]
]
```

## 120

```
define[
  count leaves[t]
  accumulate[
    [??]
    [??]
    map[ [??] [??] ]
  ]
]

define[
  accumulate n[ [op] [init] [seqs] ]
  ?[
    null?[car[seqs]]  [nil]
    cons[
      accumulate[ [op] [init] [??] ]
      accumulate n[ [op] [init] [??] ]
    ]
  ]
]

dot product[ [v] [w] ]

matrix * vector[ [m] [v] ]

matrix * matrix[ [m] [n] ]

transpose[m]
```

## 121

```
define[
  dot product[ [v] [w] ]
  accumulate[  [+]  [0]  map[ [*] [v] [w] ]  ]
]

define[
  matrix * vector[ [m] [v] ]
  map[ [??] [m] ]
]

define[
  transpose[mat]
  accumulate n[ [??] [??] [mat] ]
]

define[
  matrix * matrix[ [m] [n] ]
  let[
    [cols] transpose[n]
    map[ [??] [m] ]
  ]
]

define[
  fold left[ [op] [initial] [sequence] ]
  define[
    iter[ [result] [rest] ]
    ?[
      null?[rest]  [result]
      iter[
        op[ [result] car[rest] ]
        cdr[rest]
      ]
    ]
  ]
  iter[ [initial] [sequence] ]
]

fold right[  [/]  [1]  list[ [1] [2] [3] ]  ]

fold left[  [/]  [1]  list[ [1] [2] [3] ]  ]

fold right[  [list]  [nil]  list[ [1] [2] [3] ]  ]

fold left[  [list]  [nil]  list[ [1] [2] [3] ]  ]
```

## 122

```
define[
  reverse[sequence]
  fold right[
    fun[
      [ [x] [y] ]
      [??]
    ]
    [nil]
    [sequence]
  ]
]

define[
  reverse[sequence]
  fold left[
    fun[
      [ [x] [y] ]
      [??]
    ]
    [nil]
    [sequence]
  ]
]
```

## 123

```
accumulate[
  [append]
  [nil]
  map[
    fun[ [i]
      map[
        fun[ [j]
          list[ [i] [j] ]
        ]
        enumerate interval[  [1]  -[ [i] [1] ]  ]
      ]
    ]
    enumerate interval[ [1] [n] ]
  ]
]

define[
  flatmap[ [proc] [seq] ]
  accumulate[  [append]  [nil]  map[ [proc] [seq] ]  ]
]

define[
  prime sum?[pair]
  prime?[
    +[ car[pair] cadr[pair] ]
  ]
]

define[
  make pair sum[pair]
  list[
    car[pair]
    cadr[pair]
    +[
      car[pair]
      cadr[pair]
    ]
  ]
]

define[
  prime sum pairs[n]
  map[
    [make pair sum]
    filter[
      [prime sum?]
      flatmap[
        fun[ [i]
          map[
            fun[ [j]
              list[ [i] [j] ]
            ]
            enumerate interval[ [1] -[[i][1]] ]
          ]
        ]
        enumerate interval[ [1] [n] ]
      ]
    ]
  ]
]
```

## 124

```
define[
  permutations[s]
  ?[
    null?[s] list[nil]
    flatmap[
      fun[ [x]
        map[
          fun[ [p]
            cons[ [x] [p] ]
          ]
          permutations[
            remove[ [x] [s] ]
          ]
        ]
      ]
      [s]
    ]
  ]
]

define[
  remove[ [item] [sequence] ]
  filter[
    fun[ [x]
      not[=[ [x] [item] ]]
    ]
    [sequence]
  ]
]
```

## 125

```
define[
  queens[board size]
  define[
    queen cols[k]
    ?[
      =[ [k] [0] ]  list[empty board]
      filter[
        fun[ [positions]
          safe?[ [k] [positions] ]
        ]
        flatmap[
          fun[ [rest of queens]
            map[
              fun[ [new row]
                adjoin position[ [new row] [k] [rest of queens] ]
              ]
              enumerate interval[ [1] [board size] ]
            ]
          ]
          queen cols[-[ [k] [1] ]]
        ]
      ]
    ]
  ]
  queen cols[board size]
]
```

## 126

```
flatmap[
  fun[ [new row]
    map[
      fun[ [rest of queens]
        adjoin position[ [new row] [k] [rest of queens] ]
      ]
      queen cols[-[ [k] [1] ]]
    ]
  ]
  enumerate interval[ [1] [board size] ]
]
```

## 128

```
define[ [wave2]
  beside[ [wave] flip vert[wave] ]
]

define[ [wave4]
  below[ [wave2] [wave2] ]
]
```

## 130

```
define[
  flipped pairs[painter]
  let[
    [painter2]  beside[ [painter] flip vert[painter] ]
    below[ [painter2] [painter2] ]
  ]
]

define[ [wave4] flipped pairs[wave] ]
```

## 131

```
define[  right split[ [painter] [n] ]
  ?[
    =[ [n] [0] ]  [painter]
    let[
      [smaller]
        right split[  [painter]  -[ [n] [1] ]  ]
      beside[  [painter]  below[ [smaller] [smaller] ]  ]
    ]
  ]
]
```

## 132

```
define[
  corner split[ [painter] [n] ]
  ?[
    =[ [n] [0] ]  [painter]
    let[
      [up]  up split[ [painter] -[[n][1]] ]
      [right]  right split[ [painter] -[[n][1]] ]
      let[
        [top left]  beside[ [up] [up] ]
        [bottom right]  below[ [right] [right] ]
        [corner]  corner split[ [painter] -[[n][1]] ]
        beside[
          below[ [painter] [top left] ]
          below[ [bottom right] [corner] ]
        ]
      ]
    ]
  ]
]

define[
  square limit[ [painter] [n] ]
  let[
    [quarter]  corner split[ [painter] [n] ]
    let[
      [half]  beside[ flip horiz[quarter] [quarter] ]
      below[ flip vert[half] [half] ]
    ]
  ]
]

define[
  square of four[ [tl] [tr] [bl] [br] ]
  fun[ [painter] 
    let[
      [top]  beside[ tl[painter] tr[painter] ]
      [bottom]  beside[ bl[painter] br[painter] ]
      below[ [bottom] [top] ]
    ]
  ]
]
```

## 133

```
right split[ [wave] [4] ]

right split[ [rogers] [4] ]

corner split[ [wave] [4] ]

corner split[ [rogers] [4] ]

define[ [flipped pairs]
  square of four[ [identity] [flip vert] [identity] [flip vert] ]
]
```

## 134

```
define[ flipped pairs[painter]
  let[
    [combine4]  square of four[ [identity] [flip vert] [identity] [flip vert] ]
    combine4[painter]
  ]
]

define[  square limit[ [painter] [n] ]
  let[
    [combine4]  square of four[ [flip horiz] [identity] [rotate180] [flip vert] ]
    combine4[corner split[ [painter] [n] ]]
  ]
]

define[  [right split]  split[ [beside] [below] ]  ]
define[  [up split]  split[ [below] [beside] ]  ]
```

## 135

```
define[  frame coord map[frame]
  fun[ [v]
    add vect[
      origin frame[frame]
      add vect[  
        scale vect[ xcor vect[v] edge1 frame[frame] ]
        scale vect[ ycor vect[v] edge2 frame[frame] ]
      ]
    ]
  ]
]
```

## 136

```
ap[
  frame coord map[a frame]
  [  make vect[ [0] [0] ]  ]
]

origin frame[a frame]

define[  make frame[ [origin] [edge1] [edge2] ]
  list[ [origin] [edge1] [edge2] ]
]

define[  make frame[ [origin] [edge1] [edge2] ]
  cons[  [origin]  cons[ [edge1] [edge2] ]  ]
]
```

## 137

```
define[
  segments->painter[segment list]
  fun[ [frame]
    for each[
      fun[ [segment]
        draw line[
          ap[ frame coord map[frame][start segment[segment]] ]
          ap[ frame coord map[frame][end segment[segment]] ]
        ]
      ]
      [segment list]
    ]
  ]
]
```

## 138

```
define[
  transform painter[ [painter] [origin] [corner1] [corner2] ]
  fun[ [frame]
    let[
      [m]  frame coord map[frame]
      let[
        [new origin]  m[origin]
        painter[
          make frame[
            [new origin]
            sub vect[ m[corner1] [new origin] ]
            sub vect[ m[corner2] [new origin] ]
          ]
        ]
      ]
    ]
  ]
]

define[
  flip vert[painter]
  transform painter[
    [painter]
    make vect[ [0.0] [1.0] ]   new origin
    make vect[ [1.0] [1.0] ]   new end of edge1
    make vect[ [0.0] [0.0] ]   new end of edge2 
  ]
]

define[
  shrink to upper right[painter]
  transform painter[
    [painter]
    make vect[ [0.5] [0.5] ]
    make vect[ [1.0] [0.5] ]
    make vect[ [0.5] [1.0] ]
  ]
]
```

## 139

```
define[
  rotate90[painter]
  transform painter[
    [painter]
    make vect[ [1.0] [0.0] ]
    make vect[ [1.0] [1.0] ]
    make vect[ [0.0] [0.0] ]
  ]
]

define[
  squash inwards[painter]
  transform painter[
    [painter]
    make vect[ [0.0] [0.0] ]
    make vect[ [0.65] [0.35] ]
    make vect[ [0.35] [0.65] ]
  ]
]

define[
  beside[ [painter1] [painter2] ]
  let[
    [split point]  make vect[ [0.5] [0.0] ]
    let[
      [paint left]  transform painter[
        [painter1]
        make vect[ [0.0] [0.0] ]
        [split point]
        make vect[ [0.0] [1.0] ]
      ]
      [paint right]  transform painter[
        [painter2]
        [split point]
        make vect[ [1.0] [0.0] ]
        make vect[ [0.5] [1.0] ]
      ]
      fun[ [frame]
        paint left[frame]
        paint right[frame]
      ]
    ]
  ]
]
```

## 142

### Introducing Quotation!

So here we're using S-expressions not to write MIT Scheme, but to encode some lists. Similarly, the first two lists could be sensibly translated to Jevko (as opposed to Jevkalk) as:

```
[ [a] [b] [c] [d] ]

[ [23] [45] [17] ]
```

The third list could be:

```
[  [ [Norah] [12] ]  [ [Molly] [9] ]  [ [Anna] [7] ]  [ [Lauren] [6] ]  [ [Charlotte] [4] ]  ]
```

or, more succinctly:

```
[ Norah[12] Molly[9] Anna[7] Lauren[6] Charlotte[4] ]
```

Now the following two S-expressions are also meant to be just S-expressions (and not code), but happen to look like Scheme. So our translation will look like Jevkalk (but is meant to be just Jevko):

```
*[  +[ [23] [45] ]  +[ [x] [9] ]  ]

define[ fact[n]
  ?[
    =[ [n] [1] ]  [1]
    *[  [n]  fact[ -[[n][1]] ]  ]
  ]
]
```

## 143

```
define[ [a] [1] ]

define[ [b] [2] ]

list[ [a] [b] ]

list[ '[a] '[b] ]

list[ '[a] [b] ]
```

Note: we don't need separate `quote[...]`.

## 144

Now, a somewhat naive translation of the code at the top of the page would be:

```
car[  '[ [a] [b] [c] ]  ]

cdr[  '[ [a] [b] [c] ]  ]
```

But this creates a problem. `car` and `cdr` are well-defined for lists, but not really for arbitrary jevkos.

So here we are forced to continue to flesh out the thread from page [110](#110).

One way to proceed would be to define `car` and `cdr` only for lists. So this would be valid:

```
car[  list[ [a] [b] [c] ]  ]

cdr[  list[ [a] [b] [c] ]  ]
```

While the above wouldn't. `'` would actually mean `quote` rather than `list`, like I imagined previously.

Now for quoted jevkos we would need a separate set for primitive functions for analysis.

Let's imagine how could such functions look like.

I'll leave proper naming for later. First let's make up a function `f1`, which would be somewhat like `car` and could be applied like so:

```
f1[  '[ [a] [b] [c] ]  ]
```

and for this application it would return:

```
[a]
```

Or should that be:

```
'[a]
```

? Not sure yet, let's not commit to either for the time being. Let's say it returns:

```
?[a]
```

where `?` represents the prefix being empty or equal to `'` (or maybe something else).

Now what should `f1` return for something like:

```
f1[  '[ x1[x2] y1[y2] ]  ]
```

Here I will take my reasoning process offline. I am leaving it to serve as an example of how one might go about designing something like this.

***

Upon some reflection, we may imagine the following useful functions:

```
fsj[jevko]

fsp[jevko]
```

`fsj` takes a `jevko` and returns its first subjevko's jevko, e.g.:

```
fsj[ '[x1[x2] y1[y2]] ]
```

would return

```
'[x2]
```

`fsp` takes a `jevko` and returns its first subjevko's prefix, e.g.:

```
fsp[ '[x1[x2] y1[y2]] ]
```

would return

```
'[x1]
```

Note: the prefix is returned as a jevko (perhaps it should be a string instead -- or there should be a separate function or conversion for that).

Another useful function would be `rss`:

```
rss[jevko]
```

`rss` takes a `jevko` and returns it sans the first subjevko, e.g.:

```
rss[ '[x1[x2] y1[y2]] ]
```

would return

```
'[ y1[y2]]
```

### Homoiconic output

A provisional name for a concept I've been thinking about on and off for a long time, can be defined something like:

> Homoiconic output/representation of a piece of data is the code that when executed would construct an equivalent piece of data.

Rephrased:

> A homoiconic text representation of data refers to the code that, when executed, can construct an identical replica of the original data using the smallest possible amount of code.

Something like that.

It's important to note here that most if not all languages, including MIT Scheme don't adhere to this. E.g. `(list 1 2 3)` is displayed as `(1 2 3)`. `(1 2 3)` can't be then executed to obtain the same list.

### Jevkalk-specific alternatives to `memq`

This is the original definition of `memq` translated to Jevkalk:

```
define[  memq[ [item] [x] ]
  ?[
    null?[x]  [false]
    eq?[ [item] car[x] ]  [x]
    memq[
      [item]
      cdr[x]
    ]
  ]
]
```

This won't do. We would be better served by a tailor-made equivalent or equivalents, e.g. `memj` which would use `fsj` and `rss` instead of `car` and `cdr`, `memp` which would use `fsp` and `rss`, maybe `memjp` which would use an alternative of both. Perhaps we could write a generalized `member` function in Jevkalk which would look something like this:

```
define[  member[ [item] [x] ]
  ?[
    null?[x]  [false]
    or[
      equal?[ [item] fsj[x] ]
      equal?[ [item] fsp[x] ]
    ]  [x]
    member[ [item] rss[x] ]
  ]
]
```

where `equal?` would signify generalized structural equality.

Let's translate the rest of the code with that in mind.

***

So instead of:

```
memq[  '[apple]  '[ [pear] [banana] [prune] ]  ]

memq[  '[apple]  '[ [x] apple[sauce] [y] [apple] [pear] ]  ]
```

we'd have something like:

```
memj[  '[apple]  '[ [pear] [banana] [prune] ]  ]

memj[  '[apple]  '[ [x] apple[sauce] [y] [apple] [pear] ]  ]
```

Then we have this (which is rather uncontroversial):

```
list[ '[a] '[b] '[c] ]

list[ list['[george]] ]
```

Then instead of this:

```
cdr[  '[ x1[x2] y1[y2] ]  ]
```

we'd have

```
rss[  '[ x1[x2] y1[y2] ]  ]
```

***

Now this naive translation:

```
cadr[  '[ x1[x2] y1[y2] ]  ]
```

should be this instead:

```
fsj[  '[ x1[x2] y1[y2] ]  ]
```

## 145

Just riffing here...

```
pair?[
  fsp[  '[ a[[short][list]] ]  ]
]

memj[
  '[red]
  '[ red[shoes] blue[socks] ]
]

memp[
  '[red]
  '[  red[ [shoes] [blue] [socks] ]  ]
]

equal?[
  '[  this[ [is] [a] [jevko] ]  ]
  '[  this[ [is] [a] [jevko] ]  ]
]

equal?[
  '[  this[ [is] [a] [jevko] ]  ]
  '[  this[ is[a] [jevko] ]  ]
]

fsp[ '['[abracadabra]] ]
```

## 147

```
variable?[e]

same variable?[ [v1] [v2] ]

sum?[e]

addend[e]

augend[e]

make sum[ [a1] [a2] ]

product?[e]

multiplier[e]

make product[ [m1] [m2] ]

define[  deriv[ [exp] [var] ]
  ?[
    number?[exp]  [0]
    variable?[exp]  ?[
      same variable?[ [exp] [var] ]  [1]
      [0]
    ]
    sum?[exp]  make sum[
      deriv[ addend[exp] [var] ]
      deriv[ augend[exp] [var] ]
    ]
    product?[exp]  make sum[
      make product[
        multiplier[exp]
        deriv[ multiplicand[exp] [var] ]
      ]
      make product[
        deriv[ multiplier[exp] [var] ]
        multiplicand[exp]
      ]
    ]
    error[
      [`unknown expression type -- DERIV`]
      [exp]
    ]
  ]
]
```

## 148

Note: we are assuming our expressions are lists, rather than jevkos, e.g.:

```
list[ '[+] [2] [3] ]
```

rather than

```
'[  +[ [2] [3] ]  ]
```

With that in mind, we proceed.

Now, we shall introduce the `pj?` predicate which will be used in place of `symbol?` in the definition of `variable?`:

```
define[  variable?[x]  pj?[x]  ]
```

`pj?` takes a jevko and returns `true` if it is primitive. A primitive jevko is one which does not have any subjevkos. E.g.:

```
pj?[ '[x] ]  true
pj?[ '[[a][b]] ]  false
pj?[ '[] ]  not sure; let's say true for now
```

Now we continue translating.

```
define[  same variable?[ [v1] [v2] ]
  and[
    variable?[v1]
    variable?[v2]
    eq?[ [v1] [v2] ]
  ]
]

define[  make sum[ [a1] [a2] ]  list[ '[+] [a1] [a2] ]  ]

define[  make product[ [m1] [m2] ]  list[ '[*] [m1] [m2] ]  ]

define[  sum?[x]
  and[
    pair?[x]
    eq?[ car[x] '[+] ]
  ]
]
```

Note: `cadr`, `caddr`, etc. can be defined for `list`s.

```
define[ addend[s] cadr[s] ]

define[ augend[s] caddr[s] ]

define[ product?[s]
  and[
    pair?[x]
    eq?[ car[x] '[*] ]
  ]
]

define[  multiplier[p]  cadr[p]  ]
```

### Alternative definitions

Here I introduce some functions to manipulate jevkos and make the whole thing based around jevkos rather than lists.

`'number?` checks if a jevko can be evaluated to a number (looks like a number literal).

The apostrophes in the signature of `deriv[ '[exp] '[var] ]` supress evaluation of the arguments (they are interpreted verbatim, as jevkos).

```
define[  deriv[ '[exp] '[var] ]
  ?[
    'number?[exp]  [0]
    variable?[exp]  ?[
      same variable?[ [exp] [var] ]  [1]
      [0]
    ]
    sum?[exp]  make sum[
      deriv[ addend[exp] [var] ]
      deriv[ augend[exp] [var] ]
    ]
    product?[exp]  make sum[
      make product[
        multiplier[exp]
        deriv[ multiplicand[exp] [var] ]
      ]
      make product[
        deriv[ multiplier[exp] [var] ]
        multiplicand[exp]
      ]
    ]
    error[
      [`unknown expression type -- DERIV`]
      [exp]
    ]
  ]
]
```

`name?` checks if a jevko looks like an identifier.

```
define[  variable?['[x]]  'name?[x]  ]
```

`'$` constructs jevkos and allows splicing in various parts from variables.

```
define[  make sum[ '[a1] '[a2] ]
  '$[ +[$[a1]$[a2]] ]
]

define[  make product[ '[m1] '[m2] ]
  '$[ *[$[m1]$[m2]] ]
]
```

`'nonempty?` checks if a jevko has at least one subjevko. Maybe there is a better name for this one.

`subs[jevko]` returns the list of the `jevko`'s subjevkos.

`at[list]` returns a function to select elements from the `list`. The function accepts 0-based indices. It should also work for negative indices, to select elements backwards from the end of the list (`-1` is the last element).

`prefix[subjevko]` returns the `subjevko`'s prefix as text.

`.` is a placeholder variable that always holds the value of the previous expression.

```
define[  sum?['[x]]
  and[
    'nonempty?[x]
    equals?[
      [[x] subs[.] at[.].[0] prefix[.]]
      ['+']
    ]
  ]
]
```

`as jevko[subjevko]` wraps the `subjevko` in a jevko.

```
define[ addend['[s]] 
  [s]
  subs[.]
  at[.].[0]
  jevko[.]
  subs[.]
  at[.].[0]
  as jevko[.] 
]

define[ augend['[s]] 
  [s]
  subs[.]
  at[.].[0]
  jevko[.]
  subs[.]
  at[.].[1]
  as jevko[.] 
]
```

## 149

```
define[  multiplicand[p]  caddr[p]  ]
```

Note: we shall translate `'(+ x 3)` into `list[ '[x] [3] ]`, etc.

```
deriv[  list[ '[+] '[x] [3] ]  '[x]  ]

deriv[  list[ '[*] '[x] [y] ]  '[x]  ]

deriv[  list[ '[*] list['[*]'[x]'[y]] list['[+]'[x][3]] ]  '[x]  ]

define[  make sum[ [a1] [a2] ]
  ?[
    =number?[ [a1] [0] ]  [a2]
    =number?[ [a2] [0] ]  [a1]
    and[
      number?[a1]
      number?[a2]
    ]  +[ [a1] [a2] ]
    list[ '[+] [a1] [a2] ]
  ]
]
```

## 150

```
define[  =number?[ [exp] [num] ]
  and[
    number?[exp]
    =[ [exp] [num] ]
  ]
]

define[  make product[ [m1] [m2] ]
  ?[
    or[
      =number?[ [m1] [0] ]
      =number?[ [m2] [0] ]
    ]  [0]
    =number?[ [m1] [1] ]  [m2]
    =number?[ [m2] [1] ]  [m1]
    and[
      number?[m1]
      number?[m2]
    ]  *[ [m1] [m2] ]
    list[ '[*] [m1] [m2] ]
  ]
]

deriv[  list[ '[+] '[x] [3] ]  '[x]  ]

deriv[  list[ '[*] '[x] '[y] ]  '[x]  ]

deriv[  list[ '[*] list['[*]'[x]'[y]] list['[+]'[x][3]] ]  '[x]  ]
```

## 151

```
deriv[
  list[ '[*] '[x] '[y] list['[+]'[x][3]] ]
  '[x]
]
```

## 152

```
define[
  element of set?[ [x] [set] ]
  ?[
    null?[set]  [false]
    equal?[ [x] car[set] ]  [true]
    element of set?[ [x] cdr[set] ]
  ]
]

define[
  adjoin set[ [x] [set] ]
  ?[
    element of set?[ [x] [set] ]  [set]
    cons[ [x] [set] ]
  ]
]
```

## 153

```
define[
  intersection set[ [set1] [set2] ]
  ?[
    or[ null?[set1] null?[set2] ]  [nil]
    element of set?[ car[set1] [set2] ]  cons[
      car[set1]
      intersection set[ cdr[set1] [set2] ]
    ]
    intersection set[ cdr[set1] [set2] ]
  ]
]
```

Or using `head`, `tail`, and `pair` instead of `car`, `cdr`, and `cons`.

```
define[
  intersection set[ [set1] [set2] ]
  ?[
    or[ null?[set1] null?[set2] ]  [nil]
    element of set?[ head[set1] [set2] ]  pair[
      head[set1]
      intersection set[ tail[set1] [set2] ]
    ]
    intersection set[ tail[set1] [set2] ]
  ]
]
```

## 154

```
define[
  element of set?[ [x] [set] ]
  ?[
    null?[set]  [false]
    =[ [x] car[set] ]  [true]
    <[ [x] car[set] ]  [false]
    element of set?[ [x] cdr[set] ]
  ]
]
```

## 155

```
define[
  intersection set[ [set1] [set2] ]
  ?[
    or[ null?[set1] null?[set2] ]  [nil]
    let[
      [x1]  car[set1]
      [x2]  car[set2]
      ?[
        =[ [x1] [x2] ]  cons[
          [x1]
          intersection set[
            cdr[set1]
            cdr[set2]
          ]
        ]
        <[ [x1] [x2] ]  intersection set[
          cdr[set1]
          [set2]
        ]
        <[ [x2] [x1] ]  intersection set[
          [set1]
          cdr[set2]
        ]
      ]
    ]
  ]
]
```

## 156

```
define[  entry[tree]  car[tree]  ]

define[  left branch[tree]  cadr[tree]  ]
```

## 157

```
define[  right branch[tree]  caddr[tree]  ]

define[  make tree[ [entry] [left] [right] ]
  list[ [entry] [left] [right] ]
]

define[  element of set?[ [x] [set] ]
  ?[
    null?[set]  [false]
    =[ [x] entry[set] ]  [true]
    <[ [x] entry[set] ]  element of set?[
      [x]
      left branch[set]
    ]
    >[ [x] entry[set] ]  element of set?[
      [x]
      right branch[set]
    ]
  ]
]

define[  adjoin set[ [x] [set] ]
  ?[
    null?[set]  make tree[ [x] [nil] [nil] ]
    =[ [x] entry[set] ]  [set]
    <[ [x] entry[set] ]  make tree[
      entry[set]
      adjoin set[ [x] left branch[set] ]
      right branch[set]
    ]
    >[ [x] entry[set] ]  make tree[
      entry[set]
      left branch[set]
      adjoin set[ [x] right branch[set] ]
    ]
  ]
]
```

## 158

```
define[
  tree->list 1[tree]
  ?[
    null?[tree]  [nil]
    append[
      tree->list 1[ left branch[tree] ]
      cons[
        entry[tree]
        tree->list 1[ right branch[tree] ]
      ]
    ]
  ]
]
```

## 159

```
define[  tree->list 2[tree]
  define[  copy to list[ [tree] [result list] ]
    ?[
      null?[tree]  [result list]
      copy to list[
        left branch[tree]
        cons[
          entry[tree]
          copy to list[
            right branch[tree]
            [result list]
          ]
        ]
      ]
    ]
  ]
  copy to list[ [tree] [nil] ]
]

define[  list->tree[elements]
  car[
    partial tree[ [elements] length[elements] ]
  ]
]

define[  partial tree[ [elts] [n] ]
  ?[
    =[ [n] [0] ]  cons[ [nil] [elts] ]
    let[
      [left size]  quotient[ -[[n][1]] [2] ]
      let[
        [left result]  partial tree[ [elts] [left size] ]
        let[
          [left tree]  car[left result]
          [non left elts]  cdr[left result]
          [right size]  -[ [n] +[[left size][1]] ]
          let[
            [this entry]  car[non left elts]
            [right result]  partial tree[
              cdr[non left elts]
              [right size]
            ]
            let[
              [right tree]  car[right result]
              [remaining elts]  cdr[right result]
              cons[
                make tree[ [this entry] [left tree] [right tree] ]
                [remaining elts]
              ]
            ]
          ]
        ]
      ]
    ]
  ]
]
```

## 160

```
define[
  lookup[ [given key] [set of records] ]
  ?[
    null?[set of records]  [false]
    equal?[ [given key] key[car[set of records]] ]  car[set of records]
    lookup[ [given key] cdr[set of records] ]
  ]
]
```

## 165

```
define[  make leaf[ [symbol] [weight] ]
  list[ '[leaf] [symbol] [weight] ]
]

define[  leaf?[object]
  eq?[ car[object] '[leaf] ]
]

define[  symbol leaf[x]  cadr[x]  ]
define[  weight leaf[x]  caddr[x]  ]

define[  make code tree[ [left] [right] ]
  list[
    [left]
    [right]
    append[ symbols[left] symbols[right] ]
    +[ weight[left] weight[right] ]
  ]
]

define[  left branch[tree]  car[tree]  ]

define[  right branch[tree]  cadr[tree]  ]

define[  symbols[tree]
  ?[
    leaf?[tree]  list[symbol leaf[tree]]
    caddr[tree]
  ]
]

define[  weight[tree]
  ?[
    leaf?[tree]  weight leaf[tree]
    cadddr[tree]
  ]
]
```

## 166

```
define[  decode[ [bits] [tree] ]
  define[  decode 1[ [bits] [current branch] ]
    ?[
      null?[bits]  [nil]
      let[
        [next branch]  choose branch[
          car[bits]
          [current branch]
        ]
        ?[
          leaf?[next branch]  cons[
            symbol leaf[next branch]
            decode 1[ cdr[bits] [tree] ]
          ]
          decode 1[ cdr[bits] [next branch] ]
        ]
      ]
    ]
  ]
  decode 1[ [bits] [tree] ]
]

define[  choose branch[ [bit] [branch] ]
  ?[
    =[ [bit] [0] ]  left branch[branch]
    =[ [bit] [1] ]  right branch[branch]
    error[ ['bad bit -- CHOOSE-BRANCH'] [bit] ]
  ]
]
```

## 167

```
define[  adjoin set[ [x] [set] ]
  ?[
    null?[set]  list[x]
    <[ weight[x] weight[car[set]] ]  cons[ [x] [set] ]
    cons[
      car[set]
      adjoin set[ [x] cdr[set] ]
    ]
  ]
]

define[  make leaf set[pairs]
  ?[
    null?[pairs]  [nil]
    let[
      [pair]  car[pair]
      adjoin set[
        make leaf[ car[pair] cadr[pair] ]
        make leaf set[ cdr[pairs] ]
      ]
    ]
  ]
]

define[  [sample tree]
  make code tree[
    make leaf[ '[A] [4] ]
    make code tree[
      make leaf[ '[B] [2] ]
      make code tree[
        make leaf[ '[D] [1] ]
        make leaf[ '[C] [1] ]
      ]
    ]
  ]
]

define[  [sample message]  '[[0][1][1][0][0][1][0][1][0][1][1][1][0]]  ]

define[  encode[ [message] [tree] ]
  ?[  null?[message] [nil]
    append[
      encode symbol[ car[message] [tree] ]
      encode[ cdr[message] [tree] ]
    ]
  ]
]
```

## 168

```
define[  generate huffman tree[pairs]
  successive merge[ make leaf set[pairs] ]
]
```

## 173

```
make from real imag[ real part[z] imag part[z] ]

make from mag ang[ magnitude[z] angle[z] ]

define[  add complex[ [z1] [z2] ]
  make from real imag[
    +[ real part[z1] real part[z2] ]
    +[ imag part[z1] imag part[z2] ]
  ]
]

define[  sub complex[ [z1] [z2] ]
  make from real imag[
    -[ real part[z1] real part[z2] ]
    -[ imag part[z1] imag part[z2] ]
  ]
]

define[  mul complex[ [z1] [z2] ]
  make from mag ang[
    *[ magnitude[z1] magnitude[z2] ]
    +[ angle[z1] angle[z2] ]
  ]
]

define[  div complex[ [z1] [z2] ]
  make from mag ang[
    /[ magnitude[z1] magnitude[z2] ]
    -[ angle[z1] angle[z2] ]
  ]
]
```

## 174

```
define[  real part[z]  car[z]  ]

define[  imag part[z]  cdr[z]  ]

define[  magnitude[z]
  sqrt[+[ square[real part[z]] square[imag part[z]] ]]
]

define[  angle[z]
  atan[ imag part[z] real part[z] ]
]

define[  make from real imag[ [x] [y] ]  cons[ [x] [y] ]  ]

define[  make from mag ang[ [r] [a] ]
  cons[  *[ [r] cos[a] ]  *[ [r] sin[a] ]  ]
]

define[  real part[z]
  *[ magnitude[z] cos[angle[z]] ]
]
```

## 175

```
define[  imag part[z]
  *[ magnitude[z] sin[angle[z]] ]
]

define[  magnitude[z]  car[z]  ]

define[  angle[z]  cdr[z]  ]

define[  make from real imag[ [x] [y] ]
  cons[
    sqrt[+[ square[x] square[y] ]]
    atan[ [y] [x] ]
  ]
]

define[  make from mag ang[ [r] [a] ]  cons[ [r] [a] ]  ]
```

## 176

```
define[  attach tag[ [type tag] [contents] ]
  cons[ [type tag] [contents] ]
]

define[  type tag[datum]
  ?[
    pair?[datum]  car[datum]
    error[ ['Bad tagged datum -- TYPE-TAG'] [datum] ]
  ]
]

define[  contents[datum]
  ?[
    pair?[datum]  cdr[datum]
    error[ ['Bad tagged datum -- CONTENTS'] [datum] ]
  ]
]

define[  rectangular?[z]
  eq?[ type tag[z] '[rectangular] ]
]

define[  polar?[z]
  eq?[ type tag[z] '[polar] ]
]

define[  real part rectangular[z]  car[z]  ]

define[  imag part rectangular[z]  cdr[z]  ]

define[  magnitude rectangular[z]
  sqrt[+[
    square[real part rectangular[z]]
    square[imag part rectangular[z]]
  ]]
]

define[  angle rectangular[z]
  atan[
    imag part rectangular[z]
    real part rectangular[z]
  ]
]
```

## 177

```
define[  make from real imag rectangular[ [x] [y] ]
  attach tag[  '[rectangular]  cons[ [x] [y] ]  ]
]

define[  make from mag ang rectangular[ [r] [a] ]
  attach tag[
    '[rectangular]
    cons[
      *[ [r] cos[a] ]
      *[ [r] sin[a] ]
    ]
  ]
]

define[  real part polar[z]
  *[  magnitude polar[z]  cos[angle polar[z]]  ]
]

define[  imag part polar[z]
  *[  magnitude polar[z] sin[angle polar[z]] ]
]

define[  magnitude polar[z]  car[z]  ]

define[  angle polar[z]  cdr[z]  ]

define[  make from real imag polar[ [x] [y] ]
  attach tag[
    '[polar]
    cons[
      sqrt[+[ square[x] square[y] ]]
      atan[ [y] [x] ]
    ]
  ]
]

define[  make from mag ang polar[ [r] [a] ]
  attach tag[  '[polar]  cons[ [r] [a] ]  ]
]

define[  real part[z]
  ?[
    rectangular?[z]  real part rectangular[contents[z]]
    polar?[z]  real part polar[contents[z]]
    error[ ['Unknown type -- REAL-PART'] [z] ]
  ]
]

define[  imag part[z]
  ?[
    rectangular?[z]  imag part rectangular[contents[z]]
    polar?[z]  imag part polar[contents[z]]
    error[ ['Unknown type -- IMAG-PART'] [z] ]
  ]
]
```

## 178

```
define[  magnitude[z]
  ?[
    rectangular?[z]  magnitude rectangular[contents[z]]
    polar?[z]  magnitude polar[contents[z]]
    error[ ['Unknown type -- MAGNITUDE'] [z] ]
  ]
]

define[  angle[z]
  ?[
    rectangular?[z]  angle rectangular[contents[z]]
    polar?[z]  angle polar[contents[z]]
    error[ ['Unknown type -- ANGLE'] [z] ]
  ]
]

define[  add complex[ [z1] [z2] ]
  make from real imag[
    +[ real part[z1] real part[z2] ]
    +[ imag part[z1] imag part[z2] ]
  ]
]

define[  make from real imag[ [x] [y] ]
  make from real imag rectangular[ [x] [y] ]
]

define[  make from mag ang[ [r] [a] ]
  make from mag ang polar[ [r] [a] ]
]
```

## 181

```
put[ [op] [type] [item] ]

get[ [op] [type] ]
```

## 182

```
define[  install rectangular package[]
  internal procedures:
  define[  real part[z]  car[z]  ]
  define[  imag part[z]  cdr[z]  ]
  define[  magnitude[z]
    sqrt[+[ square[real part[z]] square[imag part[z]] ]]
  ]
  define[  angle[z]
    atan[ imag part[z] real part[z] ]
  ]
  define[  make from real imag[ [x] [y] ]  cons[ [x] [y] ]  ]
  define[  make from mag ang[ [r] [a] ]
    cons[  *[ [r] cos[a] ]  *[ [r] sin[a] ]  ]
  ]

  interface to the rest of the system:
  define[  tag[x]  attach tag[ '[rectangular] [x] ]  ]
  put[ '[real part] '[[rectangular]] [real part]]
  put[ '[imag part] '[[rectangular]] [imag part]]
  put[ '[magnitude] '[[rectangular]] [magnitude]]
  put[ '[angle] '[[rectangular]] [angle]]

  put[ '[make from real imag] '[rectangular] fun[
    [ [x] [y] ]
    tag[ make from real imag[ [x] [y] ]]
  ]]
  put[ '[make from mag ang] '[rectangular] fun[
    [ [r] [a] ]
    tag[ make from mag ang[ [r] [a] ]]
  ]]

  '[done]
]
```

## 183

```
define[  install polar package[]
  internal procedures:
  define[  magnitude[z]  car[z]  ]
  define[  angle[z]  cdr[z]  ]
  define[  make from mag ang[ [r] [a] ]
    cons[ [r] [a] ]
  ]
  define[  real part[z]
    *[ magnitude[z] cos[angle[z]] ]
  ]
  define[  imag part[z]
    *[ magnitude[z] sin[angle[z]] ]
  ]
  define[  make from real imag[ [x] [y] ]
    cons[
      sqrt[+[ square[x] square[y] ]]
      atan[ [y] [x] ]
    ]
  ]

  interface to the rest of the system:
  define[  tag[x]  attach tag[ '[polar] [x] ]  ]
  put[ '[real part] '[[polar]] [real part]]
  put[ '[imag part] '[[polar]] [imag part]]
  put[ '[magnitude] '[[polar]] [magnitude]]
  put[ '[angle] '[[polar]] [angle]]

  put[ '[make from real imag] '[polar] fun[
    [ [x] [y] ]
    tag[ make from real imag[ [x] [y] ]]
  ]]
  put[ '[make from mag ang] '[polar] fun[
    [ [r] [a] ]
    tag[ make from mag ang[ [r] [a] ]]
  ]]

  '[done]
]

apply[ [+] list[[1][2][3][4]] ]
```

## 184

```
define[  apply generic[ [op] ...[args] ]
  let[
    [type tags] map[ [type tag] [args] ]
    let[
      [proc] get[ [op] [type tags] ]
      ?[
        [proc]  apply[  [proc]  map[ [contents] [args] ]  ]
        error[
          ['No method for these types -- APPLY-GENERIC']
          list[ [op] [type tags] ]
        ]
      ]
    ]
  ]
]

define[  real part[z]  apply generic[ '[real part] [z] ]  ]

define[  imag part[z]  apply generic[ '[imag part] [z] ]  ]

define[  magnitude[z]  apply generic[ '[magnitude] [z] ]  ]

define[  angle[z]  apply generic[ '[angle] [z] ]  ]

define[  make from real imag[ [x] [y] ]
  [  get[ '[make from real imag] '[rectangular] ] .[ [x] [y] ] ]
]

define[  make from mag ang[ [r] [a] ]
  [  get[ '[make from mag ang] '[polar] ] .[ [r] [a] ] ]
]

define[  deriv[ [exp] [var] ]
  ?[
    number?[exp]  [0]
    variable?[exp]  ?[ same variable?[[exp][var]] [1] [0] ]
    sum?[exp] make sum[
      deriv[ addend[exp] [var] ]
      deriv[ augend[exp] [var] ]
    ]
    product?[exp]  make sum[
      make product[
        multiplier[exp]
        deriv[ multiplicand[exp] [var] ]
      ]
      make product[
        deriv[ multiplier[exp] [var] ]
        multiplicand[exp]
      ]
    ]
  ]
  <more rules can be added here>
  error[ ['unknown expression type -- DERIV'] [exp] ]
]
```

## 185

```
define[  deriv[ [exp] [var] ]
  ?[
    number?[exp]  [0]
    variable?[exp]  ?[ same variable?[[exp][var]] [1] [0] ]
    [
      get[ '[deriv] operator[exp] ]
      .[ operands[exp] [var] ]
    ]
  ]
]

define[  operator[exp]  car[exp]  ]

define[  operands[exp]  cdr[exp]  ]

[  get[ operator[exp] '[deriv] ]  .[ operands[exp] [var] ]  ]
```

## 186

```
define[  make from real imag[ [x] [y] ]
  define[  dispatch[op]
    ?[
      eq?[ [op] '[real part] ]  [x]
      eq?[ [op] '[imag part] ]  [y]
      eq?[ [op] '[magnitude] ]  sqrt[+[ square[x] square[y] ]]
      eq?[ [op] '[angle] ]  atan[ [y] [x] ]
      error[ ['Unknown op -- MAKE-FROM-REAL-IMAG'] [op] ]
    ]
  ]
  [dispatch]
]
```

## 187

```
define[  apply generic[ [op] [arg] ]  arg[op]  ]
```

## 189

```
define[  add[ [x] [y] ]  apply generic[ '[add] [x] [y] ]  ]

define[  sub[ [x] [y] ]  apply generic[ '[sub] [x] [y] ]  ]

define[  mul[ [x] [y] ]  apply generic[ '[mul] [x] [y] ]  ]

define[  div[ [x] [y] ]  apply generic[ '[div] [x] [y] ]  ]

define[  install scheme number package[]
  define[  tag[x]
    attach tag[ '[scheme number] [x] ]
  ]
  put[  '[add]  '[ [scheme number] [scheme number] ]
    fun[  [ [x] [y] ]  tag[ +[[x][y]] ]  ]
  ]
  put[  '[sub]  '[ [scheme number] [scheme number] ]
    fun[  [ [x] [y] ]  tag[ -[[x][y]] ]  ]
  ]
  put[  '[mul]  '[ [scheme number] [scheme number] ]
    fun[  [ [x] [y] ]  tag[ *[[x][y]] ]  ]
  ]
  put[  '[div]  '[ [scheme number] [scheme number] ]
    fun[  [ [x] [y] ]  tag[ /[[x][y]] ]  ]
  ]
  put[  '[make]  '[scheme number]
    fun[  [x]  tag[x]  ]
  ]
  '[done]
]

define[  make scheme number[n]
  get[ '[make] '[scheme number] ].[n]
]
```

## 190

```
define[  install rational package[]
  internal procedures:
  define[  numer[x]  car[x]  ]
  define[  denom[x]  cdr[x]  ]
  define[  make rat[ [n] [d] ]
    let[
      [g]  gcd[ [n] [d] ]
      cons[  /[ [n] [g] ]  /[ [d] [g] ]  ]
    ]
  ]
  define[  add rat[ [x] [y] ]
    make rat[
      +[
        *[ numer[x] denom[y] ]
        *[ numer[y] denom[x] ]
      ]
      *[ denom[x] denom[y] ]
    ]
  ]
  define[  sub rat[ [x] [y] ]
    make rat[
      -[
        *[ numer[x] denom[y] ]
        *[ numer[y] denom[x] ]
      ]
      *[ denom[x] denom[y] ]
    ]
  ]
  define[  mul rat[ [x] [y] ]
    make rat[
      *[ numer[x] numer[y] ]
      *[ denom[x] denom[y] ]
    ]
  ]
  define[  div rat[ [x] [y] ]
    make rat[
      *[ numer[x] denom[y] ]
      *[ denom[x] numer[y] ]
    ]
  ]

  interface to the rest of the system:
  define[  tag[x]  attach tag[ '[rational] [x] ]  ]
  put[  '[add]  '[ [rational] [rational] ]
    fun[  [ [x] [y] ]  tag[ add rat[[x][y]] ]  ]
  ]
  put[  '[sub]  '[ [rational] [rational] ]
    fun[  [ [x] [y] ]  tag[ sub rat[[x][y]] ]  ]
  ]
  put[  '[mul]  '[ [rational] [rational] ]
    fun[  [ [x] [y] ]  tag[ mul rat[[x][y]] ]  ]
  ]
  put[  '[div]  '[ [rational] [rational] ]
    fun[  [ [x] [y] ]  tag[ div rat[[x][y]] ]  ]
  ]

  put[  '[make]  '[rational]
    fun[  [ [n] [d] ]  tag[ make rat[[n][d]] ]  ]
  ]
  '[done]
]

define[  make rational[ [n] [d] ]
  get[ '[make] '[rational] ].[ [n] [d] ]
]
```

## 191

```
define[  install complex package[]
  imported procedures from rectangular and polar packages:
  define[  make from real imag[ [x] [y] ]
    get[ '[make from real imag] '[rectangular] ].[ [x] [y] ]
  ]
  define[  make from mag ang[ [r] [a] ]
    get[ '[make from mag ang] '[polar] ].[ [r] [a] ]
  ]

  internal procedures:
  define[  add complex[ [z1] [z2] ]
    make from real imag[
      +[ real part[z1] real part[z2] ]
      +[ imag part[z1] imag part[z2] ]
    ]
  ]
  define[  sub complex[ [z1] [z2] ]
    make from real imag[
      -[ real part[z1] real part[z2] ]
      -[ imag part[z1] imag part[z2] ]
    ]
  ]
  define[  mul complex[ [z1] [z2] ]
    make from mag ang[
      *[ magnitude[z1] magnitude[z2] ]
      +[ angle[z1] angle[z2] ]
    ]
  ]
  define[  div complex[ [z1] [z2] ]
    make from mag ang[
      /[ magnitude[z1] magnitude[z2] ]
      -[ angle[z1] angle[z2] ]
    ]
  ]

  interface to the rest of the system:
  define[  tag[z]  attach tag[ '[complex] [z] ]  ]
  put[  '[add]  '[ [complex] [complex] ]
    fun[  [ [z1] [z2] ]  tag[ add complex[[z1][z2]] ]  ]
  ]
  put[  '[sub]  '[ [complex] [complex] ]
    fun[  [ [z1] [z2] ]  tag[ sub complex[[z1][z2]] ]  ]
  ]
  put[  '[mul]  '[ [complex] [complex] ]
    fun[  [ [z1] [z2] ]  tag[ mul complex[[z1][z2]] ]  ]
  ]
  put[  '[div]  '[ [complex] [complex] ]
    fun[  [ [z1] [z2] ]  tag[ div complex[[z1][z2]] ]  ]
  ]

  put[  '[make from real imag]  '[complex]
    fun[  [ [x] [y] ]  tag[ make from real imag[[x][y]] ]  ]
  ]
  put[  '[make from mag ang]  '[complex]
    fun[  [ [r] [a] ]  tag[ make from mag ang[[r][a]] ]  ]
  ]
  '[done]
]
```

## 192

```
define[  make complex from real imag[ [x] [y] ]
  get[ '[make from real imag] '[complex] ].[ [x] [y] ]
]
define[  make complex from mag ang[ [r] [a] ]
  get[ '[make from mag ang] '[complex] ].[ [r] [a] ]
]
```

## 193

```
put[  '[real part]  '[[complex]]  [real part]  ]
put[  '[real part]  '[[complex]]  [real part]  ]
put[  '[magnitude]  '[[complex]]  [magnitude]  ]
put[  '[angle]  '[[complex]]  [angle]  ]
```

## 194

```
to be included in the complex package:
define[  add complex to schemenum[ [z] [x] ]
  make from real imag[
    +[ real part[z] [x] ]
    imag part[z]
  ]
]

put[  '[add]  '[ [complex] [scheme number] ]
  fun[  [ [z] [x] ]  tag[add complex to schemenum[ [z] [x] ]]  ]
]
```

## 195

```
define[  scheme number->complex[n]
  make complex from real imag[ contents[n] [0] ]
]

put coerction[  '[scheme number]  '[complex]  scheme number->complex  ]
```

## 196

```
define[  apply generic[ [op] ...[args] ]
  let[
    [type tags]  map[ [type tag] [args] ]
    let[
      [proc]  get[ [op] [type tags] ]
      ?[
        [proc]  apply[ [proc] map[[contents][args]] ]
        ?[
          =[ length[args] [2] ]  let[
            [type1]  car[type tags]
            [type2]  cadr[type tags]
            [a1]  car[args]
            [a2]  cadr[args]
            let[
              [t1->t2]  get coercion[ [type1] [type2] ]
              [t2->t1]  get coercion[ [type2] [type1] ]
              ?[
                [t1->t2]  apply generic[ [op] t1->t2[a1] [a2] ]
                [t2->t1]  apply generic[ [op] [a1] t2->t1[a2] ]
                error[
                  ['No method for these types']
                  list[ [op] [type tags] ]
                ]
              ]
            ]
          ]
          error[
            ['No method for these types']
            list[ [op] [type tags] ]
          ]
        ]
      ]
    ]
  ]
]
```

Note: for `apply generic` to work properly, `get` needs to accept the following forms as interchangeable:

```
list[ '[a] '[b] '[c] ]
'[ [a] [b] [c] ]
```

`get` is thus far not defined in the book, but we should take that into account later.

Anyway, to accept these forms as interchangeable, we shall define conversion functions:

```
define[  list of jevkos->jevko[l]
  jevko[
    map[ 
      fun[  [j]  subjevko[ [''] [j] ]  ]
      [l]
    ]
    ['']
  ]
]

define[  jevko->list of jevkos[j]
  map[
    fun[  [s]  get jevko[s]  ]
    subs[j]
  ]
]
```

where `get jevko[subjevko]` extracts the `subjevko's` `jevko`.

The same functions with added type checking:

```
define[  list of jevkos->jevko[l]
  ?[
    list?[l]  jevko[
      map[ 
        fun[  [j]
          ?[
            jevko?[j]  subjevko[ [''] [j] ]
            error[ ['Expected jevko, got '] [j] ]
          ]
        ]
        [l]
      ]
      ['']
    ]
    error[ ['Expected list, got '] [l] ]
  ]
]

define[  jevko->list of jevkos[j]
  ?[
    jevko?[j]  map[
      fun[  [s]  get jevko[s]  ]
      subs[j]
    ]
    error[ ['Expected jevko, got '] [j] ]
  ]
]
```

Where `jevko?[value]` checks whether a value is a `jevko`.

Perhaps it would be sensible to specify a more organized naming convention(s) for selector and constructor functions, e.g.:

```
selectors start with 'get'
get subs[jevko]
get jevko[subjevko]

constructors start with 'make'
make jevko[ [subs] [suffix] ]
make sub[ [prefix] [jevko] ]
```

[certain?] selectors could also be invokable something like:

```
at[jevko].['subs']
at[subjevko].['jevko']
```

i.e. as "fields". The generalized `at` would check the type of its argument and return a function which accepts the name of a selector. An editor could autocomplete the names.

## 200

```
define[  scheme number->scheme number[n]  [n]  ]

define[  complex->complex[z]  [z]  ]

put coercion[  '[scheme number] '[scheme number]  scheme number->scheme number  ]

put coercion[  '[complex] '[complex]  complex->complex  ]

define[  exp[ [x] [y] ]  apply generic[ '[exp] [x] [y] ]  ]

put[  '[exp]  '[ [scheme number] [scheme number] ]
  fun[  [ [x] [y] ]  tag[expt[ [x] [y] ]]  using primitive expt  ]
]
```

## 204

```
define[  add poly[ [p1] [p2] ]
  ?[
    same variable?[ variable[p1] variable[p2] ]  make poly[
      variable[p1]
      add terms[
        term list[p1]
        term list[p2]
      ]
    ]
    error[
      [`Polys not in same var -- ADD-POLY`]
      list[ [p1] [p2] ]
    ]
  ]
]

define[  mul poly[ [p1] [p2] ]
  ?[
    same variable?[ variable[p1] variable[p2] ]  make poly[
      variable[p1]
      mul terms[
        term list[p1]
        term list[p2]
      ]
    ]
    error[
      [`Polys not in same var -- MUL-POLY`]
      list[ [p1] [p2] ]
    ]
  ]
]

define[  install polynomial package[]
  internal procedures
  representation of poly
  define[  make poly[ [variable] [term list] ]
    cons[ [variable] [term list] ]
  ]
  define[  variable[p]  car[p]  ]
  define[  term list[p]  cdr[p]  ]
  <procedures 'same variable?' and 'variable?' from section 2.3.2>

  representation of terms and term lists
  <procedures 'adjoin term' ... 'coeff' from text below>

  continued on next page
```

## 205

```
  define[  add poly[ [p1] [p2] ]  ...  ]
  <procedures used by 'add poly'>
  define[  mul poly[ [p1] [p2] ]  ...  ]
  <procedures used by 'mul poly'>

  interface to the rest of the system
  define[  tag[p]  attach tag[ '[polynomial] [p] ]  ]
  put[  '[add]  '[ [polynomial] [polynomial] ]
    fun[  [ [p1] [p2] ]  tag[add poly[ [p1] [p2] ]]  ]
  ]
  put[  '[mul]  '[ [polynomial] [polynomial] ]
    fun[  [ [p1] [p2] ]  tag[mul poly[ [p1] [p2] ]]  ]
  ]
  put[  '[make]  '[polynomial]
    fun[  [ [var] [terms] ]  tag[make poly[ [var] [terms] ]]  ]
  ]
  '[done]
]
```

An idea for a leaner lambda variant:

```
fun1[  [p1] [p2]  tag[mul poly[ [p1] [p2] ]]  ]
```

The syntax here is:

```
fun1[ [arg1] ... [argN] [body] ]
```

The brackets around the args are discarded in exchange for single-expression body. The body could always be made into a block however.

## 206

```
define[  add terms[ [L1] [L2] ]
  ?[
    empty termlist?[L1]  [L2]
    empty termlist?[L2]  [L1]
    let[
      [t1]  first term[L1]
      [t2]  first term[L2]
      ?[
        >[ order[t1] order[t2] ]  adjoin term[
          [t1]
          add terms[ rest terms[L1] [L2] ]
        ]
        <[ order[t1] order[t2] ]  adjoin term[
          [t2]
          add terms[ [L1] rest terms[L2] ]
        ]
        adjoin term[
          make term[
            order[t1]
            add[ coeff[t1] coeff[t2] ]
          ]
          add terms[
            rest terms[L1]
            rest terms[L2]
          ]
        ]
      ]
    ]
  ]
]

define[  mul terms[ [L1] [L2] ]
  ?[
    empty termlist?[L1]  the empty termlist[]
    add terms[
      mul term by all terms[ first term[L1] [L2] ]
      mul terms[ rest terms[L1] [L2] ]
    ]
  ]
]

define[  mul term by all terms[ [t1] [L] ]
  ?[
    empty termlist?[L]  the empty termlist[]
    let[
      [t2]  first term[L]
      adjoin term[
        make term[
          +[ order[t1] order[t2] ]
          mul[ coeff[t1] coeff[t2] ]
        ]
        mul term by all terms[ [t1] rest terms[L] ]
      ]
    ]
  ]
]
```

## 209

```
define[  adjoin term[ [term] [term list] ]
  ?[
    =zero?[coeff[term]]  [term list]
    cons[ [term] [term list] ]
  ]
]

define[  the empty termlist[]  [nil]  ]

define[  first term[term list]  car[term list]  ]

define[  rest terms[term list]  cdr[term list]  ]

define[  empty termlist?[term list]  null?[term list]  ]

define[  make term[ [order] [coeff] ]  list[ [order] [coeff] ]  ]

define[  order[term]  car[term]  ]

define[  coeff[term]  cadr[term]  ]

define[  make polynomial[ [var] [terms] ]
  get[ '[make] '[polynomial] ].[ [var] [terms] ]
]
```

An idea: a `list'` function that works much like Scheme's quote applied to a list: it returns a list of unevaluated jevkos. That's in contrast to `'` which returns a jevko.

```
list'[ [a] [b] ]

would be equivalent to

list[ '[a] '[b] ]
```

## 210

```
define[  div terms[ [L1] [L2] ]
  ?[
    empty termlist?[L1]  list[ the empty termlist[] the empty termlist[] ]
    let[
      [t1]  first term[L1]
      [t2]  first term[L2]
      ?[
        >[ order[t2] order[t1] ]  list[ the empty termlist[] [L1] ]
        let[
          [new c]  div[ coeff[t1] coeff[t2] ]
          [new o]  -[ order[t1] order[t2] ]
          let[
            [rest of result]  <compute rest of result recursively>
            <form complete result>
          ]
        ]
      ]
    ]
  ]
]
```

## 212

```
define[  [p1]  
  make polynomial[ 
    '[x] 
    list'[ [[2][1]] [[0][1]] ] 
  ]
]

define[  [p2]  
  make polynomial[ 
    '[x] 
    list'[ [[3][1]] [[0][1]] ] 
  ]
]

define[  [rf]
  make rational[ [p2] [p1] ]
]

define[  gcd[ [a] [b] ]
  ?[
    =[ [b] [0] ]  [a]
    gcd[ [b] remainder[[a][b]] ]
  ]
]
```

Note: `list'` should then interpret things like:

```
list'[ [[2][1]] [[0][1]] ] 
```

as

```
list[ list['[2]'[1]] list['[0]'[1]] ] 
```

## 213

```
define[  gcd terms[ [a] [b] ]
  ?[
    empty termlist?[b]  [a]
    gcd terms[ [b] remainder terms[[a][b]] ]
  ]
]

define[  [p1]
  make polynomial[
    '[x]
    list'[ [[4][1]] [[3][-1]] [[2][-2]] [[1][2]] ]
  ]
]

define[  [p2]
  make polynomial[
    '[x]
    list'[ [[3][1]] [[1][-1]] ]
  ]
]

greatest common divisor[ [p1] [p2] ]
```

## 215

```
define[  reduce integers[ [n] [d] ]
  let[
    [g]  gcd[[n][d]]
    list[ /[[n][g]] /[[d][g]] ]
  ]
]

define[  [p1]
  make polynomial[
    '[x]
    list'[ [[1][1]] [[0][1]] ]
  ]
]
define[  [p2]
  make polynomial[
    '[x]
    list'[ [[3][1]] [[0][-1]] ]
  ]
]
define[  [p3]
  make polynomial[
    '[x]
    list'[ [[1][1]] ]
  ]
]
define[  [p4]
  make polynomial[
    '[x]
    list'[ [[2][1]] [[0][-1]] ]
  ]
]

define[  [rf1]  make rational[ [p1] [p2] ]  ]
define[  [rf2]  make rational[ [p3] [p4] ]  ]

add[ [rf1] [rf2] ]
```

## Chapter 3

## 219

```
withdraw[25]

withdraw[25]

withdraw[60]

withdraw[15]
```


## 220

```
define[  [balance]  [100]  ]

define[  withdraw[amount]
  ?[
    >=[ [balance] [amount] ]  [
      set![ [balance] -[[balance][amount]] ]
      [balance]
    ]
    [`Insufficient funds`]
  ]
]

set![ [balance] -[[balance][amount]] ]

set![ [name] [new value] ]
```

## 221

The equivalent of `begin` in Jevkalk is simply:

```
[ [exp_1] [exp_2] ... [exp_k] ]
```

```
define[  [new withdraw]
  let[
    [balance]  [100]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      [`Insufficient funds`]
    ]
  ]
]
```

An Unified Call Syntax I've been developing would also allow this:

```
[balance].set![-[[balance][amount]]]
```

or even:

```
[balance].set![[balance].-[amount]]
```

More on that later.


## 222

```
define[  make withdraw[balance]
  fun[ [amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      [`Insufficient funds`]
    ]
  ]
]

define[  [W1]  make withdraw[100]  ]
define[  [W2]  make withdraw[100]  ]

W1[50]

W2[70]
```

## 223

```
W2[40]

W1[40]

define[  make account[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ] [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      [`Insufficient funds`]
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  define[  dispatch[m]
    ?[
      eq?[ [m] '[withdraw] ]  [withdraw]
      eq?[ [m] '[deposit] ]  [deposit]
      error[
        [`Unknown request -- MAKE-ACCOUNT`]
        [m]
      ]
    ]
  ]
  [dispatch]
]

define[  [acc]  make account[100]  ]

acc[ '[withdraw] ].[50]
```

## 224

```
acc[ '[withdraw] ].[60]

acc[ '[deposit] ].[40]

acc[ '[withdraw] ].[60]

define[  [acc2]  make account[100]  ]

define[  [A]  make accumulator[5]  ]

A[10]

A[10]
```

If we redefine `make account`'s `dispatch` as:

```
define[  dispatch[m]
  ?[
    eq?[ [m] [`withdraw`] ]  [withdraw]
    eq?[ [m] [`deposit`] ]  [deposit]
    error[
      [`Unknown request -- MAKE-ACCOUNT`]
      [m]
    ]
  ]
]
```

i.e. we accept strings instead of "symbols", the above code will look nicer:

```
acc[`withdraw`].[60]

acc[`deposit`].[40]

acc[`withdraw`].[60]
```

## 225

```
define[  [s]  make monitored[sqrt]  ]

s[100]

s[ '[how many calls] ]

define[  [acc]  make account[ [100] '[secret password] ]  ]

acc[ '[secret password] '[withdraw] ].[40]

acc[ '[some other password] '[deposit] ].[50]

x_2 = rand update[x_1]
x_3 = rand update[x_2]
```

## 226

```
define[  [rand]
  let[
    [x]  [random init]
    fun[ []
      set![ [x] rand update[x] ]
      [x]
    ]
  ]
]
```

## 227

```
define[  estimate pi[trials]
  sqrt[/[ [6] monte carlo[[trials][cesaro test]] ]]
]

define[  cesaro test[]
  =[ gcd[rand[]rand[]] [1] ]
]

define[  monte carlo[ [trials] [experiment] ]
  define[  iter[ [trials remaining] [trials passed] ]
    ?[
      =[ [trials remaining] [0] ]  /[ [trials passed] [trials] ]
      [experiment]  iter[ -[[trials remaining][1]] +[[trials passed][1]] ]
      iter[ -[[trials remaining][1]] [trials passed] ]
    ]
  ]
  iter[ [trials] [0] ]
]

define[  estimate pi[trials]
  sqrt[/[ [6] random gcd test[[trials][random init]] ]]
]

define[  random gcd test[ [trials] [initial x] ]
  define[  iter[ [trials remaining] [trials passed] [x] ]
    let[
      [x1]  rand update[x]
      let[
        [x2]  rand update[x1]
        ?[
          =[ [trials remaining] [0] ]  /[ [trials passed] [trials] ]
          =[ gcd[[x1][x2]] [1] ]  iter[
            -[ [trials remaining] [1] ]
            +[ [trials passed] [1] ]
            [x2]
          ]
          iter[
            -[ [trials remaining] [1] ]
            [trials passed]
            [x2]
          ]
        ]
      ]
    ]
  ]
  iter[ [trials] [0] [initial x] ]
]
```

## 229

```
define[  random in range[ [low] [high] ]
  let[
    [range]  -[ [high] [low] ]
    +[ [low] random[range] ]
  ]
]
```

## 230

```
define[  make simplified withdraw[balance]
  fun[ [amount]
    set![ [balance] -[[balance][amount]] ]
    [balance]
  ]
]

define[  [W]  make simplified withdraw[25]  ]

W[20]

W[10]

define[  make decrementer[balance]
  fun[ [amount]
    -[ [balance] [amount] ] 
  ]
]

define[  [D]  make decrementer[25]  ]

D[20]

D[10]

make decrementer[25].[20]
```

## 231

```
fun[ [amount] -[[25][amount]] ].[20]

-[ [25] [20] ]

make simplified withdraw[25].[20]

fun[  [amount]  set![ [balance] -[[25][amount]] ]  [25]  ].[20]

set![ [balance] -[[25][20]] ] [25]
```

## 232

```
define[  [D1]  make decrementer[25]  ]

define[  [D2]  make decrementer[25]  ]

define[  [W1]  make simplified withdraw[25]  ]

define[  [W2]  make simplified withdraw[25]  ]

W1[20]

W1[20]

W2[20]
```

## 233

```
define[  [peter acc]  make account[100]  ]

define[  [paul acc]  make account[100]  ]

define[  [peter acc]  make account[100]  ]

define[  [paul acc]  [peter acc]  ]
```

## 234

```
define[  factorial[n]
  define[  iter[ [product] [counter] ]
    ?[
      >[ [counter] [n] ]  [product]
      iter[
        *[ [counter] [product] ]
        +[ [counter] [1] ]
      ]
    ]
  ]
  iter[ [1] [1] ]
]
```

## 235

```
define[  factorial[n]
  let[
    [product]  [1]
    [counter]  [1]
    [
      define[  iter[]
        ?[
          >[ [counter] [n] ]  [product]
          [
            set![ [product] *[[counter][product]] ]
            set![ [counter] +[[counter][1]] ]
            iter[]
          ]
        ]
      ]
      iter[]
    ]
  ]
]

set![ [counter] +[[counter][1]] ]
set![ [product] *[[counter][product]] ]
```

## 236

```
define[  [paul acc]
  make joint[ [peter acc] '[open sesame] '[rosebud] ]
]
```

## 238

```
define[  square[x]
  *[ [x] [x] ]
]
```

## 239

```
define[  [square]
  fun[  [x]  *[ [x] [x] ]  ]
]
```

## 241

```
define[  square[x]
  *[ [x] [x] ]
]

define[  sum of squares[ [x] [y] ]
  +[ square[x] square[y] ]
]

define[  f[a]
  sum of squares[ +[[a][1]] *[[a][2]] ]
]
```

## 242

```
sum of squares[ +[[a][1]] *[[a][2]] ]
```

## 243

```
define[  factorial[n]
  ?[
    =[ [n] [1] ]  [1]
    *[ [n] factorial[-[[n][1]]] ]
  ]
]

define[  factorial[n]
  fact iter[ [1] [1] [n] ]
]
```

## 244

```
define[  fact iter[ [product] [counter] [max count] ]
  ?[
    >[ [counter] [max count] ]  [product]
    fact iter[
      *[ [counter] [product] ]
      +[ [counter] [1] ]
      [max count]
    ]
  ]
]

define[  make withdraw[balance]
  fun[  [amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      [`Insufficient funds`]
    ]
  ]
]

define[  [W1]  make withdraw[100]  ]

W1[50]

define[  [W1]  make withdraw[100]  ]
```

## 245

```
W1[50]

?[
  >=[ [balance] [amount] ] [
    set![ [balance] -[[balance][amount]] ]
    [balance]
  ]
  [`Insufficient funds`]
]
```

## 246

```
define[  [W2]  make withdraw[100]  ]
```

## 248

```
define[  make withdraw[initial amount]
  let[
    [balance]  [initial amount]
    fun[  [amount]
      ?[
        >=[ [balance] [amount] ]  [
          set![ [balance] -[[balance][amount]] ]
          [balance]
        ]
        [`Insufficient funds`]
      ]
    ]
  ]
]

define[  [W1]  make withdraw[100]  ]

W1[50]

define[  [W2]  make withdraw[100]  ]
```

## 249

```
define[  sqrt[x]
  define[  good enough?[guess]
    <[  abs[-[ square[guess] [x] ]]  [0.001]  ]
  ]
  define[  improve[guess]
    average[ [guess] /[[x][guess]] ]
  ]
  define[  sqrt iter[guess]
    ?[
      good enough?[guess]  [guess]
      sqrt iter[ improve[guess] ]
    ]
  ]
  sqrt iter[1.0]
]
```

## 250

```
define[  good enough?[guess]
  <[  abs[-[ square[guess] [x] ]]  [0.001]  ]
]
```

## 251

```
define[  make account[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      ['Insufficient funds']
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  define[  dispatch[m]
    ?[
      eq?[ [m] ['withdraw'] ]  [withdraw]
      eq?[ [m] ['deposit'] ]  [deposit]
      error[
        ['Unknown request -- MAKE-ACCOUNT']
        [m]
      ]
    ]
  ]
  [dispatch]
]

define[  [acc]  make account[50]  ]

acc['deposit'].[40]

acc['withdraw'].[60]

define[  [acc2]  make account[100] ]
```

## 252

```
set balance![ [<account>] [<new value>] ]
```

## 255

```
define[  cons[ [x] [y] ]
  let[
    [new]  get new pair[]
    [
      set car![ [new] [x] ]
      set cdr![ [new] [y] ]
      [new]
    ]
  ]
]

define[  append[ [x] [y] ]
  ?[
    null?[x]  [y]
    cons[  car[x]  append[ cdr[x] [y] ]  ]
  ]
]

define[  append![ [x] [y] ]
  set cdr![ last pair[x] [y] ]
  [x]
]

define[  last pair[x]
  ?[
    null?[cdr[x]]  [x]
    last pair[cdr[x]]
  ]
]

define[  [x]  list[ ['a'] ['b'] ]  ]

define[  [y]  list[ ['c'] ['d'] ]  ]

define[  [z]  append[ [x] [y] ]  ]
```

## 256

```
[z]

cdr[x]

define[  [w]  append![ [x] [y] ]  ]

[w]

cdr[x]

define[  make cycle[x]
  set cdr![ last pair[x] [x] ]
  [x]
]

define[  [z]  make cycle[ list[['a']['b']['c']] ]  ]

define[  mystery[x]
  define[  loop[ [x] [y] ]
    ?[
      null?[x]  [y]
      let[
        [temp]  cdr[x]
        [
          set cdr![ [x] [y] ]
          loop[ [temp] [x] ]
        ]
      ]
    ]
  ]
  loop[ [x] [nil] ]
]
```

## 257

Experimenting here with using strings instead of symbols.

`['a]` is the string `a`. It is equivalent to `['a']` and `` [`a`] ``.

```
define[  [x]  list[ ['a] ['b] ]  ]

define[  [z1]  cons[ [x] [x] ]  ]

define[  [z2]  cons[ list[['a]['b]] list[['a]['b]] ]  ]
```

## 258

```
define[  set to wow![x]
  set car![ car[x] ['wow] ]
  [x]
]

[z1]

set to wow![z1]

[z2]

set to wow![z2]
```

## 259

```
define[  count pairs[x]
  ?[
    not[pair?[x]]  [0]
    +[
      count pairs[car[x]]
      count pairs[cdr[x]]
      [1]
    ]
  ]
]
```

## 260

```
define[  cons[ [x] [y] ]
  define[  dispatch[m]
    ?[
      eq?[ [m] ['car] ]  [x]
      eq?[ [m] ['cdr] ]  [y]
      error[ ['Undefined operation -- CONS] [m] ]
    ]
  ]
  [dispatch]
]

define[  car[z]  z['car]  ]

define[  cdr[z]  z['cdr]  ]

define[  cons[ [x] [y] ]
  define[  set x![v]  set![ [x] [v] ]  ]
  define[  set y![v]  set![ [y] [v] ]  ]
  define[  dispatch[m]
    ?[
      eq?[ [m] ['car] ]  [x]
      eq?[ [m] ['cdr] ]  [y]
      eq?[ [m] ['set car!] ]  [set x!]
      eq?[ [m] ['set cdr!] ]  [set y!]
      error[ ['Undefined operation -- CONS] [m] ]
    ]
  ]
  [dispatch]
]

define[  car[z]  z['car]  ]
define[  cdr[z]  z['cdr]  ]
```

## 261

```
define[  set car![ [z] [new value] ]
  z['set car!].[new value]
  [z]
]

define[  set cdr![ [z] [new value] ]
  z['set cdr!].[new value]
  [z]
]

define[  [z]  cons[ [1] [2] ]  ]

define[  [z]  cons[ [x] [x] ]  ]

set car![ cdr[z] [17] ]

car[x]
```

## 262

```
define[  [q]  make queue[]  ]

insert queue![ [q] ['a] ]    a

insert queue![ [q] ['b] ]    a b

delete queue![q]             b

insert queue![ [q] ['c] ]    b c

insert queue![ [q] ['d] ]    b c d

delete queue![q]             c d

make queue[]

empty queue?[<queue>]

front queue[<queue>]

insert queue![ [<queue>] [<item>] ]

delete queue![<queue>]
```

## 263

```
define[  front ptr[queue]  car[queue]  ]

define[  rear ptr[queue]  cdr[queue]  ]

define[  set front ptr![ [queue] [item] ]  set car![ [queue] [item] ]  ]

define[  set rear ptr![ [queue] [item] ]  set cdr![ [queue] [item] ]  ]
```

## 264

```
define[  make queue[]  cons[ [nil] [nil] ]  ]

define[  front queue[queue]
  ?[
    empty queue?[queue]  error[ [`FRONT called with an empty queue`] [queue] ]
    car[front ptr[queue]]
  ]
]

define[  insert queue![ [queue] [item] ]
  let[
    [new pair]  cons[ [item] [nil] ]
    ?[
      empty queue?[queue]  [
        set front ptr![ [queue] [new pair] ]
        set rear ptr![ [queue] [new pair] ]
        [queue]
      ]
      [
        set cdr![ rear ptr[queue] [new pair] ]
        set rear ptr![ [queue] [new pair] ]
        [queue]
      ]
    ]
  ]
]
```

## 265

```
define[  delete queue![queue]
  ?[
    empty queue?[queue]  error[
      [`DELETE! called with an empty queue`]
      [queue]
    ]
    [
      set front ptr![ [queue] cdr[front ptr[queue]] ]
      [queue]
    ]
  ]
]

define[  [q1]  make queue[]  ]

insert queue![ [q1] ['a] ]

insert queue![ [q1] ['b] ]

delete queue![q1]

delete queue![q1]
```

## 266

```
define[  make queue[]
  let[
    [front ptr]  [...]
    [rear ptr]  [...]
    [
      <definitions of internal procedures>
      define[  dispatch[m]  [...]  ]
      [dispatch]
    ]
  ]
]
```

## 268

```
define[  lookup[ [key] [table] ]
  let[
    [record]  assoc[ [key] cdr[table] ]
    ?[
      [record]  cdr[record]
      [false]
    ]
  ]
]

define[  assoc[ [key] [records] ]
  ?[
    null?[records]  [false]
    equal?[ [key] caar[records] ]  car[records]
    assoc[ [key] cdr[records] ]
  ]
]

define[  insert![ [key] [value] [table] ]
  let[
    [record]  assoc[ [key] cdr[table] ]
    ?[
      [record]  set cdr![ [record] [value] ]
      set cdr![
        [table]
        cons[  cons[ [key] [value] ]  cdr[table]  ]
      ]
    ]
  ]
  ['ok]
]

define[  make table[]
  list[ ['*table*] ]
]
```

## 270

```
define[  lookup[ [key 1] [key 2] [table] ]
  let[
    [subtable]  assoc[ [key 1] cdr[table] ]
    ?[
      [subtable]  let[
        [record]  assoc[ [key 2] cdr[subtable] ]
        ?[
          [record]  cdr[record]
          [false]
        ]
      ]
      [false]
    ]
  ]
]

define[  insert![ [key 1] [key 2] [value] [table] ]
  let[
    [subtable]  assoc[ [key 1] cdr[table] ]
    ?[
      [subtable]  let[
        [record]  assoc[ [key 2] cdr[subtable] ]
        ?[
          [record]  set cdr![ [record] [value] ]
          set cdr![
            [subtable]
            cons[
              cons[ [key 2] [value] ]
              cdr[subtable]
            ]
          ]
        ]
      ]
      set cdr![
        [table]
        cons[
          list[  [key 1]  cons[ [key 2] [value] ]  ]
          cdr[table]
        ]
      ]
    ]
  ]
  ['ok]
]
```

## 271

```
define[  make table[]
  let[
    [local table]  list['*table*]
    [
      define[  lookup[ [key 1] [key 2] ]
        let[
          [subtable]  assoc[ [key 1] cdr[local table] ]
          ?[
            [subtable]  let[
              [record]  assoc[ [key 2] cdr[subtable] ]
              ?[
                [record]  cdr[record]
                [false]
              ]
            ]
            [false]
          ]
        ]
      ]
      define[  insert![ [key 1] [key 2] [value] ]
        let[
          [subtable]  assoc[ [key 1] cdr[local table] ]
          ?[
            [subtable]  let[
              [record]  assoc[ [key 2] cdr[subtable] ]
              ?[
                [record]  set cdr![ [record] [value] ]
                set cdr![
                  [subtable]
                  cons[
                    cons[ [key 2] [value] ]
                    cdr[subtable]
                  ]
                ]
              ]
            ]
            set cdr![
              [local table]
              cons[
                list[  [key 1]  cons[ [key 2] [value] ]  ]
                cdr[local table]
              ]
            ]
          ]
        ]
        ['ok]
      ]
      define[  dispatch[m]
        ?[
          eq?[ [m] ['lookup proc] ]  [lookup]
          eq?[ [m] ['insert proc!] ]  [insert!]
          error[ [`Unknown operation -- TABLE`] [m] ]
        ]
      ]
      [dispatch]
    ]
  ]
]

define[  [operation table]  make table[]  ]
define[  [get]  operation table['lookup proc]  ]
define[  [set]  operation table['insert proc!]  ]
```

Note that the above definition uses strings instead of "symbols", so it's inconsistent with the previous code that assumed the existence of `get` and `put` operations. That would need to be adjusted accordingly. Perhaps at a later time. For now the purpose of this translation is to explore different language features, learn about them, apply the spirit of minimalism, come up with new ideas in the process, filter and solidify these ideas.

As I get to the end of the book or sufficiently far, I may do a round of editing that will make things neat.

BTW I'm thinking that the `let` construct may be entirely done away with in favor of (generalized?) `define`. Also I may want to replace `cons`, `cdr`, `car` with higher-level modern equivalents. In fact I am forming an idea for a language codenamed `JevoScript` which would be compiled to JavaScript and highly-interoperable with it. It would be a thin Jevko-based syntactic layer that generalizes certain language constructs, streamlining and simplifying JavaScript, fixing some design errors, making the language fully expression oriented. It would take the best from Scheme (which after all, is the root of JavaScript) and JavaScript, combining the simplicity of the former with the modern feeling and ease of use of the latter. We shall see how this develops.

## 272

```
define[  fib[n]
  ?[
    =[ [n] [0] ]  [0]
    =[ [n] [1] ]  [1]
    +[
      fib[-[ [n] [1] ]]
      fib[-[ [n] [2] ]]
    ]
  ]
]

define[  [memo fib]
  memoize[fun[  [n]
    ?[
      =[ [n] [0] ]  [0]
      =[ [n] [1] ]  [1]
      +[
        memo fib[-[ [n] [1] ]]
        memo fib[-[ [n] [2] ]]
      ]
    ]
  ]]
]
```

## 273

```
define[  memoize[f]
  let[
    [table]  make table[]
    fun[  [x]
      let[
        [previously computed result]  lookup[ [x] [table] ]
        or[
          [previously computed result]
          let[
            [result]  f[x]
            [
              insert![ [x] [result] [table] ]
              [result]
            ]
          ]
        ]
      ]
    ]
  ]
]
```

## 274

```
define[  [a]  make wire[]  ]
define[  [b]  make wire[]  ]
define[  [c]  make wire[]  ]
```

## 275

```
define[  [d]  make wire[]  ]
define[  [e]  make wire[]  ]
define[  [s]  make wire[]  ]

or gate[ [a] [b] [d] ]

and gate[ [a] [b] [c] ]

inverter[ [c] [e] ]

and gate[ [d] [e] [s] ]

define[  half adder[ [a] [b] [s] [c] ]
  let[
    [d]  make wire[]
    [e]  make wire[]
    [
      or gate[ [a] [b] [d] ]
      and gate[ [a] [b] [c] ]
      inverter[ [c] [e] ]
      and gate[ [d] [e] [s] ]
      ['ok]
    ]
  ]
]
```

## 276

```
define[  full adder[ [a] [b] [c in] [sum] [c out] ]
  let[
    [s]  make wire[]
    [c1]  make wire[]
    [c2]  make wire[]
    [
      half adder[ [b] [c in] [s] [c1] ]
      half adder[ [a] [s] [sum] [c2] ]
      or gate[ [c1] [c2] [c out] ]
      ['ok]
    ]
  ]
]

get signal[<wire>]

set signal![ [<wire>] [<new value>] ]

add action![ [<wire>] [<procedure of no arguments>] ]
```

## 277

```
define[  inverter[ [input] [inverter] ]
  define[  invert input[]
    let[
      [new value]  logical not[get signal[input]]
      after delay[
        [inverter delay]
        fun[  []
          set signal![ [output] [new value] ]
        ]
      ]
    ]
  ]
  add action![ [input] [invert input] ]
  ['ok]
]

define[  logical not[s]
  ?[
    =[ [s] [0] ]  [1]
    =[ [s] [1] ]  [0]
    error[ ['Invalid signal] [s] ]
  ]
]

define[  and gate[ [a1] [a2] [output] ]
  define[  and action procedure[]
    let[
      [new value]  logical and[ get signal[a1] get signal[a2] ]
      after delay[
        [and gate delay]
        fun[ []
          set signal![ [output] [new value] ]
        ]
      ]
    ]
  ]
  add action![ [a1] [and action procedure] ]
  add action![ [a2] [and action procedure] ]
  ['ok]
]
```

## 279

```
define[  make wire[]
  let[
    [signal value]  [0]
    [action procedues]  [nil]
    [
      define[  set my signal![new value]
        ?[
          not[=[ [signal value] [new value] ]]  [
            set![ [signal value] [new value] ]
            call each[action procedures]
          ]
          ['done]
        ]
      ]
      
      define[  accept action procedure![proc]
        set![ [action procedures] cons[[proc][action procedures]] ]
        proc[]
      ]

      define[  dispatch[m]
        ?[
          eq?[ [m] ['get signal] ]  [signal value]
          eq?[ [m] ['set signal!] ]  [set my signal!]
          eq?[ [m] ['add action!] ]  [accept action procedure]
          error[ ['Unknown operation -- WIRE] [m] ]
        ]
      ]
      [dispatch]
    ]
  ]
]

define[  call each[procedures]
  ?[
    null?[procedures]  ['done]
    [
      car[procedures].[]
      call each[cdr[procedures]]
    ]
  ]
]
```

## 280

```
define[  get signal[wire]
  wire['get signal]
]

define[  set signal![ [wire] [new value] ]
  wire['set signal!].[new value]
]

define[  add action![ [wire] [action procedure] ]
  wire['add action!].[action procedure]
]

make agenda[]

empty agenda?[<agenda>]

first agenda item[<agenda>]

remove first agenda item![<agenda>]

add to agenda![ [<time>] [<action>] [<agenda>] ]

current time[<agenda>]
```

## 281

```
define[  after delay[ [delay] [action] ]
  add to agenda![
    +[ [delay] current time[the agenda] ]
    [action]
    [the agenda]
  ]
]

define[ propagate[]
  ?[
    empty agenda?[the agenda]  ['done]
    let[
      [first item]  first agenda item[the agenda]
      [
        first item[]
        remove first agenda item![the agenda]
        propagate[]
      ]
    ]
  ]
]

define[  probe[ [name] [wire] ]
  add action![
    [wire]
    fun[  []
      newline[]
      display[name]
      display[' ']
      display[ current time[the agenda] ]
      display['  New value = ']
      display[ get signal[wire] ]
    ]
  ]
]

define[  [the agenda]  make agenda[]  ]
define[  [inverter delay]  [2]  ]
define[  [and gate delay]  [3]  ]
define[  [or gate delay]  [5]  ]
```

## 282

```
define[  [input 1]  make wire[]  ]
define[  [input 2]  make wire[]  ]
define[  [sum]  make wire[]  ]
define[  [carry]  make wire[]  ]

probe[ ['sum] [sum] ]

probe[ ['carry] [carry] ]

half adder[ [input 1] [input 2] [sum] [carry] ]

set signal![ [input 1] [1] ]

propagate[]

set signal![ [input 2] [1] ]

propagate[]

define[  accept action procedure![proc]
  set![ [action procedures] cons[[proc][action procedures]] ]
]
```

## 283

```
define[  make time segment[ [time] [queue] ]
  cons[ [time] [queue] ]
]

define[  segment time[s]  car[s]  ]

define[  segment queue[s]  cdr[s]  ]

define[  make agenda[]  list[0]  ]

define[  current time[agenda]  car[agenda]  ]

define[  set current time![ [agenda] [time] ]
  set car![ [agenda] [time] ]
]

define[  segments[agenda]  cdr[agenda]  ]

define[  set segments![ [agenda] [segments] ]
  set cdr![ [agenda] [segments] ]
]

define[  first segment[agenda]  car[segments[agenda]]  ]

define[  rest segments[agenda]  cdr[segments[agenda]]  ]
```

## 284

```
define[  empty agenda?[agenda]
  null?[segments[agenda]]
]

define[  add to agenda![ [time] [action] [agenda] ]
  define[  belongs before?[segments]
    or[
      null?[segments]
      <[ [time] segment time[car[segments]] ]
    ]
  ]
  define[  make new time segment[ [time] [action] ]
    let[
      [q]  make queue[]
      [
        insert queue![ [q] [action] ]
        make time segment[ [time] [q] ]
      ]
    ]
  ]
  define[  add to segments![segments]
    ?[
      =[ segment time[car[segments]] [time] ]  insert queue![
        segment queue[car[segments]]
        [action]
      ]
      let[
        [rest]  cdr[segments]
        ?[
          belongs before?[rest]  set cdr![
            [segments]
            cons[
              make new time segment[ [time] [action] ]
              cdr[segments]
            ]
          ]
          add to segments![rest]
        ]
      ]
    ]
  ]
  let[
    [segments]  segments[agenda]
    ?[
      belongs before?[segments]  set segments![
        [agenda]
        cons[
          make new time segment[ [time] [action] ]
          [segments]
        ]
      ]
      add to segments![segments]
    ]
  ]
]
```

## 285

```
define[  remove first agenda item![agenda]
  let[
    [q]  segment queue[first segment[agenda]]
    [
      delete queue![q]
      ?[
        empty queue?[q]  set segments![ [agenda] rest segments[agenda] ]
      ]
    ]
  ]
]

define[  first agenda item[agenda]
  ?[
    empty agenda?[agenda]  error['Agenda is empty -- FIRST-AGENDA-ITEM']
    let[
      [first seg]  first segment[agenda]
      [
        set current time![ [agenda] segment time[first seg] ]
        front queue[segment queue[first seg]]
      ]
    ]
  ]
]
```

## 287

```
define[  [C]  make connector[]  ]
define[  [F]  make connector[]  ]
celsius fahrenheit converter[ [C] [F] ]

define[  celsius fahrenheit converter[ [c] [f] ]
  let[
    [u]  make connector[]
    [v]  make connector[]
    [w]  make connector[]
    [x]  make connector[]
    [y]  make connector[]
    [
      multiplier[ [c] [w] [u] ]
      multiplier[ [v] [x] [u] ]
      adder[ [v] [y] [f] ]
      constant[ [9] [w] ]
      constant[ [5] [x] ]
      constant[ [32] [y] ]
      ['ok]
    ]
  ]
]
```

## 288

```
probe[ ['Celsius temp] [C] ]
probe[ ['Fahrenheit temp] [F] ]

set value![ [C] [25] ['user] ]

set value![ [F] [212] ['user] ]

forget value![ [C] ['user] ]
```

## 289

```
set value![ [F] [212] ['user] ]

has value?[<connector>]

get value[<connector>]

set value![ [<connector>] [<new value>] [<informant>] ]

forget value![ [<connector>] [<retractor>] ]

connect[ [<connector>] [<new constraint>] ]
```

## 290

```
define[  adder[ [a1] [a2] [sum] ]
  define[  process new value[]
    ?[
      and[ has value?[a1] has value?[a2] ]  set value![
        [sum]
        +[ get value[a1] get value[a2] ]
        [me]
      ]
      and[ has value?[a1] has value?[sum] ]  set value![
        [a2]
        -[ get value[sum] get value[a1] ]
        [me]
      ]
      and[ has value?[a2] has value?[sum] ]  set value![
        [a1]
        -[ get value[sum] get value[a2] ]
        [me]
      ]
    ]
  ]
  define[  process forget value[]
    forget value![ [sum] [me] ]
    forget value![ [a1] [me] ]
    forget value![ [a2] [me] ]
    process new value[]
  ]
  define[  me[request]
    ?[
      eq?[ [request] ['I have a value] ]  process new value[]
      eq?[ [request] ['I lost my value] ]  process forget value[]
      error[ ['Unknown request -- ADDER] [request] ]
    ]
  ]
  connect[ [a1] [me] ]
  connect[ [a2] [me] ]
  connect[ [sum] [me] ]
  [me]
]

define[  inform about value[constraint]
  constraint['I have a value]
]

define[  inform about no value[constraint]
  constraint['I lost my value]
]
```

## 291

```
define[  multipiler[ [m1] [m2] [product] ]
  define[  process new value[]
    ?[
      or[
        and[ has value?[m1] =[get value[m1][0]] ]
        and[ has value?[m2] =[get value[m2][0]] ]
      ]  set value![ [product] [0] [me] ]
      and[ has value?[m1] has value?[m2] ]  set value![
        [product]
        *[ get value[m1] get value[m2] ]
        [me]
      ]
      and[ has value?[product] has value?[m1] ]  set value![
        [m2]
        /[ get value[product] get value[m1] ]
        [me]
      ]
      and[ has value?[product] has value?[m2] ]  set value![
        [m1]
        /[ get value[product] get value[m2] ]
        [me]
      ]
    ]
  ]
  define[  process forget value[]
    forget value![ [product] [me] ]
    forget value![ [m1] [me] ]
    forget value![ [m2] [me] ]
    process new value[]
  ]
  define[  me[request]
    ?[
      eq?[ [request] ['I have a value] ]  process new value[]
      eq?[ [request] ['I lost my value] ]  process forget value[]
      error[ ['Unknown request -- MULTIPLIER] [request] ]
    ]
  ]
  connect[ [m1] [me] ]
  connect[ [m2] [me] ]
  connect[ [product] [me] ]
  [me]
]
```

## 292

```
define[  constant[ [value] [connector] ]
  define[  me[request]
    error[ ['Unknown request -- CONSTANT] [request] ]
  ]
  connect[ [connector] [me] ]
  set value![ [connector] [value] [me] ]
  [me]
]

define[  probe[ [name] [connector] ]
  define[  print probe[value]
    newline[]
    display['Probe: ']
    display[name]
    display[' = ']
    display[value]
  ]
  define[  process new value[]
    print probe[get value[connector]]
  ]
  define[  process forget value[]
    print probe['?]
  ]
  define[  me[request]
    ?[
      eq?[ [request] ['I have a value] ]  process new value[]
      eq?[ [request] ['I lost my value] ]  process forget value[]
      error[ ['Unknown request -- PROBE] [request] ]
    ]
  ]
  connect[ [connector] [me] ]
  [me]
]
```

## 293

```
define[  make connector[]
  let[
    [value]  [false]
    [informant]  [false]
    [constraints]  [nil]
    [
      define[  set my value[ [newval] [setter] ]
        ?[
          not[has value?[me]]  [
            set![ [value] [newval] ]
            set![ [informant] [setter] ]
            for each except[
              [setter]
              [inform about value]
              [constraints]
            ]
          ]
          not[=[ [value] [newval] ]]  error[ ['Contradiction] list[[value][newval]] ]
          ['ignored]
        ]
      ]
      define[  forget my value[retractor]
        ?[
          eq?[ [retractor] [informant] ]  [
            set![ [informant] [false] ]
            for each except[
              [retractor]
              [inform about no value]
              [constraints]
            ]
          ]
          ['ignored]
        ]
      ]
      define[  connect[new constraint]
        ?[
          not[memq[ [new constraint] [constraints] ]]  set![
            [constraints]
            cons[ [new constraint] [constraints] ]
          ]
        ]
        ?[
          has value?[me]  inform about value[new constraint]
        ]
        ['done]
      ]
      define[  me[request]
        ?[
          eq?[ [request] ['has value?] ]  ?[ [informant] [true] [false] ]
          eq?[ [request] ['value] ]  [value]
          eq?[ [request] ['set value!] ]  [set my value]
          eq?[ [request] ['forget] ]  [forget my value]
          eq?[ [request] ['connect] ]  [connect]
          error[ ['Unknown operation -- CONNECTOR] [request] ]
        ]
      ]
      [me]
    ]
  ]
]
```

## 294

```
define[  for each except[ [exception] [procedure] [list] ]
  define[  loop[items]
    ?[
      null?[items]  ['done]
      eq?[ car[items] [exception] ]  loop[cdr[items]]
      [
        procedure[car[items]]
        loop[cdr[items]]
      ]
    ]
  ]
  loop[list]
]

define[  has value?[connector]
  connector['has value?]
]

define[  get value[connector]
  connector['value]
]

define[  set value![ [connector] [new value] [informant] ]
  connector['set value!].[ [new value] [informant] ]
]

define[  forget value![ [connector] [retractor] ]
  connector['forget].[retractor]
]

define[  connect[ [connector] [new constraint] ]
  connector['connect].[new constraint]
]
```

## 295

```
define[  squarer[ [a] [b] ]
  define[  process new value[]
    ?[
      has value?[b]  ?[
        <[ get value[b] [0] ]  error[ ['square less than 0 -- SQUARER] get value[b] ]
        <alternative 1>
      ]
      <alternative 2>
    ]
  ]
  define[  process forget value[]  <body 1>  ]
  define[  me[request]  <body 2>  ]
  <rest of definition>
  [me]
]

define[  [a]  make connector[]  ]
define[  [b]  make connector[]  ]
set value![ [a] [10] ['user] ]

for each except[ [setter] [inform about value] [constraints] ]
```

## 296

```
define[  celsius fahrenheit converter[x]
  c+[
    c*[  c/[ cv[9] cv[5] ]  [x]  ]
    cv[32]
  ]
]

define[  [C]  make connector[]  ]
define[  [F]  celsius fahrenheit converter[C]  ]

define[  c+[ [x] [y] ]
  let[
    [x]  make connector[]
    [
      adder[ [x] [y] [z] ]
      [z]
    ]
  ]
]

v sum[ [a] [b] [temp1] ]
v sum[ [c] [d] [temp2] ]
v prod[ [temp1] [temp2] [answer] ]

define[  [answer]  v prod[ v sum[[a][b]] v sum[[c][d]] ]  ]
```

## 297

```
withdraw[25]

withdraw[25]
```

## 299

```
define[  withdraw[amount]
  ?[
    >=[ [balance] [amount] ]  [
      set![ [balance] -[[balance][amount]] ]
      [balance]
    ]
    ['Insufficient funds]
  ]
]

set![ [balance] -[[balance][amount]] ]
```

## 303

```
set![ [balance] +[[balance][10]] ]
set![ [balance] -[[balance][20]] ]
set![  [balance]  -[ [balance] /[[balance][2]] ]  ]
```

## 304

```
parallel execute[ [<p_1>] [<p_2>] ... [<p_k>] ]

define[  [x]  [10]  ]

parallel execute[
  fun[  []  set![ [x] *[[x][x]] ]  ]
  fun[  []  set![ [x] +[[x][1]] ]  ]
]
```

## 305

```
define[  [x]  [10]  ]

define[  [s]  make serializer[]  ]

parallel execute[
  s[fun[  []  set![ [x] *[[x][x]] ]  ]]
  s[fun[  []  set![ [x] +[[x][1]] ]  ]]
]

define[  make account[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      ['Insufficient funds]
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  let[
    [protected]  make serializer[]
    [
      define[  dispatch[m]
        ?[
          eq?[ [m] ['withdraw] ]  protected[withdraw]
          eq?[ [m] ['deposit] ]  protected[deposit]
          eq?[ [m] ['balance] ]  [balance]
          error[ ['Unknown request -- MAKE-ACCOUNT] [m] ]
        ]
      ]
      [dispatch]
    ]
  ]
]
```

## 306

```
define[  [x]  [10]  ]

define[  [s]  make serializer[]  ]

parallel execute[
  fun[  []  set![ [x]
    s[fun[  []  *[[x][x]]  ]].[]
  ]  ]
  s[fun[  []  set![ [x] +[[x][1]] ]  ]]
]

define[  [x]  [10]  ]

parallel execute[
  fun[  []  set![ [x] *[[x][x]] ]  ]
  fun[  []  set![ [x] +[[x][x][x]] ]  ]
]

define[  [x]  [10]  ]

define[  [s]  make serializer[]  ]

parallel execute[
  s[fun[  []  set![ [x] *[[x][x]] ]  ]]
  s[fun[  []  set![ [x] +[[x][x][x]] ]  ]]
]

define[  make account[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      ['Insufficient funds]
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  continued on next page
```

## 307

```
  let[
    [protected]  make serializer[]
    [
      define[  dispatch[m]
        ?[
          eq?[ [m] ['withdraw] ]  protected[withdraw]
          eq?[ [m] ['deposit] ]  protected[deposit]
          eq?[ [m] ['balance] ]  [
            protected[fun[  []  [balance]  ]].[]   serialized
          ]
          error[ ['Unknown request -- MAKE-ACCOUNT] [m] ]
        ]
      ]
      [dispatch]
    ]
  ]
]

define[  make account[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      ['Insufficient funds]
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  let[
    [protected]  make serializer[]
    let[
      [protected withdraw]  protected[withdraw]
      [protected deposit]  protected[deposit]
      [
        define[  dispatch[m]
          ?[
            eq?[ [m] ['withdraw] ]  [protected withdraw]
            eq?[ [m] ['deposit] ]  [protected deposit]
            eq?[ [m] ['balance] ]  [balance]
            error[ ['Unknown request -- MAKE-ACCOUNT] [m] ]
          ]
        ]
        [dispatch]
      ]
    ]
  ]
]
```

## 308

```
define[  exchange[ [account1] [account2] ]
  let[
    [difference]  -[
      account1['balance]
      account2['balance]
    ]
    [
      account1['withdraw].[difference]
      account2['deposit].[difference]
    ]
  ]
]
```

## 309

```
define[  make account and serializer[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      ['Insufficient funds]
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  let[
    [balance serializer]  make serializer[]
    [
      define[  dispatch[m]
        ?[
          eq?[ [m] ['withdraw] ]  [withdraw]
          eq?[ [m] ['deposit] ]  [deposit]
          eq?[ [m] ['balance] ]  [balance]
          eq?[ [m] ['serializer] ]  [balance serializer]
          error[ ['Unknown request -- MAKE-ACCOUNT] [m] ]
        ]
      ]
      [dispatch]
    ]
  ]
]

define[  deposit[ [account] [amount] ]
  let[
    [s]  account['serializer]
    [d]  account['deposit]
    [s[d].[amount]]
  ]
]

define[  serialized exchange[ [account1] [account2] ]
  let[
    [serializer1]  account1['serializer]
    [serializer2]  account2['serializer]
    [
      serializer1[serializer2[exchange]].[
        [account1]
        [account2]
      ]
    ]
  ]
]
```

## 310

```
define[  transfer[ [from account] [to account] [amount] ]
  from account['withdraw].[amount]
  to account['deposit].[amount]
]

define[  make account and serializer[balance]
  define[  withdraw[amount]
    ?[
      >=[ [balance] [amount] ]  [
        set![ [balance] -[[balance][amount]] ]
        [balance]
      ]
      ['Insufficient funds]
    ]
  ]
  define[  deposit[amount]
    set![ [balance] +[[balance][amount]] ]
    [balance]
  ]
  let[
    [balance serializer]  make serializer[]
    [
      define[  dispatch[m]
        ?[
          eq?[ [m] ['withdraw] ]  balance serializer[withdraw]
          eq?[ [m] ['deposit] ]  balance serializer[deposit]
          eq?[ [m] ['balance] ]  [balance]
          eq?[ [m] ['serializer] ]  [balance serializer]
          error[ ['Unknown request -- MAKE-ACCOUNT] [m] ]
        ]
      ]
      [dispatch]
    ]
  ]
]
```

## 311

```
define[  deposit[ [account] [amount] ]
  account['deposit].[amount]
]

define[  make serializer[]
  let[
    [mutex]  make mutex[]
    fun[  [p]
      define[  serialized p[...[args]]
        mutex['acquire]
        let[
          [val]  apply[ [p] [args] ]
          [
            mutex['release]
            [val]
          ]
        ]
      ]
      [serialized p]
    ]
  ]
]
```

## 312

```
define[  make mutex[]
  let[
    [cell]  list[false]
    [
      define[  the mutex[m]
        ?[
          eq?[ [m] ['acquire] ]  ?[
            test and set![cell]  the mutex['acquire]
          ]   retry
          eq?[ [m] ['release] ]  clear![cell]
        ]
      ]
      [the mutex]
    ]
  ]
]

define[  clear![cell]
  set car![ [cell] [false] ]
]

define[  test and set![cell]
  ?[
    car[cell]  [true]
    [
      set car![ [cell] [true] ]
      [false]
    ]
  ]
]
```

## 313

```
define[  test and set![cell]
  without interrupts[
    fun[  []
      ?[
        car[cell]  [true]
        [
          set car![ [cell] [true] ]
          [false]
        ]
      ]
    ]
  ]
]
```

## 318

```
define[  sum primes[ [a] [b] ]
  define[  iter[ [count] [accum] ]
    ?[
      >[ [count] [b] ]  [accum]
      prime?[count]  iter[ +[[count][1]] +[[count][accum]] ]
      iter[ +[[count][1]] [accum] ]
    ]
  ]
  iter[ [a] [0] ]
]

define[  sum primes[ [a] [b] ]
  accumulate[
    [+]
    [0]
    filter[ [prime?] enumerate interval[[a][b]] ]
  ]
]

car[  cdr[ filter[
  [prime?]
  enumerate interval[ [10000] [1000000] ]
] ]  ]
```

## 319

```
stream car[  cons stream[ [x] [y] ]  ] = [x]
stream cdr[  cons stream[ [x] [y] ]  ] = [y]

define[  stream ref[ [s] [n] ]
  ?[
    =[ [n] [0] ]  stream car[s]
    stream ref[ stream cdr[s] -[[n][1]] ]
  ]
]
```

## 320

```
define[  stream map[ [proc] [s] ]
  ?[
    stream null?[s]  [the empty stream]
    cons stream[
      proc[stream car[s]]
      stream map[ [proc] stream cdr[s] ]
    ]
  ]
]

define[  stream for each[ [proc] [s] ]
  ?[
    stream null?[s]  ['done]
    [
      proc[stream car[s]]
      stream for each[ [proc] stream cdr[s] ]
    ]
  ]
]

define[  display stream[s]
  stream for each[ [display line] [s] ]
]

define[  display line[x]
  newline[]
  display[x]
]
```

## 321

```
cons stream[ [<a>] [<b>] ]

cons stream[ [<a>] delay[<b>] ]

define[  stream car[stream]  car[stream]  ]

define[  stream cdr[stream]  force[cdr[stream]]  ]

stream car[
  stream cdr[
    stream filter[
      [prime?]
      stream enumerate interval[ [10000] [1000000] ]
    ]
  ]
]

define[  stream enumerate interval[ [low] [high] ]
  ?[
    >[ [low] [high] ]  [the empty stream]
    cons stream[
      [low]
      stream enumerate interval[ +[[low][1]] [high] ]
    ]
  ]
]
```

## 322

```
cons[
  [10000]
  delay[stream enumerate interval[ [10001] [1000000] ]]
]

define[  stream filter[ [pred] [stream] ]
  ?[
    stream null?[stream]  [the empty stream]
    pred[stream car[stream]]  cons stream[
      stream car[stream]
      stream filter[
        [pred]
        stream cdr[stream]
      ]
    ]
    stream filter[ [pred] stream cdr[stream] ]
  ]
]

cons[
  [10001]
  delay[stream enumerate interval[ [10002] [1000000] ]]
]

cons stream[
  stream car[stream]
  stream filter[ [pred] stream cdr[stream] ]
]

cons[
  [10007]
  delay[stream filter[
    [prime?]
    cons[
      [10008]
      delay[stream enumerate interval[
        [10009]
        [1000000]
      ]]
    ]
  ]]
]
```

## 323

```
cons[
  [10009]
  delay[stream filter[
    [prime?]
    cons[
      [10010]
      delay[stream enumerate interval[
        [10011]
        [1000000]
      ]]
    ]
  ]]
]

delay[<exp>]

fun[ [] [<exp>] ]

define[  force[delayed object]
  delayed object[]
]
```

## 324

```
define[  memo proc[proc]
  let[
    [already run?]  [false]
    [result]  [false]
    fun[  []
      ?[
        not[already run?]  [
          set![ [result] proc[] ]
          set![ [already run?] [true] ]
          [result]
        ]
        [result]
      ]
    ]
  ]
]

memo proc[fun[  []  [<exp>]  ]]
```

## 325

```
define[  stream map[ [proc] ...[argstreams] ]
  ?[
    <??>[car[argstreams]]  [the empty stream]
    <??>[
      apply[ [proc] map[[<??>][argstreams]] ]
      apply[
        [stream map]
        cons[ [proc] map[[<??>][argstreams]] ]
      ]
    ]
  ]
]

define[  show[x]
  display line[x]
  [x]
]

define[  [x]  stream map[ [show] stream enumerate interval[[0][10]] ]  ]

stream ref[ [x] [5] ]

stream ref[ [x] [7] ]

define[  [sum]  [0]  ]

define[  accum[x]
  set![ [sum] +[[x][sum]] ]
  [sum]
]

define[  [seq]  stream map[ [accum] stream enumerate interval[[1][20]] ]  ]
define[  [y]  stream filter[ [even?] [seq] ]  ]
define[  [z]  stream filter[ 
  fun[  [x]  =[ remainder[[x][5]] [0] ]  ] 
  [seq] 
]  ]

stream ref[ [y] [7] ]

display stream[z]
```

## 326

```
define[  integers starting from[n]
  cons stream[  [n]  integers starting from[ +[[n][1]] ]  ]
]

define[  integers  integers starting from[1]  ]

define[  divisible?[ [x] [y] ]  =[ remainder[[x][y]] [0] ]  ]

define[  [no sevens]
  stream filter[
    fun[  [x]  not[divisible?[ [x] [7] ]]  ]
    [integers]
  ]
]

stream ref[ [no sevens] [100] ]

define[  fibgen[ [a] [b] ]
  cons stream[  [a]  fibgen[ [b] +[[a][b]] ]  ]
]
```

## 327

```
define[  [fibs]  fibgen[ [0] [1] ]  ]

define[  sieve[stream]
  cons[
    stream car[stream]
    sieve[stream filter[
      fun[  [x]  not[divisible?[ [x] stream car[stream] ]]  ]
      stream cdr[stream]
    ]]
  ]
]

define[  [primes]  sieve[integers starting from[2]]  ]

stream ref[ [primes] [50] ]
```

## 328

```
define[  [ones]  cons stream[ [1] [ones] ]  ]
```

## 329

```
define[  add streams[ [s1] [s2] ]
  stream map[ [+] [s1] [s2] ]
]

define[  [integers]  cons stream[ [1] add streams[[ones][integers]] ]  ]

define[  [fibs]
  cons stream[
    [0]
    cons stream[
      [1]
      add streams[
        stream cdr[fibs]
        [fibs]
      ]
    ]
  ]
]

define[  scale stream[ [stream] [factor] ]
  stream map[  fun[ [x] *[[x][factor]] ]  [stream]  ]
]
```

## 330

```
define[  [double]  cons stream[ [1] scale stream[[double][2]] ]  ]

define[  [primes]
  cons stream[
    [2]
    stream filter[  [prime?]  integers starting from[3]  ]
  ]
]

define[  prime?[n]
  define[  iter[ps]
    ?[
      >[ square[stream car[ps]] [n] ]  [true]
      divisible?[ [n] stream car[ps] ]  [false]
      iter[ stream cdr[ps] ]
    ]
  ]
  iter[primes]
]

define[  [s]  cons stream[ [1] add streams[[s][s]] ]  ]
```

## 331

```
define[  [factorials]  cons stream[ [1] mul streams[[??][??]] ]  ]

define[  merge[ [s1] [s2] ]
  ?[
    stream null?[s1]  [s2]
    stream null?[s2]  [s1]
    let[
      [s1car]  stream car[s1]
      [s2car]  stream car[s2]
      ?[
        <[ [s1car] [s2car] ]
        cons stream[  [s1car]  merge[ stream cdr[s1] [s2] ]  ]
        >[ [s1car] [s2car] ]
        cons stream[  [s2car]  merge[ [s1] stream cdr[s2] ]  ]
        
        cons stream[
          [s1car]
          merge[
            stream cdr[s1]
            stream cdr[s2]
          ]
        ]
      ]
    ]
  ]
]

define[  [S]  cons stream[ [1] merge[[??][??]] ]  ]
```

## 332

```
define[  expand[ [num] [den] [radix] ]
  cons stream[
    quotient[ *[[num][radix]] [den] ]
    expand[
      remainder[ *[[num][radix]] [den] ]
      [den]
      [radix]
    ]
  ]
]
```

## 333

```
define[  [exp series]
  cons stream[ [1] integrate series[exp series] ]
]

define[  [cosine series]  cons stream[ [1] [??] ]  ]

define[  [sine series]  cons stream[ [0] [??] ]  ]

define[  mul series[ [s1] [s2] ]
  cons stream[ [??] add streams[[??][??]] ]
]
```

## 334

```
define[  sqrt improve[ [guess] [x] ]
  average[  [guess]  /[ [x] [guess] ]  ]
]
```

## 335

```
define[  sqrt stream[x]
  define[  [guesses]
    cons stream[
      [1.0]
      stream map[
        fun[  [guess]  sqrt improve[ [guess] [x] ]  ]
        [guesses]
      ]
    ]
  ]
  [guesses]
]

display stream[ sqrt stream[2] ]

define[  pi summands[n]
  cons stream[
    /[ [1.0] [n] ]
    stream map[  [-]  pi summands[ +[[n][2]] ]  ]
  ]
]

define[  [pi stream]
  scale stream[  partial sums[ pi summands[1] ]  [4]  ]
]

display stream[pi stream]
```

## 336

```
define[  euler transform[s]
  let[
    [s0]  stream ref[ [s] [0] ]
    [s1]  stream ref[ [s] [1] ]
    [s2]  stream ref[ [s] [2] ]
    cons stream[
      -[
        [s2]
        /[
          square[-[[s2][s1]]]
          +[ [s0] *[[-2][s1]] [s2] ]
        ]  
      ]
      euler transform[stream cdr[s]]
    ]
  ]
]

display stream[euler transform[pi stream]]
```

## 337

```
define[  make tableau[ [transform] [s] ]
  cons stream[
    [s]
    make tableau[
      [transform]
      transform[s]
    ]
  ]
]

define[  accelerated sequence[ [transform] [s] ]
  stream map[
    [stream car]
    make tableau[ [transform] [s] ]
  ]
]

display stream[
  accelerated sequence[ [euler transform] [pi stream] ]
]

define[  sqrt stream[x]
  cons stream[
    [1.0]
    stream map[
      fun[  [guess]  sqrt improve[ [guess] [x] ]  ]
      sqrt stream[x]
    ]
  ]
]

define[  sqrt[ [x] [tolerance] ]
  stream limit[ sqrt stream[x] [tolerance] ]
]
```

## 339

```
stream filter[
  fun[  [pair]  prime?[+[ car[pair] cadr[pair] ]]  ]
  [int pairs]
]
```

## 340

```
stream map[
  fun[  [x]  list[ stream car[s] [x] ]  ]
  stream cdr[t]
]

define[  pairs[ [s] [t] ]
  cons stream[
    list[ stream car[s] stream car[t] ]
    <combine in some way>[
      stream map[
        fun[  [x]  list[ stream car[s] [x] ]  ]
        stream cdr[t]
      ]
      pairs[ stream cdr[s] stream cdr[t] ]
    ]
  ]
]

define[  stream append[ [s1] [s2] ]
  ?[
    stream null?[s1]  [s2]
    cons stream[
      stream car[s1]
      stream append[ stream cdr[s1] [s2] ]
    ]
  ]
]

pairs[ [integers] [integers] ]
```

## 341

```
define[  interleave[ [s1] [s2] ]
  ?[
    stream null?[s1]  [s2]
    cons stream[
      stream car[s1]
      interleave[ [s2] stream cdr[s1] ]
    ]
  ]
]

define[  pairs[ [s] [t] ]
  cons stream[
    list[ stream car[s] stream car[t] ]
    interleave[
      stream map[
        fun[  [x]  list[ stream car[s] [x] ]  ]
        stream cdr[t]
      ]
      pairs[ stream cdr[s] stream cdr[t] ]
    ]
  ]
]

define[  pairs[ [s] [t] ]
  interleave[
    stream map[
      fun[  [x]  list[ stream car[s] [x] ]  ]
      [t]
    ]
    pairs[ stream cdr[s] stream cdr[t] ]
  ]
]
```

## 343

```
define[  integral[ [integrand] [initial value] [dt] ]
  define[  [int]
    cons stream[
      [initial value]
      add streams[
        scale stream[ [integrand] [dt] ]
        [int]
      ]
    ]
  ]
  [int]
]
```

## 345

```
define[  make zero crossings[ [input stream] [last value] ]
  cons stream[
    sign change detector[ stream car[input stream] [last value] ]
    make zero crossings[
      stream cdr[input stream]
      stream car[input stream]
    ]
  ]
]

define[  [zero crossings]  make zero crossings[ [sense data] [0] ]  ]

define[  [zero crossings]
  stream map[ [sign change detector] [sense data] [<expression>] ]
]

define[  make zero crossings[ [input stream] [last value] ]
  let[
    [avpt]  /[ +[stream car[input stream][last value]] [2] ]
    cons stream[
      sign change detector[ [avpt] [last value] ]
      make zero crossings[
        stream cdr[input stream]
        [avpt]
      ]
    ]
  ]
]
```

## 346

```
define[  [int]
  cons stream[
    [initial value]
    add streams[
      scale stream[ [integrand] [dt] ]
      [int]
    ]
  ]
]
```

## 347

```
define[  solve[ [f] [y0] [dt] ]
  define[  [y]  integral[ [dy] [y0] [dt] ]  ]
  define[  [dy]  stream map[ [f] [y] ]  ]
  [y]
]

define[  integral[ [delayed integrand] [initial value] [dt] ]
  define[  [int]
    cons stream[
      [initial value]
      let[
        [integrand]  force[delayed integrand]
        add streams[
          scale stream[ [integrand] [dt] ]
          [int]
        ]
      ]
    ]
  ]
  [int]
]
```

## 348

```
define[  solve[ [f] [y0] [dt] ]
  define[  [y]  integral[ delay[dy] [y0] [dt] ]  ]
  define[  [dy]  stream map[ [f] [y] ]  ]
  [y]
]

stream ref[  solve[ fun[[y][y]] [1] [0.001] ]  [1000]  ]

define[  integral[ [integrand] [initial value] [dt] ]
  cons stream[
    [initial value]
    ?[
      stream null?[integrand]  [the empty stream]
      integral[
        stream cdr[integrand]
        +[
          *[ [dt] stream car[integrand] ]
          [initial value]
        ]
        [dt]
      ]
    ]
  ]
]
```

## 352

```
define[  [rand]
  let[
    [x]  [random init]
    fun[  []
      set![ [x] rand update[x] ]
      [x]
    ]
  ]
]

define[  [random numbers]
  cons stream[
    [random init]
    stream map[ [rand update] [random numbers] ]
  ]
]
```

## 353

```
define[  [cesaro stream]
  map successive pairs[
    fun[  [ [r1] [r2] ]  =[ gcd[[r1][r2]] [1] ]  ]
    [random numbers]
  ]
]

define[  map successive pairs[ [f] [s] ]
  cons stream[
    f[  stream car[s]  stream car[ stream cdr[s] ]  ]
    map successive pair[  [f]  stream cdr[ stream cdr[s] ]  ]
  ]
]

define[  monte carlo[ [experiment stream] [passed] [failed] ]
  define[  next[ [passed] [failed] ]
    cons stream[
      /[ [passed] +[[passed][failed]] ]
      monte carlo[
        stream cdr[experiment stream]
        [passed]
        [failed]
      ]
    ]
  ]
  ?[
    stream car[experiment stream]  next[ +[[passed][1]] [failed] ]
    next[ [passed] +[[failed][1]] ]
  ]
]

define[  [pi]
  stream map[
    fun[  [p]  sqrt[ /[[6][p]] ]  ]
    monte carlo[ [cesaro stream] [0] [0] ]
  ]
]
```

## 354

```
define[  make simplified withdraw balance[]
  fun[  [amount]
    set![ [balance] -[[balance][amount]] ]
    [balance]
  ]
]
```

## 355

```
define[  stream withdraw[ [balance] [amount stream] ]
  cons stream[
    [balance]
    stream withdraw[
      -[ [balance] stream car[amount stream] ]
      stream cdr[amount stream]
    ]
  ]
]
```

## Chapter 4: Metalinguistic Abstraction

My favorite part!

## 365

```
define[  eval[ [exp] [env] ]
  ?[
    self evaluating?[exp]  [exp]
    variable?[exp]  lookup variable value[ [exp] [env] ]
    quoted?[exp]  text of quotation[exp]
    assignment?[exp]  eval assignmenet[ [exp] [env] ]
    definition?[exp]  eval definition[ [exp] [env] ]
    if?[exp]  eval if[ [exp] [env] ]
    lambda?[exp]  make procedure[
      lambda parameters[exp]
      lambda body[exp]
      [env]
    ]
    begin?[exp]  eval sequence[ begin actions[exp] [env] ]
    cond?[exp]  eval[ cond->if[exp] [enc] ]
    application?[exp]  apply[
      eval[ operator[exp] [env] ]
      list of values[ operands[exp] [env] ]
    ]
    error[ ['Unknown expression type -- EVAL] [exp] ]
  ]
]
```

Now let's slightly modify that to match how Jevkalk happens to be defined:

```
define[  evalsub[ [exp] [env] ]
  ?[
    self evaluating?[exp]  [exp]
    variable?[exp]  lookup variable value[ [exp] [env] ]
    quoted?[exp]  text of quotation[exp]
    assignment?[exp]  eval assignmenet[ [exp] [env] ]
    definition?[exp]  eval definition[ [exp] [env] ]
    cond?[exp]  eval cond[ [exp] [env] ]
    fun?[exp]  make procedure[
      fun parameters[exp]
      fun body[exp]
      [env]
    ]
    block?[exp]  eval sequence[ block actions[exp] [env] ]
    application?[exp]  apply[
      eval[ operator[exp] [env] ]
      list of values[ operands[exp] [env] ]
    ]
    error[ ['Unknown expression type -- EVAL] [exp] ]
  ]
]
```

## 366

```
define[  apply[ [procedure] [arguments] ]
  ?[
    primitive procedure?[procedure]  apply primitive procedure[
      [procedure]
      [arguments]
    ]
    compound procedure?[procedure]  eval sequence[
      procedure body[procedure]
      extend environment[
        procedure parameters[procedure]
        [arguments]
        procedure environment[procedure]
      ]
    ]
    error[
      ['Unknown procedure type -- APPLY]
      [procedure]
    ]
  ]
]
```

## 367

```
define[  list of values[ [exps] [env] ]
  ?[
    no operands?[exps]  [nil]
    cons[
      eval[ first operand[exps] [env] ]
      list of values[ rest operands[exps] [env] ]
    ]
  ]
]

define[  eval if[ [exp] [env] ]
  ?[
    true?[eval[ if predicate[exp] [env] ]]  eval[ if consequent[exp] [env] ]
    eval[ if alternative[exp] [env] ]
  ]
]

define[  eval sequence[ [exps] [env] ]
  ?[
    last exp?[exps]  eval[ first exp[exps] [env] ]
    [
      eval[ first exp[exps] [env] ]
      eval sequence[ rest exps[exps] [env] ]
    ]
  ]
]
```

## 368

```
define[  eval assignment[ [exp] [env] ]
  set variable value![
    assignment variable[exp]
    eval[ assignment value[exp] [env] ]
    [env]
  ]
  ['ok]
]

define[  eval definition[ [exp] [env] ]
  define variable![
    definition variable[exp]
    eval[ definition value[exp] [env] ]
    [env]
  ]
  ['ok]
]
```

## 369

```
define[  self evaluating?[exp]
  ?[
    number?[exp]  [true]
    string?[exp]  [true]
    [false]
  ]
]

define[  variable?[exp]  symbol?[exp]  ]

define[  quoted?[exp]  tagged list?[ [exp] ['quote] ]  ]

define[  text of quotation[exp]  cadr[exp]  ]

define[  tagged list?[ [exp] [tag] ]
  ?[
    pair?[exp]  eq?[ car[exp] [tag] ]
    [false]
  ]
]

define[  assignment?[exp]
  tagged list?[ [exp] ['set!] ]
]

define[  assignment variable[exp]  cadr[exp]  ]

define[  assignment value[exp]  caddr[exp]  ]
```

To better match Jevkalk we'd do something like:

```
note: ignoring definitions of number? and string? for now
define[  self evaluating?[exp]
  ?[
    number?[exp]  [true]
    string?[exp]  [true]
    [false]
  ]
]

note: ignoring definition of identifier? for now
define[  variable?[exp]  identifier?[exp]  ]

define[  quoted?[exp]  prefix=[ [exp] ['quote] ]  ]

define[  text of quotation[exp]  [exp].jevko[]  ]

define[  prefix=[ [exp] [tag] ]
  ?[
    subjevko?[exp]  eq?[ prefix[exp] [tag] ]
    [false]
  ]
]

define[  assignment?[exp]
  prefix=[ [exp] ['set!] ]
]

define[  assignment variable[exp]  [exp].jevko[].subs[0]  ]

define[  assignment value[exp]  [exp].jevko[].subs[1]  ]
```

## 370

Dumb translation from Scheme:

```
define[  definition?[exp]
  tagged list?[ [exp] ['define] ]
]

define[  definition variable[exp]
  ?[
    symbol?[cadr[exp]]  cadr[exp]
    caadr[exp]
  ]
]

define[  definition value[exp]
  ?[
    symbol?[cadr[exp]]  caddr[exp]
    make lambda[
      cdadr[exp]   formal parameters
      cddr[exp]    body
    ]
  ]
]

define[  lambda?[exp]  tagged list?[ [exp] ['lambda] ]  ]

define[  lambda parameters[exp]  cadr[exp]  ]

define[  lambda body[exp]  cddr[exp]  ]

define[  make lambda[ [parameters] [body] ]
  cons[ ['lambda] cons[[parameters][body]] ]
]
```

However the Jevkalk forms are not like Scheme, but instead:

```
define[  [<var>]  [<value>]  ]

define[  <var>[<parameter>]  [<body>]  ]
define[  <var>[ [<parameter_1>] ... [<parameter_n>] ]  [<body>]  ]

define[  [<var>]  fun[ [<parameter>] [<body>] ]  ]
define[  [<var>]  fun[ [[<parameter_1>]...[<parameter_n>]] [<body>] ]  ]
```

Therefore we would have something like:

```
define[  definition?[sub]
  prefix=[ [sub] ['define] ]
]

define[  definition variable[sub]
  define[  [first]  [[sub].jevko[].subs[0]]  ]
  ?[
    identifier?[first]  [[first].jevko[].suffix[]]
    [[first].prefix[]]
  ]
]

define[  definition value[sub]
  define[  [j]  [[sub].jevko[]]  ]
  define[  [first]  [[j].subs[0]]  ]
  ?[
    identifier?[first]  [[j].subs[1]]
    make fun[
      note: using whole jevko rather than only its subs
      [[first].jevko[]]        formal parameters
      [[j].subs[].slice[1]]    body
    ]
  ]
]

define[  fun?[exp]  prefix[ [exp] ['fun] ]  ]

define[  fun parameters[exp]  [[exp].jevko[].subs[0].jevko[].subs[]]  ]

define[  fun body[exp]  [[exp].jevko[].subs[0].slice[1]]  ]

define[  make fun[ [parameters] [body] ]
  subjevko[
    ['fun]  
    jevko[ 
      list[
        subjevko[ ['] [parameters] ]
        note: assuming list can handle special ...spread parameters
        ...[body]
      ]
      note: assume default suffix blank
    ] 
  ]
]
```

## 371

```
define[  if?[exp]  tagged list?[ [exp] ['if] ]  ]

define[  if predicate[exp]  cadr[exp]  ]

define[  if consequent[exp]  caddr[exp]  ]

define[  if alternative[exp]
  ?[
    not[null?[cdddr[exp]]]  cadddr[exp]
    ['false]
  ]
]

define[  make if[ [predicate] [consequent] [alternative] ]
  list[ ['if'] [predicate] [consequent] [alternative] ]
]

define[  begin?[exp]  tagged list?[ [exp] ['begin] ]  ]

define[  begin actions[exp]  cdr[exp]  ]

define[  last exp?[seq]  null?[cdr[seq]]  ]

define[  first exp[seq]  car[seq]  ]

define[  rest exps[seq]  cdr[seq]  ]
```

Jevkalk version:

```
(skipping if)

define[  block?[exp]  prefix=[ [exp] ['] ]  ]

define[  block actions[exp]  [[exp].jevko[].subs[]]  ]

define[  last exp?[seq]  =[ [[seq].length[]] [1] ]  ]

define[  first exp[seq]  [[seq].[0]]  ]

define[  rest exps[seq]  [[seq].slice[1]]  ]
```

## 372

```
define[  sequence->exp[seq] 
  ?[
    null?[seq]  [seq]
    last exp?[seq]  first exp[seq]
    make begin[seq]
  ]
]

define[  make begin[seq]  cons[ ['begin] [seq] ]  ]

define[  application?[exp]  pair?[exp]  ]

define[  operator[exp]  car[exp]  ]

define[  operands[exp]  cdr[exp]  ]

define[  no operands?[ops]  null?[ops]  ]

define[  first operand[ops]  car[ops]  ]

define[  rest operands[ops]  cdr[ops]  ]

?[
  >[ [x] [0] ]  [x]
  =[ [x] [0] ]  [ display['zero] [0] ]
  -[x]
]

only sensible to translate this literally at this point:
if[
  >[ [x] [0] ]  [x]
  if[
    =[ [x] [0] ]  begin[
      display['zero]
      [0]
    ]
    -[x]
  ]
]
```

Jevkalk version would be something like:

```
define[  sequence->exp[seq] 
  ?[
    null?[seq]  [seq]
    last exp?[seq]  first exp[seq]
    make block[seq]
  ]
]

define[  make block[seq]  subjevko[ ['] jevko[seq] ]  ]

define[  application?[exp]  subjevko?[exp]  ]

define[  operator[exp]  [[exp].prefix[]]  ]

define[  operands[exp]
  define[  [j]  [[exp].jevko[]]  ]
  ?[
    =[ [[j].subs[].length[]] [0] ]  list[ make identifier[[[j].suffix[]]] ]
    [[exp].jevko[].subs[]]
  ]
]

define[  no operands?[ops]  =[ [[ops].length[]] [0] ]  ]

define[  first operand[ops]  [[ops].[0]]  ]

define[  rest operands[ops]  [[ops].slice[1]]  ]
```

## 373

```
define[  cond?[exp]  tagged list?[ [exp] ['cond] ]  ]

define[  cond clauses[exp]  cdr[exp]  ]

define[  cond else clause?[clause]  eq?[ cond predicate[clause] ['else] ]  ]

define[  cond predicate[clause]  car[clause]  ]

define[  cond actions[clause]  cdr[clause]  ]

define[  cond->if[exp]
  expand clauses[ cond clauses[exp] ]
]

define[  expand clauses[clauses]
  ?[
    null?[clauses]  ['false]    no else clause
    let[
      [first]  car[clauses]
      [rest]  cdr[clauses]
      ?[
        cond else clause?[first]  ?[
          null?[rest]  sequence->exp[ cond actions[first] ]
          error[ [`ELSE clause isn't last -- COND->IF`] [clauses] ]
        ]
        make if[
          cond predicate[first]
          sequence->exp[ cond actions[first] ]
          expand clauses[rest]
        ]
      ]
    ]
  ]
]
```

## 375

```
?[
  assoc[  ['b]  list'[ [[a][1]] [[b][2]] ]  ]   =>[cadr]
  [false]
]

let*[
  [x]  [3]
  [y]  +[ [x] [2] ]
  [z]  +[ [x] [y] [5] ]
  *[ [z] [z] ]
]

eval[ let*->nested lets[exp] [env] ]
```

## 376

```
let[ [<var>] [<bindings>] [<body>] ]

define[  fib[n]
  nlet[ 
    fib iter[
      [a]  [1]
      [b]  [0]
      [count]  [n]
    ]
    ?[
      =[ [count] [0] ]  [b]
      fib iter[
        +[ [a] [b] ]
        [a]
        -[ [count] [1] ]
      ]
    ]
  ]
]
```

## 377

```
define[  true?[x]
  not[eq?[ [x] [false] ]]
]

define[  false?[x]
  eq?[ [x] [false] ]
]

apply primitive procedure[ [<proc>] [<args>] ]

primitive procedure?[<proc>]

define[  make procedure[ [parameters] [body] [env] ]
  list[ ['procedure] [parameters] [body] [env] ]
]

define[  compound procedure?[p]
  tagged list?[ [p] ['procedure] ]
]

define[  procedure parameters[p]  cadr[p]  ]

define[  procedure body[p]  caddr[p]  ]

define[  procedure environment[p]  cadddr[p]  ]

lookup variable value[ [<var>] [<env>] ]
```

## 378

```
extend environment[ [<variables>] [<values>] [<base env>] ]

define variable![ [<var>] [<value>] [<env>] ]

set variable value![ [<var>] [<value>] [<env>] ]

define[  enclosing environment[env]  cdr[env]  ]

define[  first frame[env]  car[env]  ]

define[  [the empty environment]  [nil]  ]

define[  make frame[ [variables] [values] ]
  cons[ [variables] [values] ]
]

define[  frame variables[frame]  car[frame]  ]

define[  frame values[frame]  cdr[frame]  ]

define[  add binding to frame![ [var] [val] [frame] ]
  set car![ [frame] cons[[var]car[frame]] ]
  set cdr![ [frame] cons[[val]cdr[frame]] ]
]
```

## 379

```
define[  extend environment[ [vars] [vals] [base env] ]
  ?[
    =[ length[vars] length[vals] ]  cons[
      make frame[ [vars] [vals] ]
      [base env]
    ]
    ?[
      <[ length[vars] length[vals] ]  error[
        ['Too many arguments supplied]
        [vars]
        [vals]
      ]
      error[
        ['Too few arguments supplied]
        [vars]
        [vals]
      ]
    ]
  ]
]

define[  lookup variable value[ [var] [env] ]
  define[  env loop[env]
    define[  scan[ [vars] [vals] ]
      ?[
        null?[vars]  env loop[enclosing environment[env]]
        eq?[ [var] car[vars] ]  car[vals]
        scan[ cdr[vars] cdr[vals] ]
      ]
    ]
    ?[
      eq?[ [env] [the empty environment] ]  error[
        ['Unbound variable]
        [var]
      ]
      let[
        [frame]  first frame[env]
        scan[
          frame variables[frame]
          frame values[frame]
        ]
      ]
    ]
  ]
  env loop[env]
]

define[  set variable value![ [var] [val] [env] ]
  define[  env loop[env]
    define[  scan[ [vars] [vals] ]
      ?[
        null?[vars]  env loop[enclosing environment[env]]
        eq?[ [var] car[vars] ]  set car![ [vals] [val] ]
        scan[ cdr[vars] cdr[vals] ]
      ]
    ]
    ?[
      eq?[ [env] [the empty environment] ]  error[
        ['Unbound variable -- SET!]
        [var]
      ]
      let[
        [frame]  first frame[env]
        scan[
          frame variables[frame]
          frame values[frame]
        ]
      ]
    ]
  ]
  env loop[env]
]
```

## 380

```
define[  define variable![ [var] [val] [env] ]
  let[
    [frame]  first frame[env]
    [
      define[  scan[ [vars] [vals] ]
        ?[
          null?[vars]  add binding to frame![ [var] [val] [frame] ]
          eq?[ [var] car[vars] ]  set car![ [vals] [val] ]
          scan[ cdr[vars] cdr[vals] ]
        ]
      ]
      scan[
        frame variables[frame]
        frame values[frame]
      ]
    ]
  ]
]
```

## 381

```
define[  setup environment[]
  let[
    [initial env]  extend environment[
      primitive procedure names[]
      primitive procedure objects[]
      [the empty environment]
    ]
    [
      define variable![ ['true] [true] [initial env] ]
      define variable![ ['false] [false] [initial env] ]
      [initial env]
    ]
  ]
]

define[  [the global environments]  setup environment[]  ]
```

## 382

```
define[  primitive procedure?[proc]
  tagged list?[ [proc] ['primitive] ]
]

define[  primitive implementation[proc]  cadr[proc]  ]

define[  [primitive procedures]
  list[
    list[ ['car] [car] ]
    list[ ['cdr] [cdr] ]
    list[ ['cons] [cons] ]
    list[ ['null?] [null?] ]
    <more primitives>
  ]
]

define[  primitive procedure names[]
  map[
    [car]
    [primitive procedures]
  ]
]

define[  primitive procedure objects[]
  map[
    fun[  [proc]  list[ ['primitive] cadr[proc] ]  ]
    [primitive procedures]
  ]
]

define[  apply primitive procedure[ [proc] [args] ]
  apply in underlying scheme[
    primitive implementation[proc]
    [args]
  ]
]
```

## 383

```
define[  [input prompt]  [';;; M-Eval input:]  ]
define[  [output prompt]  [';;; M-Eval output:]  ]

define[  driver loop[]
  prompt for input[input prompt]
  let[
    [input]  read[]
    let[
      [output]  eval[ [input] [the global environment] ]
      [
        announce output[output prompt]
        user print[output]
      ]
    ]
  ]
  driver loop[]
]

define[  prompt for input[string]
  newline[]
  newline[]
  display[string]
  newline[]
]

define[  announce output[string]
  newline[]
  display[string]
  newline[]
]

define[  user print[object]
  ?[
    compound procedure?[object]  display[list[
      ['compound procedure]
      procedure parameters[object]
      procedure body[object]
      ['<procedure env>]
    ]]
    display[object]
  ]
]

define[  [the global environment]  setup environment[]  ]
```

## 384

```
driver loop[]

define[  append[ [x] [y] ]
  ?[
    null?[x]  [y]
    cons[
      car[x]
      append[ cdr[x] [y] ]
    ]
  ]
]

append[  list'[ [a] [b] [c] ]  list'[ [d] [e] [f] ]  ]

define[  factorial[n]
  ?[
    =[ [n] [1] ]  [1]
    *[
      factorial[-[ [n] [1] ]]
      [n]
    ]
  ]
]
```

## 387

```
eval[  list'[ [*] [5] [5] ]  [user initial environment]  ]

eval[  cons[ ['*] list'[[5][5]] ]  [user initial environment]  ]

define[  run forever[]  run forever[]  ]

define[  try[p]
  ?[
    halts?[ [p] [p] ]  run forever[]
    ['halted]
  ]
]

try[try]
```

## 388

```
define[  f[x]
  define[  even?[n]
    ?[
      =[ [n] [0] ]  [true]
      odd?[-[ [n] [1] ]]
    ]
  ]
  define[  odd?[n]
    ?[
      =[ [n] [0] ]  [false]
      even?[-[ [n] [1] ]]
    ]
  ]
  <rest of body of f>
]
```

## 389

```
fun[  [<vars>]
  define[  [u]  [<e1>]  ]
  define[  [v]  [<e2>]  ]
  [<e3>]
]

fun[  [<vars>]
  let[
    [u]  ['*unassigned*]
    [v]  ['*unassigned*]
    [
      set![ [u] [<e1>] ]
      set![ [v] [<e2>] ]
      [<e3>]
    ]
  ]
]
```

## 390

```
fun[  [<vars>]
  let[
    [u]  ['*unassigned*]
    [v]  ['*unassigned*]
    [
      let[
        [a]  [<e1>]
        [b]  [<e2>]
        set![ [u] [a] ]
        set![ [v] [b] ]
      ]
      [<e3>]
    ]
  ]
]
```

## 391

```
define[  solve[ [f] [y0] [dt] ]
  define[  [y]  integral[ delay[dy] [y0] [dt] ]  ]
  define[  [dy]  stream map[ [f] [y] ]  ]
  [y]
]

let[
  [a]  [1]
  [
    define[  f[x]
      define[  [b]  +[ [a] [x] ]  ]
      define[  [a]  [5]  ]
      +[ [a] [b] ]
    ]
    f[10]
  ]
]
```

## 392

```
define[  f[x]
  letrec[
    [even?]  fun[  [n]
      ?[
        =[ [n] [0] ]  [true]
        odd?[-[ [n] [1] ]]
      ]
    ]
    [odd?]  fun[  [n]
      ?[
        =[ [n] [0] ]  [false]
        even?[-[ [n] [1] ]]
      ]
    ]
    <rest of body of f>
  ]
]

letrec[
  [var_1]  [exp_1]
  [var_n]  [exp_n]
  <body>
]

letrec[
  [fact]  fun[  [n]
    ?[
      =[ [n] [1] ]  [1]
      *[  [n]  fact[-[ [n] [1] ]]  ]
    ]
  ]
  fact[10]
]
```

## 393

Shortening `fun` to `fn` from now on.

```
[
  fn[  [n]
    fn[  [fact]
      fact[ [fact] [n] ]
    ].[fn[  [ [ft] [k] ]
      ?[
        =[ [k] [1] ]  [1]
        *[  [k]  ft[ [ft] -[[k][1]] ]  ]
      ]
    ]]
  ].[10]
]

define[  f[x]
  define[  even?[n]
    ?[
      =[ [n] [0] ]  [true]
      odd?[-[ [n] [1] ]]
    ]
  ]
  define[  odd?[n]
    ?[
      =[ [n] [0] ]  [false]
      even?[-[ [n] [1] ]]
    ]
  ]
  even?[x]
]

define[  f[x]
  [
    fn[  [ [even?] [odd?] ]
      even?[ [even?] [odd?] [x] ]
    ].[
      fn[  [ [ev?] [od?] [n] ]
        ?[  =[ [n] [0] ]  [true]  od?[ [<??>] [<??>] [<??>] ]  ]
      ]
      fn[  [ [ev?] [od?] [n] ]
        ?[  =[ [n] [0] ]  [false]  ev?[ [<??>] [<??>] [<??>] ]  ]
      ]
    ]
  ]
]
```

## 394

```
define[  factorial[n]
  ?[
    =[ [n] [1] ]  [1]
    *[  factorial[-[ [n] [1] ]]  [n]  ]
  ]
]

define[  eval[ [exp] [env] ]
  analyze[exp].[env]
]
```

## 395

```
define[  analyze[exp]
  ?[
    self evaluating?[exp]  analyze self evaluating[exp]
    quoted?[exp]  analyze quoted[exp]
    variable?[exp]  analyze variable[exp]
    assignment?[exp]  analyze assignment[exp]
    definition?[exp]  analyze definition[exp]
    if?[exp]  analyze if[exp]
    lambda?[exp]  analyze lambda[exp]
    begin?[exp]  analyze sequence[begin actions[exp]]
    cond?[exp]  analyze[cond->if[exp]]
    application?[exp]  analyze application[exp]
    error[
      ['Unknown expression type -- ANALYZE]
      [exp]
    ]
  ]
]

define[  analyze self evaluating[exp]
  fun[  [env]  [exp]  ]
]

define[  analyze quoted[exp]
  let[
    [qval]  text of quotation[exp]
    lambda[  [env]  [qval]  ]
  ]
]

define[  analyze variable[exp]
  lambda[  [env]  lookup variable value[ [exp] [env] ]  ]
]
```

## 396

```
define[  analyze assignment[exp]
  let[
    [var]  assignment variable[exp]
    [vproc]  analyze[assignment value[exp]]
    fun[  [env]
      set variable value![ [var] vproc[env] [env] ]
      ['ok]
    ]
  ]
]

define[  analyze definition[exp]
  let[
    [var]  definition variable[exp]
    [vproc]  analyze[definition value[exp]]
    fun[  [env]
      define variable![ [var] vproc[env] [env] ]
      ['ok]
    ]
  ]
]

define[  analyze if[exp]
  let[
    [pproc]  analyze[if predicate[exp]]
    [cproc]  analyze[if consequent[exp]]
    [aproc]  analyze[if alternative[exp]]
    fun[  [env]
      ?[
        true?[pproc[env]]  cproc[env]
        aproc[env]
      ]
    ]
  ]
]

define[  analyze lambda[exp]
  let[
    [vars]  lambda parameters[exp]
    [bproc]  analyze sequence[lambda body[exp]]
    fun[  [env]  make procedure[ [vars] [bproc] [env] ]  ]
  ]
]
```

## 397

```
define[  analyze sequence[exps]
  define[  sequentially[ [proc1] [proc2] ]
    fun[  [env]  proc1[env]  proc2[env]  ]
  ]
  define[  loop[ [first proc] [rest procs] ]
    ?[
      null?[rest procs]  [first proc]
      loop[
        sequentially[ [first proc] car[rest procs] ]
        cdr[rest procs]
      ]
    ]
  ]
  let[
    [procs]  map[ [analyze] [exps] ]
    ?[
      null?[procs]  error[
        ['Empty sequence -- ANALYZE]
      ]
      loop[
        car[procs]
        cdr[procs]
      ]
    ]
  ]
]

define[  analyze application[exp]
  let[
    [fproc]  analyze[operator[exp]]
    [aprocs]  map[ [analyze] operands[exp] ]
    fun[  [env]
      execute application[
        fproc[env]
        map[
          fun[  [aproc]  aproc[env]  ]
          [aprocs]
        ]
      ]
    ]
  ]
]

define[  execute application[ [proc] [args] ]
  ?[
    primitive procedure?[proc]  apply primitive procedure[ [proc] [args] ]
    compound procedure?[proc]  [
      procedure body[proc].[
        extend environment[
          procedure parameters[proc]
          [args]
          procedure environment[proc]
        ]
      ]
    ]
    error[
      ['Unknown procedure type -- EXECUTE APPLICATION]
      [proc]
    ]
  ]
]
```

## 398

```
define[  analyze sequence[exps]
  define[  execute sequence[ [procs] [env] ]
    ?[
      null?[cdr[procs]]  [car[procs].[env]]
      [
        [car[procs].[env]]
        execute sequence[ cdr[procs] [env] ]
      ]
    ]
  ]
  let[
    [procs]  map[ [analyze] [exps] ]
    ?[
      null?[procs]  error['Empty sequence -- ANALYZE]
      fun[  [env]  execute sequence[ [procs] [env] ]  ]
    ]
  ]
]
```

## 399

```
define[  try[ [a] [b] ]
  ?[  =[ [a] [0] ]  [1]  [b]  ]
]

define[  unless[ [condition] [usual value] [exceptional value] ]
  ?[
    [condition]  [exceptional value]
    [usual value]
  ]
]
```

## 400

```
unless[
  =[ [b] [0] ]  /[ [a] [b] ]
  [
    display['exception: returning 0]
    [0]
  ]
]

define[  factorial[n]
  unless[
    =[ [n] [1] ]  *[ [n] factorial[-[[n][1]] ]  ]
    [1]
  ]
]
```

## 402

```
[
  application?[exp]  apply[
    actual value[ operator[exp] [env] ]
    operands[exp]
    [env]
  ]
]

define[  actual value[ [exp] [env] ]
  force it[eval[ [exp] [env] ]]
]
```

## 403

```
define[  apply[ [procedure] [arguments] [env] ]
  ?[
    primitive procedure?[procedure]  apply primitive procedure[
      [procedure]
      list of arg values[ [arguments] [env] ]   changed
    ]
    compound procedure?[procedure]  eval sequence[
      procedure body[procedure]
      extend environment[
        procedure parameters[procedure]
        list of delayed args[ [arguments] [env] ]   changed
        procedure environment[procedure]
      ]
    ]
    error[
      ['Unknown procedure type -- APPLY]
      [procedure]
    ]
  ]
]

define[  list of arg values[ [exps] [env] ]
  ?[
    no operands?[exps]  [nil]
    cons[
      actual value[ first operand[exps] [env] ]
      list of arg values[
        rest operands[exps]
        [env]
      ]
    ]
  ]
]

define[  list of delayed args[ [exps] [env] ]
  ?[
    no operands?[exps]  [nil]
    cons[
      delay it[ first operand[exps] [env] ]
      list of delayed args[
        rest operands[exps]
        [env]
      ]
    ]
  ]
]

define[  eval if[ [exp] [env] ]
  ?[
    true?[actual value[ if predicate[exp] [env] ]]  eval[
      if consequent[exp]
      [env]
    ]
    eval[
      if alternative[exp]
      [env]
    ]
  ]
]
```

## 404

```
define[  [input prompt]  [';;; L-Eval input:]  ]
define[  [output prompt]  [';;; L-Eval value:]  ]

define[  driver loop[]
  prompt for input[input prompt]
  let[
    [input]  read[]
    let[
      [output]  actual value[ [input] [the global environment] ]
      [
        announce output[output prompt]
        user print[output]
      ]
    ]
  ]
  driver loop[]
]

define[  [the global environment]  setup environment[]  ]

driver loop[]

define[  try[ [a] [b] ]
  ?[  =[ [a] [b] ]  [1]  [b]  ]
]

try[  [0]  /[ [1] [0] ]  ]
```

## 405

```
define[  force it[obj]
  ?[
    thunk?[obj]  actual value[ thunk exp[obj] thunk env[obj] ]
    [obj]
  ]
]

define[  delay it[ [exp] [env] ]
  list[ ['thunk] [exp] [env] ]
]

define[  thunk?[obj]
  tagged list?[ [obj] ['thunk] ]
]

define[  thunk exp[thunk]  cadr[thunk]  ]

define[  thunk env[thunk]  caddr[thunk]  ]

define[  evaluated thunk?[obj]
  tagged list?[ [obj] ['evaluated thunk] ]
]

define[  thunk value[evaluated thunk]  cadr[evaluated thunk]  ]
```

## 406

```
define[  force it[obj]
  ?[
    thunk?[obj]  let[
      [result]  actual value[
        thunk exp[obj]
        thunk env[obj]
      ]
      [
        set car![ [obj] ['evaluated thunk] ]
        set car![ cdr[obj] [result] ]   replace exp with its value
        set cdr![ cdr[obj] [nil] ]      forget unneeded env
        [result]
      ]
    ]
    evaluated thunk?[obj]  thunk value[obj]
    [obj]
  ]
]

define[  [count]  [0]  ]

define[  id[x]
  set![ [count] +[[count][1]] ]
  [x]
]

define[  [w]  id[ id[10] ]  ]

[count]

[w]

[count]
```

## 407

```
define[  square[x]  *[ [x] [x] ]  ]

square[ id[10] ]

[count]

define[  eval sequence[ [exps] [env] ]
  ?[
    last exp?[exps]  eval[ first exp[exps] [env] ]
    [
      actual value[ first exp[exps] [env] ]
      eval sequence[ rest exps[exps] [env] ]
    ]
  ]
]

define[  for each[ [proc] [items] ]
  ?[
    null?[items]  ['done]
    [
      proc[car[items]]
      for each[ [proc] cdr[items] ]
    ]
  ]
]
```

## 408

```
for each[
  fun[  [x]  newline[]  display[x]  ]
  list[ [57] [321] [88] ]
]

define[  p1[x]
  set![  [x]  cons[ [x] list[2] ]  ]
  [x]
]

define[  p2[x]
  define[  p[e]
    [e]
    [x]
  ]
  p[set![  [x]  cons[ [x] list[2] ]  ]]
]

define[  f[ [a] b[lazy] [c] d[lazy memo] ]
  ...
]
```

## 409

```
define[  cons[ [x] [y] ]
  fun[  [m]  m[ [x] [y] ]  ]
]

define[  car[z]
  z[fun[  [ [p] [q] ]  [p]  ]]
]

define[  cdr[z]
  z[fun[  [ [p] [q] ]  [q]  ]]
]
```

## 410

```
define[  list ref[ [items] [n] ]
  ?[
    =[ [n] [0] ]  car[items]
    list ref[ cdr[items] -[[n][1]] ]
  ]
]

define[  map[ [proc] [items] ]
  ?[
    null?[items]  [nil]
    cons[
      proc[car[items]]
      map[ [proc] cdr[items] ]
    ]
  ]
]

define[  scale list[ [items] [factor] ]
  map[
    fun[  [x]  *[ [x] [factor] ]  ]
    [items]
  ]
]

define[  add lists[ [list1] [list2] ]
  ?[
    null?[list1]  [list2]
    null?[list2]  [list1]
    cons[
      +[ car[list1] car[list2] ]
      add lists[
        cdr[list1]
        cdr[list2]
      ]
    ]
  ]
]

define[  [ones]  cons[ [1] [ones] ]  ]

define[  [integers]  cons[ [1] add lists[[ones][integers]] ]  ]

list ref[ [integers] [17] ]
```

## 411

```
define[  integral[ [integrand] [initial value] [dt] ]
  define[  [int]
    cons[
      [initial value]
      add lists[
        scale list[ [integrand] [dt] ]
        [int]
      ]
    ]
  ]
  [int]
]

define[  solve[ [f] [y0] [dt] ]
  define[  [y]  integral[ [dy] [y0] [dt] ]  ]
  define[  [dy]  map[ [f] [y] ]  ]
  [y]
]

list ref[  solve[ fun[[x][x]] [1] [0.001] ]  [1000]  ]

car[ list'[[a][b][c]] ]
```

## 412

```
define[  prime sum pair[ [list1] [list2] ]
  let[
    [a]  an element of[list1]
    [b]  an element of[list2]
    [
      require[prime?[ +[[a][b]] ]]
      list[[a][b]]
    ]
  ]
]
```

## 413

```
prime sum pair[  list'[ [1] [3] [5] [8] ]  list'[ [20] [35] [110] ]  ]
```

## 414

```
list[  amb[ [1] [2] [3] ]  amb[ ['a] ['b] ]  ]

list[[1]['a]]  list[[1]['b]]  list[[2]['a]]  list[[2]['b]]  list[[3]['a]]  list[[3]['b]]

define[  require[p]
  ?[  not[p]  amb[]  ]
]

define[  an element of[items]
  require[not[null?[items]]]
  amb[  car[items]  an element of[ cdr[items] ]  ]
]

define[  an integer starting from[n]
  amb[  [n]  an integer starting from[ +[[n][1]] ]  ]
]
```

## 417

```
prime sum pair[ list[[1][3][5][8]] list[[20][35][110]] ]

[try again]

prime sum pair[ list[[19][27][30]] list[[11][36][58]] ]

define[  a pythagorean triple between[ [low] [high] ]
  let[
    [i]  an integer between[ [low] [high] ]
    let[
      [j]  an integer between[ [i] [high] ]
      let[
        [k]  an integer between[ [j] [high] ]
        [
          require[=[  +[ *[[i][i]] *[[j][j]] ]  *[ [k] [k] ]  ]]
          list[ [i] [j] [k] ]
        ]
      ]
    ]
  ]
]
```

## 418

```
define[  a pythagorean triple between[ [low] [high] ]
  let[
    [i]  an integer between[ [low] [high] ]
    [hsq]  *[ [high] [high] ]
    let[
      [j]  an integer between[ [i] [high] ]
      let[
        [ksq]  +[ *[[i][i]] *[[j][j]] ]
        [
          require[>=[ [hsq] [ksq] ]]
          let[
            [k]  sqrt[ksq]
            [
              require[integer?[k]]
              list[[i][j][k]]
            ]
          ]
        ]
      ]
    ]
  ]
]

define[  distinct?[items]
  ?[
    null?[items]  [true]
    null?[cdr[items]]  [true]
    member[ car[items] cdr[items] ]  [false]
    distinct?[cdr[items]]
  ]
]
```

## 419

```
define[  multiple dwelling[]
  let[
    [baker]  amb[[1][2][3][4][5]]
    [cooper]  amb[[1][2][3][4][5]]
    [fletcher]  amb[[1][2][3][4][5]]
    [miller]  amb[[1][2][3][4][5]]
    [smith]  amb[[1][2][3][4][5]]
    [
      require[
        distinct?[list[ [baker] [cooper] [fletcher] [miller] [smith] ]]
      ]
      require[not[=[ [baker] [5] ]]]
      require[not[=[ [cooper] [1] ]]]
      require[not[=[ [fletcher] [5] ]]]
      require[not[=[ [fletcher] [1] ]]]
      require[>[ [miller] [cooper] ]]
      require[not[=[ abs[-[[smith][fletcher]]] [1] ]]]
      require[not[=[ abs[-[[fletcher][cooper]]] [1] ]]]
      list[
        list[ ['baker] [baker] ]
        list[ ['cooper] [cooper] ]
        list[ ['fletcher] [fletcher] ]
        list[ ['miller] [miller] ]
        list[ ['smith] [smith] ]
      ]
    ]
  ]
]

list[
  list[ ['baker] [3] ]
  list[ ['cooper] [2] ]
  list[ ['fletcher] [4] ]
  list[ ['miller] [5] ]
  list[ ['smith] [1] ]
]
```

## 421

```
define[  [nouns]  list[ ['noun] ['student] ['professor] ['cat] ['class] ]  ]

define[  [verbs]  list[ ['verb] ['studies] ['lectures] ['eats] ['sleeps] ]  ]

define[  [articles]  list[ ['article] ['the] ['a] ]  ]

sentence[
  noun phrase[ article[the] noun[cat] ]
  verb[eats]
]

define[  parse sentence[]
  list[
    ['sentence]
    parse noun phrase[]
    parse word[verbs]
  ]
]

define[  parse noun phrase[]
  list[
    ['noun phrase]
    parse word[articles]
    parse word[nouns]
  ]
]
```

## 422

```
define[  parse word[word list]
  require[not[null?[*unparsed*]]]
  require[memq[ car[*unparsed*] cdr[word list] ]]
  let[
    [found word]  car[*unparsed*]
    set![ [*unparsed*] cdr[*unparsed*] ]
    list[ car[word list] [found word] ]
  ]
]

define[  [*unparsed*]  [nil]  ]

define[  parse[input]
  set![ [*unparsed*] [input] ]
  let[
    [sent]  parse sentence[]
    [
      require[null?[*unparsed*]]
      [sent]
    ]
  ]
]

parse[list[ ['the] ['cat] ['eats] ]]

define[  [prepositions]  list[ ['prep] ['for] ['to] ['in] ['by] ['with] ]  ]
```

## 423

```
define[  parse prepositional phrase[]
  list[
    ['prep phrase]
    parse word[prepositions]
    parse noun phrase[]
  ]
]

define[  parse sentence[]
  list[
    ['sentence]
    parse noun phrase[]
    parse verb phrase[]
  ]
]

define[  parse verb phrase[]
  define[  maybe extend[verb phrase]
    amb[
      [verb phrase]
      maybe extend[
        list[
          ['verb phrase]
          [verb phrase]
          parse prepositional phrase[]
        ]
      ]
    ]
  ]
  maybe extend[parse word[verbs]]
]

define[  parse simple noun phrase[]
  list[
    ['simple noun phrase]
    parse word[articles]
    parse word[nouns]
  ]
]

define[  parse noun phrase[]
  define[  maybe extend[noun phrase]
    amb[
      [noun phrase]
      maybe extend[
        list[
          ['noun phrase]
          [noun phrase]
          parse prepositional phrase[]
        ]
      ]
    ]
  ]
  maybe extend[parse simple noun phrase[]]
]
```

## 424

```
parse[list'[[the][student][with][the][cat][sleeps][in][the][class]]]

sentence[
  noun phrase[
    simple noun phrase[ article[the] noun[student] ]
    prep phrase[
      prep[with]
      simple noun phrase[
        article[the]
        noun[cat]
      ]
    ]
  ]
  verb phrase[
    verb[sleeps]
    prep phrase[
      prep[in]
      simple noun phrase[
        article[the]
        noun[class]
      ]
    ]
  ]
]

parse[list'[[the][professor][lectures][to][the][student][with][the][cat]]]

sentence[
  simple noun phrase[ article[the] noun[professor] ]
  verb phrase[
    verb phrase[
      verb[lectures]
      prep phrase[
        prep[to]
        simple noun phrase[
          article[the]
          noun[student]
        ]
      ]
    ]
    prep phrase[
      prep[with]
      simple noun phrase[
        article[the]
        noun[cat]
      ]
    ]
  ]
]
```

## 425

```
sentence[
  simple noun phrase[ article[the] noun[professor] ]
  verb phrase[
    verb[lectures]
    prep phrase[
      prep[to]
      noun phrase[
        simple noun phrase[
          article[the]
          noun[student]
        ]
        prep phrase[
          prep[with]
          simple noun phrase[
            article[the]
            noun[cat]
          ]
        ]
      ]
    ]
  ]
]

define[  parse verb phrase[]
  amb[
    parse word[verbs]
    list[
      ['verb phrase]
      parse verb phrase[]
      parse prepositional phrase[]
    ]
  ]
]
```

## 428

```
define[  amb?[exp]  tagged list?[ [exp] ['amb] ]  ]

define[  amb choices[exp]  cdr[exp]  ]

[amb?[exp].[analyze amb[exp]]]
```

## 429

```
define[  ambeval[ [exp] [env] [succeed] [fail] ]
  analyze[exp].[ [env] [succeed] [fail] ]
]

fun[  [ [env] [succeed] [fail] ]
  ;;[succeed is fun[ [[value][fail]] ... ]]
  ;;[fail is fun[ [] ... ]]
  ...
]

ambeval[  [<exp>]
  [the global environment]
  fun[  [ [value] [fail] ]  [value]  ]
  fun[  []  ['failed]  ]
]
```

## 430

```
define[  analyze self-evaluating[exp]
  fun[  [ [env] [succeed] [fail] ]
    succeed[ [exp] [fail] ]
  ]
]

define[  analyze quoted[exp]
  let[
    [qval]  text of quotation[exp]
    fun[  [ [env] [succeed] [fail] ]
      succeed[ [qval] [fail] ]
    ]
  ]
]

define[  analyze variable[exp]
  fun[  [ [env] [succeed] [fail] ]
    succeed[
      lookup variable value[ [exp] [env] ]
      [fail]
    ]
  ]
]

define[  analyze lambda[exp]
  let[
    [vars]  lambda parameters[exp]
    [bproc]  analyze sequence[lambda body[exp]]
    fun[  [ [env] [succeed] [fail] ]
      succeed[
        make procedure[ [vars] [bproc] [env] ]
        [fail]
      ]
    ]
  ]
]

define[  analyze if[exp]
  let[
    [pproc]  analyze[if predicate[exp]]
    [cproc]  analyze[if consequent[exp]]
    [aproc]  analyze[if alternative[exp]]
    fun[  [ [env] [succeed] [fail] ]
      pproc[
        [env]

        success continuation for evaluating the predicate
        to obtain pred value
        fun[  [ [pred value] [fail2] ]
          ?[
            true?[pred value]  cproc[ [env] [succeed] [fail2] ]
            aproc[ [env] [succeed] [fail2] ]
          ]
        ]

        failure continuation for evaluating the predicate
        [fail]
      ]
    ]
  ]
]
```

## 431

```
define[  analyze sequence[exps]
  define[  sequentially[ [a] [b] ]
    fun[  [ [env] [succeed] [fail] ]
      a[
        [env]
        success continuation for calling a
        fun[  [ [a value] [fail2] ]
          b[ [env] [succeed] [fail2] ]
        ]
        failure continuation for calling a
        [fail]
      ]
    ]
  ]
  define[  loop[ [first proc] [rest procs] ]
    ?[
      null?[rest procs]  [first proc]
      loop[
        sequentially[ [first proc] car[rest procs] ]
        cdr[rest procs]
      ]
    ]
  ]
  let[
    [procs]  map[ [analyze] [exps] ]
    ?[
      null?[procs]  error['Empty sequence -- ANALYZE]
      loop[ car[procs] cdr[procs] ]
    ]
  ]
]

define[  analyze definition[exp]
  let[
    [var]  definition variable[exp]
    [vproc]  analyze[definition value[exp]]
    fun[  [ [env] [succeed] [fail] ]
      vproc[
        [env]
        fun[  [ [val] [fail2] ]
          define variable![ [var] [val] [env] ]
          succeed[ ['ok] [fail2] ]
        ]
        [fail]
      ]
    ]
  ]
]
```

## 432

```
define[  analyze assignment[exp]
  let[
    [var]  assignment variable[exp]
    [vproc]  analyze[assignment value[exp]]
    fun[  [ [env] [succeed] [fail] ]
      vproc[

        [env]

        fun[  [ [val] [fail2] ]                                   *1*
          let[
            [old value]  lookup variable value[ [var] [env] ]
            [
              set variable value![ [var] [val] [env] ]
              succeed[
                ['ok]
                fun[  []                                          *2*
                  set variable value![
                    [var]
                    [old value]
                    [env]
                  ]
                  fail2[]
                ]
              ]
            ]
          ]
        ]

        [fail]

      ]
    ]
  ]
]
```

## 433

```
define[  analyze application[exp]
  let[
    [fproc]  analyze[operator[exp]]
    [aprocs]  map[ [analyze] operands[exp] ]
    fun[  [ [env] [succeed] [fail] ]
      fproc[
        [env]
        fun[  [ [proc] [fail2] ]
          get args[
            [aprocs]
            [env]
            fun[  [ [args] [fail3] ]
              execute application[
                [proc] [args] [succeed] [fail3]
              ]
            ]
          ]
        ]
        [fail]
      ]
    ]
  ]
]

define[  get args[ [aprocs] [env] [succeed] [fail] ]
  ?[
    null?[aprocs]  succeed[ [nil] [fail] ]
    [car[aprocs].[
      [env]
      success continuation for this aproc
      fun[  [ [arg] [fail2] ]
        get args[
          cdr[aprocs]
          [env]
          success continuation for recursive call to get args
          fun[  [ [args] [fail3] ]
            succeed[
              cons[ [arg] [args] ]
              [fail3]
            ]
          ]
          [fail2]
        ]
      ]
      [fail]
    ]]
  ]
]
```

## 434

```
define[  execute application[ [proc] [args] [succeed] [fail] ]
  ?[
    primitive procedure?[proc]  succeed[
      apply primitive procedure[ [proc] [args] ]
      [fail]
    ]
    compound procedure?[proc]  [procedure body[proc].[
      extend environment[
        procedure parameters[proc]
        [args]
        procedure environment[proc]
      ]
      [succeed]
      [fail]
    ]]
    error[
      ['Unknown procedure type -- EXECUTE APPLICATION]
      [proc]
    ]
  ]
]

define[  analyze amb[exp]
  let[
    [cprocs]  map[ [analyze] amb choices[exp] ]
    fun[  [ [env] [succeed] [fail] ]
      define[  try next[choices]
        ?[
          null?[choices]  fail[]
          [car[choices].[
            [env]
            [succeed]
            fun[  []  try next[cdr[choices]]  ]
          ]]
        ]
      ]
      try next[cprocs]
    ]
  ]
]
```

## 435

```
define[  [input prompt]  [';;; Amb-Eval input:]  ]
define[  [output prompt]  [';;; Amb-Eval value:]  ]

define[  driver loop[]
  define[  internal loop[try again]
    prompt for input[input prompt]
    let[
      [input]  read[]
      ?[
        eq?[ [input] ['try again] ]  try again[]
        [
          newline[]
          display[';;; Starting a new problem ']
          ambeval[
            [input]
            [the global environment]
            embeval success
            fun[  [ [val] [next alternative] ]
              announce output[output prompt]
              user print[val]
              internal loop[next alternative]
            ]
            ambeval failure
            fun[  []
              announce output[';;; There are no more values of]
              user print[input]
              driver loop[]
            ]
          ]
        ]
      ]
    ]
  ]
  internal loop[fun[  []
    newline[]
    display[';;; There is no current problem]
    driver loop[]
  ]]
]
```

## 436

```
define[  [count]  [0]  ]

let[
  [x]  an element of[list'[[a][b][c]]]
  [y]  an element of[list'[[a][b][c]]]
  [
    permanent set![ [count] +[[count][1]] ]
    require[not[eq?[ [x] [y] ]]]
    list[ [x] [y] [count] ]
  ]
]

[try again]

if fail[
  let[
    [x]  an element of[list[[1][3][5]]]
    [
      require[even?[x]]
      [x]
    ]
  ]
  ['all odd]
]
```

## 437

```
if fail[
  let[
    [x]  an element of[list[ [1] [3] [5] [8] ]]
    [
      require[even?[x]]
      [x]
    ]
  ]
  ['all odd]
]

let[
  [pairs]  [nil]
  if fail[
    let[
      [p]  prime sum pair[ list[[1][3][5][8]] list[[20][35][110]] ]
      [
        permanent set![ [pairs] cons[[p][pairs]] ]
        amb[]
      ]
    ]
    [pairs]
  ]
]

define[  require?[exp]  tagged list?[ [exp] ['require] ]  ]

define[  require predicate[exp]  cadr[exp]  ]

[require?[exp].[analyze require[exp]]]

define[  analyze require[exp]
  let[
    [pproc]  analyze[require predicate[exp]]
    fun[  [ [env] [sicceed] [fail] ]
      pproc[
        [env]
        fun[  [ [pred value] [fail2] ]
          ?[
            [<??>]  [<??>]
            succeed[ ['ok] [fail2] ]
          ]
        ]
        [fail]
      ]
    ]
  ]
]
```

## 439

```
define[  append[ [x] [y] ]
  ?[
    null?[x]  [y]
    cons[
      car[x]
      append[ cdr[x] [y] ]
    ]
  ]
]
```

## 441

```
address[  Bitdiddle[Ben]  Slumerville[ Ridge[Road] [10] ]  ]
job[  Bitdiddle[Ben]  computer[wizard]  ]
salary[  Bitdiddle[Ben]  [60000]  ]
```

Or alternatively using list':

```
list'[  [address]  [ [Bitdiddle] [Ben] ]  [ [Slumerville] [[Ridge][Road]] [10] ]  ]
list'[  [job]  [ [Bitdiddle] [Ben] ]  [ [computer] [wizard] ]  ]
list'[  [salary]  [ [Bitdiddle] [Ben] ]  [60000]  ]
```

Update: in line with observation in [451](#451) this should actually be:

```
address[  [ [Bitdiddle] [Ben] ]  [ [Slumerville] [[Ridge][Road]] [10] ]  ]
job[      [ [Bitdiddle] [Ben] ]  [ [computer] [wizard] ]  ]
salary[   [ [Bitdiddle] [Ben] ]  [60000]  ]
```

## 442

```
list'[  [address]     [ [Hacker] [Alyssa] [P] ]  [ [Cambridge] [[Mass][Ave]] [78] ]  ]
list'[  [job]         [ [Hacker] [Alyssa] [P] ]  [ [computer] [programmer] ]  ]
list'[  [salary]      [ [Hacker] [Alyssa] [P] ]  [40000]  ]
list'[  [supervisor]  [ [Hacker] [Alyssa] [P] ]  [ [Bitdiddle] [Ben] ]  ]

list'[  [address]     [ [Fect] [Cy] [D] ]  [ [Cambridge] [[Ames][Street]] [3] ]  ]
list'[  [job]         [ [Fect] [Cy] [D] ]  [ [computer] [programmer] ]  ]
list'[  [salary]      [ [Fect] [Cy] [D] ]  [35000]  ]
list'[  [supervisor]  [ [Fect] [Cy] [D] ]  [ [Bitdiddle] [Ben] ]  ]

list'[  [address]     [ [Tweakit] [Lem] [E] ]  [ [Boston] [[Bay][State][Road]] [22] ]  ]
list'[  [job]         [ [Tweakit] [Lem] [E] ]  [ [computer] [technician] ]  ]
list'[  [salary]      [ [Tweakit] [Lem] [E] ]  [25000]  ]
list'[  [supervisor]  [ [Tweakit] [Lem] [E] ]  [ [Bitdiddle] [Ben] ]  ]

list'[  [address]     [ [Reasoner] [Louis] ]  [ [Slumerville] [[Pine][Tree][Road]] [80] ]  ]
list'[  [job]         [ [Reasoner] [Louis] ]  [ [computer] [programmer] [trainee] ]  ]
list'[  [salary]      [ [Reasoner] [Louis] ]  [30000]  ]
list'[  [supervisor]  [ [Reasoner] [Louis] ]  [ [Hacker] [Alyssa] [P] ]  ]

list'[  [supervisor]  [ [Bitdiddle] [Ben] ]  [ [Warbucks] [Oliver] ]  ]

list'[  [address]     [ [Warbucks] [Oliver] ]  [ [Swellesley] [[Top][Head][Road]] ]  ]
list'[  [job]         [ [Warbucks] [Oliver] ]  [ [administration] [big] [wheel] ]  ]
list'[  [salary]      [ [Warbucks] [Oliver] ]  [150000]  ]

list'[  [address]     [ [Scrooge] [Eben] ]  [ [Weston] [[Shady][Lane]] [10] ]  ]
list'[  [job]         [ [Scrooge] [Eben] ]  [ [accounting] [chief] [accountant] ]  ]
list'[  [salary]      [ [Scrooge] [Eben] ]  [75000]  ]
list'[  [supervisor]  [ [Scrooge] [Eben] ]  [ [Warbucks] [Oliver] ]  ]
```

Update: in line with observation in [451](#451) the above should actually be:

```
address[     [ [Hacker] [Alyssa] [P] ]  [ [Cambridge] [[Mass][Ave]] [78] ]  ]
job[         [ [Hacker] [Alyssa] [P] ]  [ [computer] [programmer] ]  ]
salary[      [ [Hacker] [Alyssa] [P] ]  [40000]  ]
supervisor[  [ [Hacker] [Alyssa] [P] ]  [ [Bitdiddle] [Ben] ]  ]

address[     [ [Fect] [Cy] [D] ]  [ [Cambridge] [[Ames][Street]] [3] ]  ]
job[         [ [Fect] [Cy] [D] ]  [ [computer] [programmer] ]  ]
salary[      [ [Fect] [Cy] [D] ]  [35000]  ]
supervisor[  [ [Fect] [Cy] [D] ]  [ [Bitdiddle] [Ben] ]  ]

address[     [ [Tweakit] [Lem] [E] ]  [ [Boston] [[Bay][State][Road]] [22] ]  ]
job[         [ [Tweakit] [Lem] [E] ]  [ [computer] [technician] ]  ]
salary[      [ [Tweakit] [Lem] [E] ]  [25000]  ]
supervisor[  [ [Tweakit] [Lem] [E] ]  [ [Bitdiddle] [Ben] ]  ]

address[     [ [Reasoner] [Louis] ]  [ [Slumerville] [[Pine][Tree][Road]] [80] ]  ]
job[         [ [Reasoner] [Louis] ]  [ [computer] [programmer] [trainee] ]  ]
salary[      [ [Reasoner] [Louis] ]  [30000]  ]
supervisor[  [ [Reasoner] [Louis] ]  [ [Hacker] [Alyssa] [P] ]  ]

supervisor[  [ [Bitdiddle] [Ben] ]  [ [Warbucks] [Oliver] ]  ]

address[     [ [Warbucks] [Oliver] ]  [ [Swellesley] [[Top][Head][Road]] ]  ]
job[         [ [Warbucks] [Oliver] ]  [ [administration] [big] [wheel] ]  ]
salary[      [ [Warbucks] [Oliver] ]  [150000]  ]

address[     [ [Scrooge] [Eben] ]  [ [Weston] [[Shady][Lane]] [10] ]  ]
job[         [ [Scrooge] [Eben] ]  [ [accounting] [chief] [accountant] ]  ]
salary[      [ [Scrooge] [Eben] ]  [75000]  ]
supervisor[  [ [Scrooge] [Eben] ]  [ [Warbucks] [Oliver] ]  ]
```

## 443

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
list'[  [address]     [ [Cratchet] [Robert] ]  [ [Allston] [[N][Harvard][Street]] [16] ]  ]
list'[  [job]         [ [Cratchet] [Robert] ]  [ [accounting] [scrivener] ]  ]
list'[  [salary]      [ [Cratchet] [Robert] ]  [18000]  ]
list'[  [supervisor]  [ [Cratchet] [Robert] ]  [ [Scrooge] [Eben] ]  ]

list'[  [address]     [ [Aull] [DeWitt] ]  [ [Slumerville] [[Onion][Square]] [5] ]  ]
list'[  [job]         [ [Aull] [DeWitt] ]  [ [administration] [secretary] ]  ]
list'[  [salary]      [ [Aull] [DeWitt] ]  [25000]  ]
list'[  [supervisor]  [ [Aull] [DeWitt] ]  [ [Warbucks] [Oliver] ]  ]

list'[  [can do job]  [ [computer] [wizard] ]  [ [computer] [programmer] ]  ]
list'[  [can do job]  [ [computer] [wizard] ]  [ [computer] [technician] ]  ]

list'[  [can do job]  [ [computer] [programmer] ]  [ [computer] [programmer] [trainee] ]  ]

list'[  [can do job]  [ [administration] [secretary] ]  [ [administration] [big] [wheel] ]  ]

list'[  [job]  [?x]  [ [computer] [programmer] ] ]

list'[  [job]  [ [Hacker] [Alyssa] [P] ]  [ [computer] [programmer] ]  ]
list'[  [job]  [ [Fect] [Cy] [D] ]  [ [computer] [programmer] ]  ]
```

## 444

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
list'[ [adress] [?x] [?y] ]

list'[ [supervisor] [?x] [?y] ]

list[ [job] [?x] computer[?type] ]

list'[  [job]  [ [Bitdiddle] [Ben] ]  [ [computer] [wizard] ]  ]
list'[  [job]  [ [Hacker] [Alyssa] [P] ]  [ [computer] [programmer] ]  ]
list'[  [job]  [ [Fect] [Cy] [D] ]  [ [computer] [programmer] ]  ]
list'[  [job]  [ [Tweakit] [Lem] [E] ]  [ [computer] [technician] ]  ]

list'[  [job]  [ [Reasoner] [Louis] ]  [ [computer] [programmer] [trainee] ]  ]
```

An alternative way of querying could be:

```
address[ [?x] [?y] ]

supervisor[ [?x] [?y] ]

job[ [?x] computer[?type] ]
```

## 445

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
list'[  [job]  [?x]  [ [computer] ...[?type] ]  ]

list'[ [computer] ...[?type] ]

list'[ [computer] [programmer] [trainee] ]

list'[ [computer] [programmer] ]

list'[ [computer] ]
```

## 446

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
and[
  list'[  [job]  [?person]  [ [computer] [programmer] ]  ]
  list'[  [address]  [?person]  [?where]  ]
]

and[
  list'[  [job]  [ [Hacker] [Alyssa] [P] ]  [ [computer] [programmer] ]  ]
  list'[  [address]  [ [Hacker] [Alyssa] [P] ]  [ [Cambridge] [[Mass][Ave]] ]  [78] ]
]

and[
  list'[  [job]  [ [Fect] [Cy] [D] ]  [ [computer] [programmer] ]  ]
  list'[  [address]  [ [Fect] [Cy] [D] ]  [ [Cambridge] [[Ames][Street]] ]  [3] ]
]

and[  [<query_1>]  [<query_2>]  [...]  [<query_n>]  ]

or[
  list'[  [supervisor]  [?x]  [ [Bitdiddle] [Ben] ]  ]
  list'[  [supervisor]  [?x]  [ [Hacker] [Alyssa] [P] ]  ]
]
```

## 447

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
or[
  list'[  [supervisor]  [ [Hacker] [Alyssa] [P] ]  [ [Bitdiddle] [Ben] ]  ]
  list'[  [supervisor]  [ [Hacker] [Alyssa] [P] ]  [ [Hacker] [Alyssa] [P] ]  ]
]

or[
  list'[  [supervisor]  [ [Fect] [Cy] [D] ]  [ [Bitdiddle] [Ben] ]  ]
  list'[  [supervisor]  [ [Fect] [Cy] [D] ]  [ [Hacker] [Alyssa] [P] ]  ]
]

or[
  list'[  [supervisor]  [ [Tweakit] [Lem] [E] ]  [ [Bitdiddle] [Ben] ]  ]
  list'[  [supervisor]  [ [Tweakit] [Lem] [E] ]  [ [Hacker] [Alyssa] [P] ]  ]
]

or[
  list'[  [supervisor]  [ [Reasoner] [Louis] ]  [ [Bitdiddle] [Ben] ]  ]
  list'[  [supervisor]  [ [Reasoner] [Louis] ]  [ [Hacker] [Alyssa] [P] ]  ]
]

or[  [<query_1>]  [<query_2>]  [...]  [<query_n>]  ]

and[
  list'[  [supervisor]  [?x]  [ [Bitdiddle] [Ben] ]  ]
  not[list'[ [job]  [?x]  [ [computer] [programmer] ]  ]]
]

not[<query_1>]

list value[ [<predicate>] [<arg_1>] [...] [<arg_n>] ]
```

## 448

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
and[
  list[ [salary] [?person] [?amount] ]
  list value[ [>] [?amount] [30000] ]
]

rule[  lives near[ [?person 1] [?person 2] ]
  and[
    list'[ [address] [?person 1] [[?town]...[?rest 1]] ]
    list'[ [address] [?person 2] [[?town]...[?rest 2]] ]
    not[same[ [?person 1] [?person 2] ]]
  ]
]

rule[  same[ [?x] [?x] ]  ]
```

## 449

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
rule[  wheel[?person]
  and[
    list'[ [supervisor] [?middle manager] [?person] ]
    list'[ [supervisor] [?x] [?middle manager] ]
  ]
]

rule[ [<conclusion>] [<body>] ]

lives near[ [?x] [[Bitdiddle][Ben]] ]

lives near[  [ [Reasoner] [Louis] ]  [ [Bitdiddle] [Ben] ]  ]
lives near[  [ [Aull] [DeWitt] ]  [ [Bitdiddle] [Ben] ]  ]

and[
  list'[ [job] [?x] [[computer][programmer]] ]
  lives near[ [?x] [[Bitdiddle][Ben]] ]
]

rule[  outranked by[ [?staff person] [?boss] ]
  or[
    list'[ [supervisor] [?staff person] [?boss] ]
    and[
      list'[ [supervisor] [?staff person] [?middle manager] ]
      outranked by[ [?middle manager] [?boss] ]
    ]
  ]
]
```

## 450

<!-- todo -->
Note: this should be updated line with observation in [451](#451).

```
list'[  [meeting]  [accounting]  [ [Monday] [9am] ]  ]
list'[  [meeting]  [administration]  [ [Monday] [10am] ]  ]
list'[  [meeting]  [computer]  [ [Wednesday] [3pm] ]  ]
list'[  [meeting]  [administration]  [ [Friday] [1pm] ]  ]

list'[  [meeting]  [whole company]  [ [Wednesday] [4pm] ]  ]

rule[  meeting time[ [?person] [?day and time] ]
  [<rule body>]
]
```

## 451

```
lives near[  [?person]  [ [Hacker] [Alyssa] [P] ]  ]

lives near[  [ [Hacker] [Alyssa] [P] ]  [ [Fect] [Cy] [D] ]  ]
lives near[  [ [Fect] [Cy] [D] ]  [ [Hacker] [Alyssa] [P] ]  ]

append to form[ [x] [y] [z] ]

rule[  append to form[ [nil] [?x] [?y] ]  ]

rule[  append to form[ [[?u]...[?v]] [?y] [[?u]...[?z]] ]
  append to form[ [?v] [?y] [?z] ]
]
```

Likely things like:

```
list'[  [meeting]  [administration]  [ [Friday] [1pm] ]  ]
```

and other lists should have had the form:

```
meeting[  [administration]  [ [Friday] [1pm] ]  ]
```

That would be more consistent with the language in the book.

As it stands, I have different syntax for rules defined by user (which are like functions) and data (which I considered to be plain lists).

Confusion comes from the fact that unquoted lists here are used both to call functions (rules) and to store data.

## 452

```
append to form[  [ [a] [b] ]  [ [c] [d] ]  [?z]  ]
->
append to form[  [ [a] [b] ]  [ [c] [d] ]  [ [a] [b] [c] [d] ]  ]

append to form[  [ [a] [b] ]  [?y]  [ [a] [b] [c] [d] ]  ]
->
append to form[  [ [a] [b] ]  [ [c] [d] ]  [ [a] [b] [c] [d] ]  ]

append to form[  [?x]  [?y]  [ [a] [b] [c] [d] ]  ]
->
append to form[  [nil]                [ [a] [b] [c] [d] ]  [ [a] [b] [c] [d] ]  ]
append to form[  [a]                  [ [b] [c] [d] ]      [ [a] [b] [c] [d] ]  ]
append to form[  [ [a] [b] ]          [ [c] [d] ]          [ [a] [b] [c] [d] ]  ]
append to form[  [ [a] [b] [c] ]      [d]                  [ [a] [b] [c] [d] ]  ]
append to form[  [ [a] [b] [c] [d] ]  [nil]                [ [a] [b] [c] [d] ]  ]

rule[  [ [?x] [next to] [?y] [in] [[?x][?y]...[?u]] ]  ]

rule[  [ [?x] [next to] [?y] [in] [[?v]...[?z]] ]
  [ [?x] [next to] [?y] [in] [?z] ]
]

list'[  [?x]  [next to]  [?y]  [in]  [ [1] [[2][3]] [4] ]  ]

list'[  [?x]  [next to]  [1]  [in]  [ [2] [1] [3] [1] ]  ]
```

Update: confusion continues.

On second thought, the following would be more correct in line with the observation from [451](#451):

```
rule[  ?x[ [next to] [?y] [in] [[?x][?y]...[?u]] ]  ]

rule[  ?x[ [next to] [?y] [in] [[?v]...[?z]] ]
  ?x[ [next to] [?y] [in] [?z] ]
]

?x[  [next to]  [?y]  [in]  [ [1] [[2][3]] [4] ]  ]

?x[  [next to]  [1]  [in]  [ [2] [1] [3] [1] ]  ]
```

So `?x` here is the operator.

The syntax of this logic language only behaves like Scheme in the outermost layer of queries. The compound "arguments" of the queries are not applications, as they would be in Scheme, but they are simple unevaluated lists.

## 453

```
son[ [Adam] [Cain] ]
son[ [Cain] [Enoch] ]
son[ [Enoch] [Irad] ]
son[ [Irad] [Mehujael] ]
son[ [Mehujael] [Methushael] ]
son[ [Metushael] [Lamech] ]
wife[ [Lamech] [Ada] ]
son[ [Ada] [Jabal] ]
son[ [Ada] [Jubal] ]
```

## 454

```
job[ [?x] [[computer][programmer]] ]
```

## 456

```
and[
  can do job[  [?x]  [ [computer] [programmer] [trainee] ]  ]
  job[ [?person] [?x] ]
]

can do job[  [?x]  [ [computer] [programmer] [trainee] ]  ]

job[ [?person] [?x] ]
```

## 457

```
not[job[ [?x] [[computer][programmer]] ]]
```

## 458

```
and[
  supervisor[ [?x] [?y] ]
  not[job[ [?x] [[computer][programmer]] ]]
]
```

## 459

```
[?x] = a[ [?y] [c] ]
[?x] = a[ [b] [?z] ]

a[ [?y] [c] ] = a[ [b] [?z] ]

[a] = [a], [?y] = [b], [c] = [?z]

[?x] = a[ [b] [c] ]
```

## 460

```
lives near[ [?x] [[Hacker][Alyssa][P]] ]

rule[
  lives near[ [?person 1] [?person 2] ]
  and[
    address[ [?person 1] [[?town]...[?rest 1]] ]
    address[ [?person 2] [[?town]...[?rest 2]] ]
    not[same[ [?person 1] [?person 2] ]]
  ]
]
```

## 462

```
assert![job[  [ [Bitdiddle] [Ben] ]  [ [computer] [wizard] ]  ]]

assert![rule[  wheel[?person]
  and[
    supervisor[ [?middle manager] [?person] ]
    supervisor[ [?x] [?middle manager] ]
  ]
]]
```

## 463

```
and[
  job[ [?x] [[computer][programmer]] ]
  supervisor[ [?x] [?y] ]
]

and[
  supervisor[ [?x] [?y] ]
  job[ [?x] [[computer][programmer]] ]
]
```

## 464

```
assert![married[ [Minnie] [Mickey] ]]

married[ [Mickey] [?who] ]

assert![rule[  married[ [?x] [?y] ]
  married[ [?y] [?x] ]
]]

married[ [Mickey] [?who] ]
```

## 465

```
and[
  supervisor[ [?x] [?y] ]
  not[job[ [?x] [[computer][programmer]] ]]
]

and[
  not[job[ [?x] [[computer][programmer]] ]]
  supervisor[ [?x] [?y] ]
]
```

## 466

```
rule[  outranked by[ [?staff person] [?boss] ]
  or[
    supervisor[ [?staff person] [?boss] ]
    and[
      outranked by[ [?middle manager] [?boss] ]
      supervisor[ [?staff person] [?middle manager] ]
    ]
  ]
]

outranked by[  [ [Bitdiddle] [Ben] ]  [?who]  ]
```

## 467

```
wheel[?who]

wheel[[ [Warbucks] [Oliver] ]]
wheel[[ [Bitdiddle] [Ben] ]]
wheel[[ [Warbucks] [Oliver] ]]
wheel[[ [Warbucks] [Oliver] ]]
wheel[[ [Warbucks] [Oliver] ]]

sum[
  [?amount]
  and[
    job[  [?x]  [ [computer] [programmer] ]  ]
    salary[  [?x]  [?amount]  ]
  ]
]

accumulation function[
  [<variable>]
  [<query pattern>]
]
```

## 468

```
define[  [input prompt]  [';;; Query input:]  ]
define[  [output prompt]  [';;; Query results:]  ]
```

## 469

```
define[  query driver loop[]
  prompt for input[input prompt]
  let[
    [q]  query syntax process[read[]]
    ?[
      assertion to be added?[q]  [
        add rule or assertion![
          add assertion body[q]
        ]
        newline[]
        display['Assertion added to data base.]
        query driver loop[]
      ]
      [
        newline[]
        display[output prompt]
        display stream[
          stream map[
            fun[  [frame]
              instantiate[
                [q]
                [frame]
                fun[  [ [v] [f] ]
                  contract question mark[v]
                ]
              ]
            ]
            qeval[  [q]  singleton stream[nil]  ]
          ]
        ]
        query driver loop[]
      ]
    ]
  ]
]
```

## 470

```
define[  instantiate[ [exp] [frame] [unbound var handler] ]
  define[  copy[exp]
    ?[
      var?[exp]  let[
        [binding]  binding in frame[ [exp] [frame] ]
        ?[
          [binding]  copy[binding value[binding]]
          unbound var handler[ [exp] [frame] ]
        ]
      ]
      pair?[exp]  cons[
        copy[car[exp]]
        copy[cdr[exp]]
      ]
      [exp]
    ]
  ]
  copy[exp]
]

define[  qeval[ [query] [frame stream] ]
  let[
    [qproc]  get[ type[query] ['qeval] ]
    ?[
      [qproc]  qproc[ contents[query] [frame stream] ]
      simple query[ [query] [frame stream] ]
    ]
  ]
]

define[  simple query[ [query pattern] [frame stream] ]
  stream flatmap[
    fun[  [frame]
      stream append delayed[
        find assertions[ [query pattern] [frame] ]
        delay[apply rules[ [query pattern] [frame] ]]
      ]
    ]
    [frame stream]
  ]
]
```

## 471

```
define[  conjoin[ [conjuncts] [frame stream] ]
  ?[
    empty conjunction?[conjuncts]  [frame stream]
    conjoin[
      rest conjuncts[conjuncts]
      qeval[
        first conjunct[conjuncts]
        [frame stream]
      ]
    ]
  ]
]

put[ ['and] ['qeval] [conjoin] ]

define[  disjoin[ [disjuncts] [frame stream] ]
  ?[
    empty disjunction?[disjuncts]  [the empty stream]
    interleave delayed[
      qeval[ first disjunct[disjuncts] [frame stream] ]
      delay[disjoin[
        rest disjuncts[disjuncts]
        [frame stream]
      ]]
    ]
  ]
]

put[ ['or] ['qeval] [disjoin] ]
```

## 472

```
define[  negate[ [operands] [frame stream] ]
  stream flatmap[
    fun[  [frame]
      ?[
        stream null?[qeval[
          negated query[operands]
          singleton stream[frame]
        ]]  singleton stream[frame]
        [the empty stream]
      ]
    ]
    [frame stream]
  ]
]

put[ ['not] ['qeval] [negate] ]

define[  lisp value[ [call] [frame stream] ]
  stream flatmap[
    fun[  [frame]
      ?[
        execute[instantiate[
          [call]
          [frame]
          fun[  [ [v] [f] ]
            error[ ['Unknown pat var -- LISP VALUE] [v] ]
          ]
        ]]  singleton stream[frame]
        [the empty stream]
      ]
    ]
    [frame stream]
  ]
]

put[ ['lisp value] ['qeval] [list value] ]
```

## 473

```
define[  execute[exp]
  apply[
    eval[ predicate[exp] [user initial environment] ]
    args[exp]
  ]
]

define[  always true[ [ignore] [frame stream] ]  [frame stream]  ]

put[ ['always true] ['qeval] [always true] ]

define[  find assertions[ [pattern] [frame] ]
  stream flatmap[
    fun[  [datum]
      check an assertion[ [datum] [pattern] [frame] ]
    ]
    fetch assertions[ [pattern] [frame] ]
  ]
]
```

## 474

```
define[  check an assertion[ [assertion] [query pat] [query frame] ]
  let[
    [match result]  pattern match[ [query pat] [assertion] [query frame] ]
    ?[
      eq?[ [match result] ['failed] ]  [the empty stream]
      singleton stream[match result]
    ]
  ]
]

define[  pattern match[ [pat] [dat] [frame] ]
  ?[
    eq?[ [frame] ['failed] ]  ['failed]
    equal?[ [pat] [dat] ]  [frame]
    var?[pat]  extend if consistent[ [pat] [dat] [frame] ]
    and[ pair?[pat] pair?[dat] ]  pattern match[
      cdr[pat]
      cdr[dat]
      pattern match[
        car[pat]
        car[dat]
        [frame]
      ]
    ]
    ['failed]
  ]
]

define[  extend if consistent[ [var] [dat] [frame] ]
  let[
    [binding]  binding in frame[ [var] [frame] ]
    ?[
      [binding]  pattern match[ binding value[binding] [dat] [frame] ]
      extend[ [var] [dat] [frame] ]
    ]
  ]
]
```

## 476

```
define[  apply rules[ [pattern] [frame] ]
  stream flatmap[
    fun[  [rule]
      apply a rule[ [rule] [pattern] [frame] ]
    ]
    fetch rules[ [pattern] [frame] ]
  ]
]

define[  apply a rule[ [rule] [query pattern] [query frame] ]
  let[
    [clean rule]  rename variables in[rule]
    let[
      [unify result]  unify match[
        [query pattern]
        conclusion[clean rule]
        [query frame]
      ]
      ?[
        eq?[ [unify result] ['failed] ]  [the empty stream]
        qeval[
          rule body[clean rule]
          singleton stream[unify result]
        ]
      ]
    ]
  ]
]
```

## 477

```
define[  rename variables in[rule]
  let[
    [rule application id]  new rule application id[]
    [
      define[  tree walk[exp]
        ?[
          var?[exp]  make new variable[ [exp] [rule application id] ]
          pair?[exp]  cons[
            tree walk[car[exp]]
            tree walk[cdr[exp]]
          ]
          [exp]
        ]
      ]
      tree walk[rule]
    ]
  ]
]

define[  unify match[ [p1] [p2] [frame] ]
  ?[
    eq?[ [frame] ['failed] ]  ['failed]
    equal?[ [p1] [p2] ]  [frame]
    var?[p1]  extend if possible[ [p1] [p2] [frame] ]
    var?[p2]  extend if possible[ [p2] [p1] [frame] ]      ***
    and[ pair?[p1] pair?[p2] ]  unify match[
      cdr[p1]
      cdr[p2]
      unify match[
        car[p1]
        car[p2]
        [frame]
      ]
    ]
    ['failed]
  ]
]
```

## 479

```
define[  extend if possible[ [var] [val] [frame] ]
  let[
    [binding]  binding in frame[ [var] [frame] ]
    ?[
      [binding]  unify match[
        binding value[binding] [val] [frame]
      ]
      var?[val]  let[                                      ***
        [binding]  binding in frame[ [val] [frame] ]
        ?[
          [binding]  unify match[
            [var] binding value[binding] [frame]
          ]
          extend[ [var] [val] [frame] ]
        ]
      ]
      depends on?[ [val] [var] [frame] ]  ['failed]        ***
      extend[ [var] [val] [frame] ]
    ]
  ]
]

define[  depends on?[ [exp] [var] [frame] ]
  define[  tree walk[e]
    ?[
      var?[e]  ?[
        equal?[ [var] [e] ]  [true]
        let[
          [b]  binding in frame[ [e] [frame] ]
          ?[
            [b]  tree walk[binding value[b]]
            [false]
          ]
        ]
      ]
      pair?[e]  or[
        tree walk[car[e]]
        tree walk[cdr[e]]
      ]
      [false]
    ]
  ]
  tree walk[exp]
]
```

## 480

```
define[  [THE ASSERTIONS]  [the empty stream]  ]

define[  fetch assertions[ [pattern] [frame] ]
  ?[
    use index?[pattern]  get indexed assertions[pattern]
    get all assertions[]
  ]
]

define[  get all assertions[]  [THE ASSERTIONS]  ]

define[  get indexed assertions[pattern]
  get stream[ index key of[pattern] ['assertion stream] ]
]

define[  get stream[ [key1] [key2] ]
  let[
    [s]  get[ [key1] [key2] ]
    ?[ [s] [s] [the empty stream] ]
  ]
]

define[  [THE RULES]  [the empty stream]  ]

define[  fetch rules[ [pattern] [frame] ]
  ?[
    use index?[pattern]  get indexed rules[pattern]
    get all rules[]
  ]
]

define[  get all rules[]  [THE RULES]  ]
```

## 481

```
define[  get indexed rules[pattern]
  stream append[
    get stream[ index key of[pattern] ['rule stream] ]
    get stream[ ['?] ['rule stream] ]
  ]
]

define[  add rule or assertion![assertion]
  ?[
    rule?[assertion]  add rule![assertion]
    add assertion![assertion]
  ]
]

define[  add assertion![assertion]
  store assertion in index[assertion]
  let[
    [old assertions]  [THE ASSERTIONS]
    [
      set![ [THE ASSERTIONS] cons stream[[assertion][old assertions]] ]
      ['ok]
    ]
  ]
]

define[  add rule![rule]
  store rule in index[rule]
  let[
    [old rules]  [THE RULES]
    [
      set![ [THE RULES] cons stream[[rule][old rules]] ]
      ['ok]
    ]
  ]
]

define[  store assertion in index[assertion]
  ?[
    indexable?[assertion]  let[
      [key]  index key of[assertion]
      let[
        [current assertion stream]  get stream[ [key] ['assertion stream] ]
        put[
          [key]
          ['assertion stream]
          cons stream[
            [assertion]
            [current assertion stream]
          ]
        ]
      ]
    ]
  ]
]

define[  store rule in index[rule]
  let[
    [pattern]  conclusion[rule]
    ?[
      indexable?[pattern]  let[
        [key]  index key of[pattern]
        let[
          [current rule stream]  get stream[ [key] ['rule stream] ]
          put[
            [key]
            ['rule stream]
            cons stream[
              [rule]
              [current rule stream]
            ]
          ]
        ]
      ]
    ]
  ]
]
```

## 482

```
define[  indexable?[pat]
  or[
    constant symbol?[car[pat]]
    var?[car[pat]]
  ]
]

define[  index key of[pat]
  let[
    [key]  car[pat]
    ?[  var?[key]  ['?]  [key]  ]
  ]
]

define[  use index?[pat]
  constant symbol?[car[pat]]
]

define[  add assertion![assertion]
  store assertion in index[assertion]
  set![
    [THE ASSERTIONS]
    cons stream[ [assertion] [THE ASSERTIONS] ]
  ]
  ['ok]
]

define[  stream append delayed[ [s1] [delayed s2] ]
  ?[
    stream null?[s1]  force[delayed s2]
    cons stream[
      stream car[s1]
      stream append delayed[
        stream cdr[s1]
        [delayed s2]
      ]
    ]
  ]
]
```

## 483

```
define[  interleave delayed[ [s1] [delayed s2] ]
  ?[
    stream null?[s1]  force[delayed s2]
    cons stream[
      stream car[s1]
      interleave delayed[
        force[delayed s2]
        delay[stream cdr[s1]]
      ]
    ]
  ]
]

define[  stream flatmap[ [proc] [s] ]
  flatten stream[stream map[ [proc] [s] ]]
]

define[  flatten stream[stream]
  ?[
    stream null?[stream]  [the empty stream]
    interleave delayed[
      stream car[stream]
      delay[flatten stream[stream cdr[stream]]]
    ]
  ]
]

define[  singleton stream[x]
  cons stream[ [x] [the empty stream] ]
]

define[  type[exp]
  ?[
    pair?[exp]  car[exp]
    error[ ['Unknown expression TYPE] [exp] ]
  ]
]

define[  contents[exp]
  ?[
    pair?[exp]  cdr[exp]
    error[ ['Unknown expression CONTENTS] [exp] ]
  ]
]
```

## 484

```
define[  assertion to be added?[exp]
  eq?[ type[exp] ['assert!] ]
]

define[  add assertion body[exp]
  car[contents[exp]]
]

define[  empty conjunction?[exps]  null?[exps]  ]
define[  first conjunct[exps]  car[exps]  ]
define[  rest conjuncts[exps]  cdr[exps]  ]

define[  empty disjunction?[exps]  null?[exps]  ]
define[  first disjunct[exps]  car[exps]  ]
define[  rest disjuncts[exps]  cdr[exps]  ]

define[  negated query[exps]  car[exps]  ]

define[  predicate[exps]  car[exps]  ]
define[  args[exps]  cdr[exps]  ]

define[  rule?[statement]
  tagged list?[ [statement] ['rule] ]
]

define[  conclusion[rule]  cadr[rule]  ]

define[  rule body[rule]
  ?[
    null?[cddr[rule]]  list'[always true]
    caddr[rule]
  ]
]
```

## 485

```
define[  query syntax process[exp]
  map over symbols[ [expand question mark] [exp] ]
]

define[  map over symbols[ [proc] [exp] ]
  ?[
    pair?[exp]  cons[
      map over symbols[ [proc] car[exp] ]
      map over symbols[ [proc] cdr[exp] ]
    ]
    symbol?[exp]  proc[exp]
    [exp]
  ]
]

define[  expand question mark[symbol]
  let[
    [chars]  symbol->string[symbol]
    ?[
      string=?[ substring[[chars][0][1]] ['?] ]  list[
        ['?]
        string->symbol[
          substring[  [chars]  [1]  string length[chars]  ]
        ]
      ]
      [symbol]
    ]
  ]
]

define[  var?[exp]
  tagged list?[ [exp] ['?] ]
]

define[  constant symbol?[exp]  symbol?[exp]  ]
```

## 486

```
define[  [rule counter]  [0]  ]

define[  new rule application id[]
  set![  [rule counter]  +[ [1] [rule counter] ]  ]
  [rule counter]
]

define[  make new variable[ [var] [rule application id] ]
  cons[  ['?]  cons[ [rule application id] cdr[var] ]  ]
]

define[  contract question mark[variable]
  string->symbol[
    string append[
      ['?]
      ?[
        number?[cadr[variable]]  string append[
          symbol->string[caddr[variable]]
          ['-]
          number->string[cadr[variable]]
        ]
        symbol->string[cadr[variable]]
      ]
    ]
  ]
]

define[  make binding[ [variable] [value] ]
  cons[ [variable] [value] ]
]

define[  binding variable[binding]
  car[binding]
]

define[  binding value[binding]
  cdr[binding]
]

define[  binding in frame[ [variable] [frame] ]
  assoc[ [variable] [frame] ]
]

define[  extend[ [variable] [value] [frame] ]
  cons[  make binding[ [variable] [value] ]  [frame] ]
]
```

Note: overall I think that the distiction between strings and symbols is not exactly necessary. Just having immutable strings, the way JavaScript has had for most of its lifetime is enough for most purposes. Most if not all of the code in SICP would work the same way if the language used immutable strings instead of symbols. This would also obviate the need for the `string->symbol` and `symbol->string` conversion functions used on this page. I've been actually translating the code with the tacit assumption that symbols = strings for some time now.

## 487

```
define[  simple query[ [query pattern] [frame stream] ]
  stream flatmap[
    fun[  [frame]
      stream append[
        find assertions[ [query pattern] [frame] ]
        apply rules[ [query pattern] [frame] ]
      ]
    ]
    [frame stream]
  ]
]

define[  disjoin[ [disjuncts] [frame stream] ]
  ?[
    empty disjunction?[disjuncts]  [the empty stream]
    interleave[
      qeval[ first disjunct[disjuncts] [frame stream] ]
      disjoin[ rest disjuncts[disjuncts] [frame stream] ]
    ]
  ]
]

define[  flatten stream[stream]
  ?[
    stream null?[stream]  [the empty stream]
    interleave[
      stream car[stream]
      flatten stream[stream cdr[stream]]
    ]
  ]
]

define[  simple stream flatmap[ [proc] [s] ]
  simple flatten[stream map[ [proc] [s] ]]
]

define[  simple flatten[stream]
  stream map[
    [??]
    stream filter[ [??] [stream] ]
  ]
]
```

## 488

```
unique[job[ [?x] [[computer][wizard]] ]]

unique[job[ [[Bitdiddle][Ben]] [[computer][wizard]] ]]

unique[job[ [?x] [[computer][programmer]] ]]

and[
  job[ [?x] [?j] ]
  unique[job[ [?anyone] [?j] ]]
]

put[ ['unique] ['qeval] [uniquely asserted] ]
```

## 489

```
define[  square[x]
  *[ [x] [x] ]
]

define[  sum of squares[ [x] [y] ]
  +[ square[x] square[y] ]
]

sum of squares[ [3] [4] ]
```

## 492

```
define[  gcd[ [a] [b] ]
  ?[
    =[ [b] [0] ]  [a]
    gcd[ [b] remainder[[a][b]] ]
  ]
]
```

## 494

```
define[  factorial[n]
  define[  iter[ [product] [counter] ]
    ?[
      >[ [counter] [n] ]  [product]
      iter[
        *[ [counter] [product] ]
        +[ [counter] [1] ]
      ]
    ]
  ]
  iter[ [1] [1] ]
]
```

## 497

```
data paths[
  registers[
    [
      name[a]
      buttons[ name[a<-b] source[register[b]] ]
    ]
    [
      name[b]
      buttons[ name[b<-t] source[register[t]] ]
    ]
    [
      name[t]
      buttons[ name[t<-r] source[operation[rem]] ]
    ]
  ]
]

operations[
  [
    name[rem]
    inputs[ register[a] register[b] ]
  ]
  [
    name[=]
    inputs[ register[b] constant[0] ]
  ]
]

controller[
[test b]                         label
  test[=]                        test
  branch[label[gcd done]]        conditional branch
  t<-r[]                         button push
  a<-b[]                         button push
  b<-t[]                         button push
  goto[label[test b]]            unconditional branch
[gcd done]                       label
]

controller[
[test b]
  test[ op[=] reg[b] const[0] ]
  branch[label[gcd done]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[test b]]
[gcd done]
]
```

## 499

```
perform[ op[print] reg[a] ]

define[  remainder[ [n] [d] ]
  ?[
    <[ [n] [d] ]  [n]
    remainder[  -[ [n] [d] ]  [d]  ]
  ]
]
```

## 500

```
controller[
[gcd loop]
  assign[ [a] op[read] ]
  assign[ [b] op[read] ]
[test b]
  test[ op[=] reg[b] const[0] ]
  branch[label[gcd done]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[test b]]
[gcd done]
  perform[ op[print] reg[a] ]
  goto[label[gcd loop]]
]

assign[ [t] op[rem] reg[a] reg[b] ]
```

## 502

```
controller[
[test b]
  test[ op[=] reg[b] const[0] ]
  branch[label[gcd done]]
  assign[ [t] reg[a] ]
[rem loop]
  test[ op[<] reg[t] reg[b] ]
  branch[label[rem done]]
  assign[ [t] op[-] reg[t] reg[b] ]
  goto[label[rem loop]]
[rem done]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[test b]]
[gcd done]
]

define[  sqrt[x]
  define[  good enough?[guess]
    <[  abs[-[ square[guess] [x] ]]  [0.001]  ]
  ]
  define[  improve[guess]
    average[  [guess]  /[ [x] [guess] ]  ]
  ]
  define[  sqrt iter[guess]
    ?[
      good enough?[guess]  [guess]
      sqrt iter[improve[guess]]
    ]
  ]
  sqrt iter[1.0]
]
```

## 503

```
[gcd 1]
  test[ op[=] reg[b] const[0] ]
  branch[label[after gcd 1]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[gcd 1]]
[after gcd 1]
  .
  .
  .
[gcd 2]
  test[ op[=] reg[d] const[0] ]
  branch[label[after gcd 2]]
  assign[ [s] op[rem] reg[c] reg[d] ]
  assign[ [c] reg[d] ]
  assign[ [d] reg[s] ]
  goto[label[gcd 2]]
[after gcd 2]
```

## 504

```
[gcd 1]
  test[ op[=] reg[b] const[0] ]
  branch[label[after gcd 1]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[gcd 1]]
[after gcd 1]
  .
  .
  .
[gcd 2]
  test[ op[=] reg[b] const[0] ]
  branch[label[after gcd 2]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[gcd 2]]
[after gcd 2]
```

## 505

```
[gcd]
  test[ op[=] reg[b] const[0] ]
  branch[label[gcd done]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[gcd]]
[gcd done]
  test[ op[=] reg[continue] const[0] ]
  branch[label[after gcd 1]]
  goto[label[after gcd 2]]
  .
  .
  .
Before branching to gcd from the first place where
it is needed, we place 0 in the continue register
  assign[ [continue] const[0] ]
  goto[label[gcd]]
[after gcd 1]
  .
  .
  .
Before the second use of gcd, we place 1 in the continue register
  assign[ [continue] const[1] ]
  goto[label[gcd]]
[after gcd 2]

[gcd]
  test[ op[=] reg[b] const[0] ]
  branch[label[gcd done]]
  assign[ [t] op[rem] reg[a] reg[b] ]
  assign[ [a] reg[b] ]
  assign[ [b] reg[t] ]
  goto[label[gcd]]
[gcd done]
  goto[reg[continue]]
  .
  .
  .
Before calling gcd, we assign to continue
the label to which gcd should return.
  assign[ [continue] label[after gcd 1] ]
  goto[label[gcd]]
[after gcd 1]
  .
  .
  .
Here is the second call to gcd, with a different continuation.
  assign[ [continue] label[after gcd 2] ]
  goto[label[gcd]]
[after gcd 2]
```

## 506

```
define[  factorial[n]
  ?[
    =[ [n] [1] ]  [1]
    *[
      factorial[-[ [n] [1] ]]
      [n]
    ]
  ]
]
```

## 507

```
define[  gcd[ [a] [b] ]
  ?[
    =[ [b] [0] ]  [a]
    gcd[ [b] remainder[[a][b]] ]
  ]
]
```

## 510

```
define[  fib[n]
  ?[
    <[ [n] [2] ]  [n]
    +[
      fib[-[ [n] [1] ]]
      fib[-[ [n] [2] ]]
    ]
  ]
]

define[  expt[ [b] [n] ]
  ?[
    =[ [n] [0] ]  [1]
    *[
      [b]
      expt[  [b]  -[ [n] [1] ]  ]
    ]
  ]
]

define[  expt[ [b] [n] ]
  define[  expt iter[ [counter] [product] ]
    ?[
      =[ [counter] [0] ]  [product]
      expt iter[
        -[ [counter] [1] ]
        *[ [b] [product] ]
      ]
    ]
  ]
  expt iter[ [n] [1] ]
]
```

## 511

```
controller[
  assign[ [continue] label[fact done] ]
[fact loop]
  test[ op[=] reg[n] const[1] ]
  branch[label[base case]]
  Set up for the recursive call by saving n and continue
  Set up continue so that the computation will continue
  at after fact when the subroutine returns.
  save[continue]
  save[n]
  assign[ [n] op[-] reg[n] const[1] ]
  assign[ [continue] label[after fact] ]
  goto[label[fact loop]]
[after fact]
  restore[n]
  restore[continue]
  assign[ [val] op[*] reg[n] reg[val] ]      val now contains n(n - 1)!
  goto[reg[continue]]                        return to caller
[base case]
  assign[ [val] const[1] ]                   base case: 1! = 1
  goto[reg[continue]]                        return to caller
[fact done]
]
```

## 512

```
controller[
  assign[ [continue] label[fib done] ]
[fib loop]
  test[ op[<] reg[n] const[2] ]
  branch[label[immediate answer]]
  set up to compute Fib(n - 1)
  save[continue]
  assign[ [continue] label[afterfib n-1] ]
  save[n]                                   save old value of n
  assign[ [n] op[-] reg[n] const[1] ]       clobber n to n - 1
  goto[label[fib loop]]                     perform recursive call
[afterfib n-1]                              upon return, val contains Fib(n - 1)
  restore[n]
  restore[continue]
  set up to compute Fib(n - 2)
  assign[ [n] op[-] reg[n] const[2] ]
  save[continue]
  assign[ [continue] label[afterfib n-2] ]
  save[val]                                 save Fib(n - 1)
  goto[label[fib loop]]
[afterfib n-2]                              upon return, val contains Fib(n - 2)
  assign[ [n] reg[val] ]                    n now contains Fib(n - 2)
  restore[val]                              val now contains Fib(n - 1)
  restore[continue]
  assign[ [val] op[+] reg[val] reg[n] ]     Fib(n - 1) + Fib(n - 2)
  goto[reg[continue]]                       return to caller, answer is in val
[immediate answer]
  assign[ [val] reg[n] ]                    base case: Fib(n) = n
  goto[reg[continue]]
[fib done]
]
```

## 513

```
assign[ [<register name>] reg[<register name>] ]

assign[ [<register name>] const[<constant value>] ]

assign[ [<register name>] op[<operation name>] [<input_1>] ... [<input_n>] ]

perform[ op[<operation name>] [<input_1>] ... [<input_n>] ]

test[ op[<operation name>] [<input_1>] ... [<input_n>] ]

branch[label[<label name>]]

goto[label[<label name>]]

assign[ [<register name>] label[<label name>] ]

goto[reg[<register name>]]

save[<register name>]

restore[<register name>]
```

General note: one thing differentiates assembly-like low-level languages from high-level languages like Lisp/Scheme is that syntax tree depth is limited and very low (flat) in the low-level languages while in high-level languages we deal with ~arbitrary trees.

## 514

```
make machine[ [<register names>] [<operations>] [<controller>] ]

set register contents![ [<machine model>] [<register name>] [<value>] ]

get register contents[ [<machine model>] [<register name>] ]

start[<machine model>]

define[  [gcd machine]
  make machine[
    list'[ [a] [b] [t] ]
    list[  list[ ['rem] [remainder] ]  list[ ['=] [=] ]  ]
    '[
    [test b]
      test[ op[=] reg[b] const[0] ]
      branch[label[gcd done]]
      assign[ [t] op[rem] reg[a] reg[b] ]
      assign[ [a] reg[b] ]
      assign[ [b] reg[t] ]
      goto[label[test b]]
    [gcd done]
    ]
  ]
]
```

## 515

```
set register contents![ [gcd machine] ['a] [206] ]

set register contents![ [gcd machine] ['b] [40] ]

start[gcd machine]

get register contents[ [gcd machine] ['a] ]
```

## 516

```
define[  make machine[ [register names] [ops] [controller text] ]
  let[
    [machine]  make new machine[]
    [
      for each[
        fun[  [register name]
          machine['allocate register].[register name]
        ]
        [register names]
      ]
      machine['install operations].[ops]
      machine['install instruction sequence].[assemble[ [controller text] [machine] ]]
      [machine]
    ]
  ]
]

define[  make register[name]
  let[
    [contents]  ['*unassigned*]
    [
      define[  dispatch[message]
        ?[
          eq?[ [message] ['get] ]  [contents]
          eq?[ [message] ['set] ]  fun[  [value]
            set![ [contents] [value] ]
          ]
          error[
            ['Unknown request -- REGISTER]
            [message]
          ]
        ]
      ]
      [dispatch]
    ]
  ]
]

define[  get contents[register]
  register['get]
]

define[  set contents![ [register] [value] ]
  register['set].[value]
]
```

## 517

```
define[  make stack[]
  let[
    [s]  [nil]
    [
      define[  push[x]
        set![  [s]  cons[ [x] [s] ]  ]
      ]
      define[  pop[]
        ?[
          null?[s]  error['Empty stack -- POP]
          let[
            [top]  car[s]
            [
              set![ [s] cdr[s] ]
              [top]
            ]
          ]
        ]
      ]
      define[  initialize[]
        set![ [s] [nil] ]
        ['done]
      ]
      define[  dispatch[message]
        ?[
          eq?[ [message] ['push] ]  [push]
          eq?[ [message] ['pop] ]  pop[]
          eq?[ [message] ['initialize] ]  initialize[]
          error[
            ['Unknown request -- STACK]
            [message]
          ]
        ]
      ]
      [dispatch]
    ]
  ]
]

define[  pop[stack]
  stack['pop]
]

define[  push[ [stack] [value] ]
  stack['push].[value]
]
```

## 518

```
define[  start[machine]
  machine['start]
]

define[  get register contents[ [machine] [register name] ]
  get contents[get register[ [machine] [register name] ]]
]

define[  set register contents![ [machine] [register name] [value] ]
  set contents![
    get register[ [machine] [register name] ]
    [value]
  ]
  ['done]
]

define[  get register[ [machine] [reg name] ]
  machine['get register].[reg name]
]
```

## 519

```
define[  make new machine[]
  let[
    [pc]  make register['pc]
    [flag]  make register['flag]
    [stack]  make stack[]
    [the instruction sequence]  [nil]
    let[
      [the ops]  list[
        list[  ['initialize stack]  fun[ [] stack['initialize] ]  ]
      ]
      [register table]  list[
        list[ ['pc] [pc] ]  list[ ['flag] [flag] ]
      ]
      [
        define[  allocate register[name]
          ?[
            assoc[ [name] [register table] ]  error[
              ['Multiply defined register: ']
              [name]
            ]
            set![
              [register table]
              cons[
                list[ [name] make register[name] ]
                [register table]
              ]
            ]
          ]
          ['register allocated]
        ]
        define[  lookup register[name]
          let[
            [val]  assoc[ [name] [register table] ]
            ?[
              [val]  cadr[val]
              error[ ['Unknown register: '] [name] ]
            ]
          ]
        ]
        define[  execute[]
          let[
            [insts]  get contents[pc]
            ?[
              null?[insts]  ['done]
              [
                instruction execution proc[car[insts]].[]
                execute[]
              ]
            ]
          ]
        ]
        define[  dispatch[message]
          ?[
            eq?[ [message] ['start] ]  [
              set contents![ [pc] [the instruction sequence] ]
              execute[]
            ]
            eq?[ [message] ['install instruction sequence] ]  fun[  [seq]
              set![ [the instruction sequence] [seq] ]
            ]
            eq?[ [message] ['allocate register] ]  [allocate register]
            eq?[ [message] ['get register] ]  [lookup register]
            eq?[ [message] ['install operations] ]  fun[  [ops]
              set![ [the ops] append[[the ops][ops]] ]
            ]
            eq?[ [message] ['stack] ]  [stack]
            eq?[ [message] ['operations] ]  [the ops]
            error[
              ['Unknown request -- MACHINE]
              [message]
            ]
          ]
        ]
        [dispatch]
      ]
    ]
  ]
]
```

## 520

```
define[  assemble[ [controller text] [machine] ]
  extract labels[
    [controller text]
    fun[  [ [insts] [labels] ]
      update insts![ [insts] [labels] [machine] ]
      [insts]
    ]
  ]
]
```

## 521

```
define[  extract labels[ [text] [receive] ]
  ?[
    null?[text]  receive[ [nil] [nil] ]
    extract labels[
      cdr[text]
      fun[  [ [insts] [labels] ]
        let[
          [next inst]  car[text]
          ?[
            symbol?[next inst]  receive[
              [insts]
              cons[
                make label entry[
                  [next inst]
                  [insts]
                ]
                [labels]
              ]
            ]
            receive[
              cons[
                make instruction[next inst]
                [insts]
              ]
              [labels]
            ]
          ]
        ]
      ]
    ]
  ]
]

define[  extract labels[ [text] ]
  ?[
    null?[text]  cons[ [nil] [nil] ]
    let[
      [result]  extract labels[cdr[text]]
      let[
        [insts]  car[result]
        [labels]  cdr[result]
        let[
          [next inst]  car[text]
          ?[
            symbol?[next inst]  cons[
              [insts]
              cons[
                make label entry[
                  [next inst]
                  [insts]
                ]
                [labels]
              ]
            ]
            cons[
              cons[
                make instruction[next inst]
                [insts]
              ]
              [labels]
            ]
          ]
        ]
      ]
    ]
  ]
]

define[  assemble[ [controller text] [machine] ]
  let[
    [result]  extract labels[controller text]
    let[
      [insts]  car[result]
      [labels]  cdr[result]
      [
        update insts![ [insts] [labels] [machine] ]
        [insts]
      ]
    ]
  ]
]
```

## 522

```
define[  update insts![ [insts] [labels] [machine] ]
  let[
    [pc]  get register[ [machine] ['pc] ]
    [flag]  get register[ [machine] ['flag] ]
    [stack]  machine['stack]
    [ops]  machine['operations]
    for each[
      fun[  [inst]
        set instruction execution proc![
          [inst]
          make execution procedure[
            instruction text[inst]
            [labels]
            [machine]
            [pc]
            [flag]
            [stack]
            [ops]
          ]
        ]
      ]
    ]
    [insts]
  ]
]

define[  make instruction[text]
  cons[ [text] [nil] ]
]

define[  instruction text[inst]
  car[inst]
]

define[  instruction execution proc[inst]
  cdr[inst]
]

define[  set instruction execution proc![ [inst] [proc] ]
  set cdr![ [inst] [proc] ]
]

define[  make label entry[ [label name] [insts] ]
  cons[ [label name] [insts] ]
]

define[  lookup label[ [labels] [label name] ]
  let[
    [val]  assoc[ [label name] [labels] ]
    ?[
      [val]  cdr[val]
      error[
        ['Undefined label -- ASSEMBLE]
        [label name]
      ]
    ]
  ]
]
```

## 523

```
[start]
  goto[label[here]]
[here]
  assign[ [a] const[3] ]
  goto[label[there]]
[here]
  assign[ [a] const[4] ]
  goto[label[there]]
[there]



define[
  make execution procedure[ [inst] [labels] [machine] [pc] [flag] [stack] [ops] ]
  ?[
    eq?[ car[inst] ['assign] ]  make assign[
      [inst] [machine] [labels] [ops] [pc]
    ]
    eq?[ car[inst] ['test] ]  make test[
      [inst] [machine] [labels] [ops] [flag] [pc]
    ]
    eq?[ car[inst] ['branch] ]  make branch[ [inst] [machine] [labels] [flag] [pc] ]
    eq?[ car[inst] ['goto] ]  make goto[ [inst] [machine] [labels] [pc] ]
    eq?[ car[inst] ['save] ]  make save[ [inst] [machine] [stack] [pc] ]
    eq?[ car[inst] ['restore] ]  make restore[ [inst] [machine] [stack] [pc] ]
    eq?[ car[inst] ['perform] ]  make perform[ [inst] [machine] [labels] [ops] [pc] ]
    error[ ['Unknown instruction type -- ASSEMBLE] [inst] ]
  ]
]
```

## 524

```
define[  make assign[ [inst] [machine] [labels] [operations] [pc] ]
  let[
    [target]  get register[ [machine] assign reg name[inst] ]
    [value exp]  assign value exp[inst]
    let[
      [value proc]  ?[
        operation exp?[value exp]  make operation exp[
          [value exp] [machine] [labels] [operations]
        ]
        make primitive exp[
          car[value exp] [machine] [labels]
        ]
      ]
      fun[  []                                    execution procedure for assign
        set contents![ [target] value proc[] ]
        advance pc[pc]
      ]
    ]
  ]
]

define[  assign reg name[assign instruction]
  cadr[assign instruction]
]

define[  assign value exp[assign instruction]
  cddr[assign instruction]
]
```

## 525

```
define[  advance pc[pc]
  set contents![ [pc] cdr[get contents[pc]] ]
]

define[  make test[ [inst] [machine] [labels] [operations] [flag] [pc] ]
  let[
    [condition]  test condition[inst]
    ?[
      operation exp?[condition]  let[
        [condition proc]  make operation exp[
          [condition] [machine] [labels] [operations]
        ]
        fun[  []
          set contents![ [flag] condition proc[] ]
          advance pc[pc]
        ]
      ]
      error[ ['Bad TEST instruction -- ASSEMBLE] [inst] ]
    ]
  ]
]

define[  test condition[test instruction]
  cdr[test instruction]
]
```

## 526

```
define[  make branch[ [inst] [machine] [labels] [flags] [pc] ]
  let[
    [dest]  branch dest[inst]
    ?[
      label exp?[dest]  let[
        [insts]  lookup label[ [labels] label exp label[dest] ]
        fun[  []
          ?[
            get contents[flag]  set contents![ [pc] [insts] ]
            advance pc[pc]
          ]
        ]
      ]
      error[ ['Bad BRANCH instruction -- ASSEMBLE] [inst] ]
    ]
  ]
]

define[  branch dest[branch instruction]
  cadr[branch instruction]
]

define[  make goto[ [inst] [machine] [labels] [pc] ]
  let[
    [dest]  goto dest[inst]
    ?[
      label exp?[dest]  let[
        [insts]  lookup label[
          [labels]
          label exp label[dest]
        ]
        fun[  []  set contents![ [pc] [insts] ]  ]
      ]
      register exp?[dest]  let[
        [reg]  get register[
          [machine]
          register exp reg[dest]
        ]
        fun[  []  set contents![ [pc] get contents[reg] ]  ]
      ]
      error[ ['Bad GOTO instruction -- ASSEMBLE] [inst] ]
    ]
  ]
]

define[  goto dest[goto instruction]
  cadr[goto instruction]
]

define[  make save[ [inst] [machine] [stack] [pc] ]
  let[
    [reg]  get register[
      [machine]
      stack inst reg name[inst]
    ]
    fun[  []
      push[ [stack] get contents[reg] ]
      advance pc[pc]
    ]
  ]
]
```

## 527

```
define[  make restore[ [inst] [machine] [stack] [pc] ]
  let[
    [reg]  get register[
      [machine]
      stack inst reg name[inst]
    ]
    fun[  []
      set contents![ [reg] pop[stack] ]
      advance pc[pc]
    ]
  ]
]

define[  stack inst reg name[stack instruction]
  cadr[stack instruction]
]

define[  make perform[ [inst] [machine] [labels] [operations] [pc] ]
  let[
    [action]  perform action[inst]
    ?[
      operation exp?[action]  let[
        [action proc]  make operation exp[
          [action] [machine] [labels] [operations]
        ]
        fun[  []
          action proc[]
          advance pc[pc]
        ]
      ]
      error[ ['Bad PERFORM instruction -- ASSEMBLE] [inst] ]
    ]
  ]
]

define[  perform action[inst]  cdr[inst]  ]

define[  make primitive exp[ [exp] [machine] [labels] ]
  ?[
    constant exp?[exp]  let[
      [c]  constant exp value[exp]
      lambda[  []  [c]  ]
    ]
    label exp?[exp]  let[
      [insts]  lookup label[
        [labels]
        label exp label[exp]
      ]
      fun[  []  [insts]  ]
    ]
    register exp?[exp]  let[
      [r]  get register[
        [machine]
        register exp reg[exp]
      ]
      fun[  []  get contents[r]  ]
    ]
    error[ ['Unknown expression type -- ASSEMBLE] [exp] ]
  ]
]
```

## 528

```
define[  register exp?[exp]  tagged list?[ [exp] ['reg] ]  ]

define[  register exp reg[exp]  cadr[exp]  ]

define[  constant exp?[exp]  tagged list?[ [exp] ['const] ]  ]

define[  constant exp value[exp]  cadr[exp]  ]

define[  label exp?[exp]  tagged list?[ [exp] ['label] ]  ]

define[  label exp label[exp]  cadr[exp]  ]

define[  make operation exp[ [exp] [machine] [labels] [operations] ]
  let[
    [op]  lookup prim[ operation exp op[exp] [operations] ]
    [aprocs]  map[
      fun[  [e]
        make primitive exp[ [e] [machine] [labels] ]
      ]
      operation exp operands[exp]
    ]
    fun[  []
      apply[
        [op]
        map[
          fun[  [p]  p[]  ]
          [aprocs]
        ]
      ]
    ]
  ]
]

define[  operation exp?[exp]
  and[  pair?[exp]  tagged list?[ car[exp] ['op] ]  ]
]

define[  operation exp op[operation exp]
  cadr[car[operation exp]]
]

define[  operation exp operands[operation exp]
  cdr[operation exp]
]
```

## 529

```
define[  lookup prim[ [symbol] [operations] ]
  let[
    [val]  assoc[ [symbol] [operations] ]
    ?[
      [val]  cadr[val]
      error[ ['Unknown operation -- ASSEMBLE] [symbol] ]
    ]
  ]
]

save[y]
save[x]
restore[y]

restore[y]

restore[y]

restore[y]
```

## 530

```
list[
  list[
    ['initialize stack]
    fun[  []  stack['initialize]  ]
  ]
  list[
    ['print stack statistics]
    fun[  []  stack['print statistics]  ]
  ]
]
```

## 531

```
define[  make stack[]
  let[
    [s]  [nil]
    [number pushes]  [0]
    [max depth]  [0]
    [current depth]  [0]
    [
      define[  push[x]
        set![  [s]  cons[ [x] [s] ]  ]
        set![  [number pushes]  +[ [1] [number pushes] ]  ]
        set![  [current depth]  +[ [1] [current depth] ]  ]
        set![  [max depth]  max[ [current depth] [max depth] ]  ]
      ]
      define[  pop[]
        ?[
          null?[s]  error['Empty stack -- POP]
          let[
            [top]  car[s]
            [
              set![ [s] cdr[s] ]
              set![ [current depth] -[[current depth][1]] ]
              [top]
            ]
          ]
        ]
      ]
      define[  initialize[]
        set![ [s] [nil] ]
        set![ [number pushes] [0] ]
        set![ [max depth] [0] ]
        set![ [current depth] [0] ]
        ['done]
      ]
      define[  print statistics[]
        newline[]
        display[
          list[ 
            ['total pushes] ['=] [number pushes]
            ['maximum depth] ['=] [max depth]
          ]
        ]
      ]
      define[  dispatch[message]
        ?[
          eq?[ [message] ['push] ]  [push]
          eq?[ [message] ['pop] ]  pop[]
          eq?[ [message] ['initialize] ]  initialize[]
          eq?[ [message] ['print statistics] ]  print statistics[]
          error[
            ['Unknown request -- STACK]
            [message]
          ]
        ]
      ]
      [dispatch]
    ]
  ]
]
```

## 533

```
set breakpoint[ [<machine>] [<label>] [<n>] ]

set breakpoint[ [gcd machine] ['test b] [4] ]

proceed machine[ [<machine>] ]

cancel breakpoint[ [<machine>] [<label>] [<n>] ]

cancel all breakpoints[<machine>]
```

## 534

```
vector ref[ [<vector>] [<n>] ]

vector set![ [<vector>] [<n>] [<value>] ]
```

## 537

```
assign[ [<reg_1>] op[car] reg[<reg_2>] ]

assign[ [<reg_1>] op[cdr] reg[<reg_2>] ]


assign[ [<reg_1>] op[vector ref] reg[the cars] reg[<reg_2>] ]

assign[ [<reg_1>] op[vector ref] reg[the cdrs] reg[<reg_2>] ]


perform[ op[set car!] reg[<reg_1>] reg[<reg_2>] ]

perform[ op[set cdr!] reg[<reg_1>] reg[<reg_2>] ]


perform[ op[vector set!] reg[the cars] reg[<reg_1>] reg[<reg_2>] ]

perform[ op[vector set!] reg[the cdrs] reg[<reg_1>] reg[<reg_2>] ]
```

## 538

```
assign[ [<reg_1>] op[cons] reg[<reg_2>] reg[<reg_3>] ]

perform[ op[vector set!] reg[the cars] reg[free] reg[<reg_2>] ]
perform[ op[vector set!] reg[the cdrs] reg[free] reg[<reg_3>] ]
assign[ [<reg_1>] reg[free] ]
assign[ [free] op[+] reg[free] const[1] ]

op[eq?] reg[<reg_1>] reg[<reg_2>]

assign[ [the stack] op[cons] reg[<reg>] reg[the stack] ]

assign[ [<reg>] op[car] reg[the stack] ]
assign[ [the stack] op[cdr] reg[the stack] ]
```

## 539

```
assign[ [the stack] const[nil] ]

define[ [x] cons[[1][2]] ]
define[ [y] list[[x][x]] ]

define[  count leaves[tree]
  ?[
    null?[tree]  [0]
    not[pair?[tree]]  [1]
    +[
      count leaves[car[tree]]
      count leaves[cdr[tree]]
    ]
  ]
]

define[  count leaves[tree]
  define[  count iter[ [tree] [n] ]
    ?[
      null?[tree]  [n]
      not[pair?[tree]]  +[ [n] [1] ]
      count iter[
        cdr[tree]
        count iter[ car[tree] [n] ]
      ]
    ]
  ]
  count iter[ [tree] [0] ]
]
```

## 540

```
accumulate[  [+]  [0]  filter[ [odd?] enumerate interval[[0][n]] ]  ]
```

## 544

```
[begin garbage collection]
  assign[ [free] const[0] ]
  assign[ [scan] const[0] ]
  assign[ [old] reg[root] ]
  assign[ [relocate continue] label[reassign root] ]
  goto[label[relocate old result in new]]
[reassign root]
  assign[ [root] reg[new] ]
  goto[label[gc loop]]

[gc loop]
  test[ op[=] reg[scan] reg[free] ]
  branch[label[gc flip]]
  assign[ [old] op[vector ref] reg[new cars] reg[scan] ]
  assign[ [relocate continue] label[update car] ]
  goto[label[relocate old result in new]]
```

## 545

```
[update car]
  perform[ op[vector set!] reg[new cars] reg[scan] reg[new] ]
  assign[ [old] op[vector ref] reg[new cdrs] reg[scan] ]
  assign[ [relocate continue] label[update cdr] ]
  goto[label[relocate old result in new]]

[update cdr]
  perform[ op[vector set!] reg[new cdrs] reg[scan] reg[new] ]
  assign[ [scan] op[+] reg[scan] const[1] ]
  goto[label[gc loop]]
```

## 546

```
[relocate old result in new]
  test[ op[pointer to pair?] reg[old] ]
  branch[label[pair]]
  assign[ [new] reg[old] ]
  goto[reg[relocate continue]]
[pair]
  assign[ [oldcr] op[vector ref] reg[the cars] reg[old] ]
  test[ op[broken heart?] reg[oldcr] ]
  branch[label[already moved]]
  assign[ [new] reg[free] ]                                new location for pair
  Update free pointer.
  assign[ [free] op[+] reg[free] const[1] ]
  Copy the car and cdr to new memory.
  perform[ op[vector set!] reg[new cars] reg[new] reg[oldcr] ]
  assign[ [oldcr] op[vector ref] reg[the cdrs] reg[old] ]
  perform[ op[vector set!] reg[new cdrs] reg[new] reg[oldcr] ]
  Construct the broken heart.
  perform[ op[vector set!] reg[the cars] reg[old] const[broken heart] ]
  perform[ op[vector set!] reg[the cdrs] reg[old] reg[new] ]
  goto[reg[relocate continue]]
[already moved]
  assign[ [new] op[vector ref] reg[the cdrs] reg[old] ]
  goto[reg[relocate continue]]

[gc flip]
  assign[ [temp] reg[the cdrs] ]
  assign[ [the cdrs] reg[new cdrs] ]
  assign[ [new cdrs] reg[temp] ]
  assign[ [temp] reg[the cars] ]
  assign[ [the cars] reg[new cars] ]
  assign[ [new cars] reg[temp] ]
```

## 549

```
[eval dispatch]
  test[ op[self evaluating?] reg[exp] ]
  branch[label[ev self eval]]
  test[ op[variable?] reg[exp] ]
  branch[label[ev variable]]
  test[ op[quoted?] reg[exp] ]
  branch[label[ev quoted]]
  test[ op[assignment?] reg[exp] ]
  branch[label[ev assignment]]
  test[ op[definition?] reg[exp] ]
  branch[label[ev definition]]
  test[ op[if?] reg[exp] ]
  branch[label[ev if]]
  test[ op[lambda?] reg[exp] ]
  branch[label[ev lambda]]
  test[ op[begin?] reg[exp] ]
  branch[label[ev begin]]
  test[ op[application?] reg[exp] ]
  branch[label[ev application]]
  goto[label[unknown expression type]]
```

## 550

```
[ev self eval]
  assign[ [val] reg[exp] ]
  goto[reg[continue]]
[ev variable]
  assign[ [val] op[lookup variable value] reg[exp] reg[env] ]
  goto[reg[continue]]
[ev quoted]
  assign[ [val] op[text of quotation] reg[exp] ]
  goto[reg[continue]]
[ev lambda]
  assign[ [unev] op[lambda parameters] reg[exp] ]
  assign[ [exp] op[lambda body] reg[exp] ]
  assign[ [val] op[make procedure] reg[unev] reg[exp] reg[env] ]
  goto[reg[continue]]
```

## 551

```
[ev application]
  save[continue]
  save[env]
  assign[ [unev] op[operands] reg[exp] ]
  save[unev]
  assign[ [exp] op[operator] reg[exp] ]
  assign[ [continue] label[ev appl did operator] ]
  goto[label[eval dispatch]]

[ev appl did operator]
  restore[unev]                          the operands
  restore[env]
  assign[ [argl] op[empty arglist] ]
  assign[ [proc] reg[val] ]              the operator
  test[ op[no operands?] reg[unev] ]
  branch[label[apply dispatch]]
  save[proc]

define[  empty arglist[]  [nil]  ]

define[  adjoin arg[ [arg] [arglist] ]
  append[ [arglist] list[arg] ]
]

define[  last operand?[ops]
  null?[cdr[ops]]
]
```

## 552

```
[ev appl operand loop]
  save[argl]
  assign[ [exp] op[first operand] reg[unev] ]
  test[ op[last operand?] reg[unev] ]
  branch[label[ev appl last arg]]
  save[env]
  save[unev]
  assign[ [continue] label[ev apply accumulate arg] ]
  goto[label[eval dispatch]]

[ev appl accumulate arg]
  restore[unev]
  restore[env]
  restore[argl]
  assign[ [argl] op[adjoin arg] reg[val] reg[argl] ]
  assign[ [unev] op[rest operands] reg[unev] ]
  goto[label[ev appl operand loop]]
```

## 553

```
[ev appl last arg]
  assign[ [continue] label[ev appl accum last arg] ]
  goto[label[eval dispatch]]
[ev appl accum last arg]
  restore[argl]
  assign[ [argl] op[adjoin arg] reg[val] reg[argl] ]
  restore[proc]
  goto[label[apply dispatch]]

[apply dispatch]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive apply]]
  test[ op[compound procedure?] reg[proc] ]
  branch[label[compound apply]]
  goto[label[unknown procedure type]]
```

## 554

```
[primitive apply]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]
  restore[continue]
  goto[reg[continue]]

[compound apply]
  assign[ [unev] op[procedure parameters] reg[proc] ]
  assign[ [env] op[procedure environment] reg[proc] ]
  assign[ [env] op[extend environment] reg[unev] reg[argl] reg[env] ]
  assign[ [unev] op[procedure body] reg[proc] ]
  goto[label[ev sequence]]
```

## 555

```
[ev begin]
  assign[ [unev] op[begin actions] reg[exp] ]
  save[continue]
  goto[label[ev sequence]]
```

## 556

```
[ev sequence]
  assign[ [exp] op[first exp] reg[unev] ]
  test[ op[last exp?] reg[unev] ]
  branch[label[ev sequence last exp]]
  save[unev]
  save[env]
  assign[ [continue] label[ev sequence continue] ]
  goto[label[eval dispatch]]
[ev sequence continue]
  restore[env]
  restore[unev]
  assign[ [unev] op[rest exps] reg[unev] ]
  goto[label[ev sequence]]
[ev sequence last exp]
  restore[continue]
  goto[label[eval dispatch]]

define[  sqrt iter[ [guess] [x] ]
  ?[
    good enough?[ [guess] [x] ]  [guess]
    sqrt iter[ improve[[guess][x]] [x] ]
  ]
]
```

## 557

```
[ev sequence]
  test[ op[no more exps?] reg[unev] ]
  branch[label[ev sequence end]]
  assign[ [exp] op[first exp] reg[unev] ]
  save[unev]
  save[env]
  assign[ [continue] label[ev sequence continue] ]
  goto[label[eval dispatch]]
[ev sequence continue]
  restore[env]
  restore[unev]
  assign[ [unev] op[rest exps] reg[unev] ]
  goto[label[ev sequence]]
[ev sequence end]
  restore[continue]
  goto[reg[continue]]

define[  no more exps?[seq] null?[seq] ]
```

## 558

```
define[  count[n]
  newline[]
  display[n]
  count[+[ [n] [1] ]]
]

[ev if]
  save[exp]                                  save expression for later
  save[env]
  save[continue]
  assign[ [continue] label[ev if decide] ]
  assign[ [exp] op[if predicate] reg[exp] ]
  goto[label[eval dispatch]]                 evaluate the predicate

[ev if decide]
  restore[continue]
  restore[env]
  restore[exp]
  test[ op[true?] reg[val] ]
  branch[label[ev if consequent]]
```

## 559

```
[ev if alternative]
  assign[ [exp] op[if alternative] reg[exp] ]
  goto[label[eval dispatch]]
[ev if consequent]
  assign[ [exp] op[if consequent] reg[exp] ]
  goto[label[eval dispatch]]

[ev assignment]
  assign[ [unev] op[assignment variable] reg[exp] ]
  save[unev]                                       save variable for later
  assign[ [exp] op[assignment value] reg[exp] ]
  save[env]
  save[continue]
  assign[ [continue] label[ev assignment 1] ]
  goto[label[eval dispatch]]                       evaluate the assignment value
[ev assignment 1]
  restore[continue]
  restore[env]
  restore[unev]
  perform[ op[set variable value!] reg[unev] reg[val] reg[env] ]
  assign[ [val] const[ok] ]
  goto[reg[continue]]

[ev definition]
  assign[ [unev] op[definition variable] reg[exp] ]
  save[unev]                                       save variable for later
  assign[ [exp] op[definition value] reg[exp] ]
  save[env]
  save[continue]
  assign[ [continue] label[ev definition 1] ]
  goto[label[eval dispatch]]                       evaluate the definition value
[ev definition 1]
  restore[continue]
  restore[env]
  restore[unev]
  perform[ op[define variable!] reg[unev] reg[val] reg[env] ]
  assign[ [val] const[ok] ]
  goto[reg[continue]]
```

## 561

```
[read eval print loop]
  perform[op[initialize stack]]
  perform[ op[prompt for input] const[';;; EC-Eval input:] ]
  assign[ [exp] op[read] ]
  assign[ [env] op[get global environment] ]
  assign[ [continue] label[print result] ]
  goto[label[eval dispatch]]
[print result]
  perform[ op[announce output] const[';;; EC-Eval value:] ]
  perform[ op[user print] reg[val] ]
  goto[label[read eval print loop]]


[unknown expression type]
  assign[ [val] const[unknown expression type error] ]
  goto[label[signal error]]

[unknown procedure type]
  restore[continue]                   clean up stack (from apply dispatch)
  assign[ [val] const[unknown procedure type error] ]
  goto[label[signal error]]

[signal error]
  perform[ op[user print] reg[val] ]
  goto[label[read eval print loop] ]


define[  [the global environment]  setup environment[]  ]

define[  get global environment[]  [the global environment]  ]
```

## 562

```
define[  [eceval]
  make machine[
    list'[ [exp] [env] [val] [proc] [argl] [continue] [unev] ]
    [eceval operations]
    list'[
      [read eval print loop]
        <entire machine controller as given above>
    ]
  ]
]

define[  [eceval operations]
  list[
    list[ ['self evaluating?] [self evaluating] ]
    <complete list of operations for eceval machine>
  ]
]

define[  [the global environment]  setup environment[]  ]

start[eceval]

define[  append[ [x] [y] ]
  ?[
    null?[x]  [y]
    cons[
      car[x]
      append[ cdr[x] [y] ]
    ]
  ]
]

append[ list'[[a][b][c]] list'[[d][e][f]] ]
```

## 563

```
[print result]
  perform[op[print stack statistics]]        added instruction
  perform[ op[announce output] const[';;; EC-Eval value:] ]
  ...  same as before

define[  factorial[n]
  ?[
    =[ [n] [1] ]  [1]
    *[  factorial[-[ [n] [1] ]]  [n]  ]
  ]
]

factorial[5]
```

## 564

```
define[  factorial[n]
  define[  iter[ [product] [counter] ]
    ?[
      >[ [counter] [n] ]  [product]
      iter[
        *[ [counter] [product] ]
        +[ [counter] [1] ]
      ]
    ]
  ]
  iter[ [1] [1] ]
]

define[  factorial[n]
  ?[
    =[ [n] [1] ]  [1]
    *[  factorial[-[ [n] [1] ]]  [n]  ]
  ]
]
```

## 565

```
define[  fib[n]
  ?[
    <[ [n] [2] ]  [n]
    +[  fib[-[ [n] [1] ]]  fib[-[ [n] [2] ]]  ]
  ]
]
```

## 569

```
assign[ [proc] op[lookup variable value] const[f] reg[env] ]
```

## 570

```
define[  compile[ [exp] [target] [linkage] ]
  ?[
    self evaluating?[exp]  compile self evaluating[ [exp] [target] [linkage] ]
    quoted?[exp]  compile quoted[ [exp] [target] [linkage] ]
    variable?[exp]  compile variable[ [exp] [target] [linkage] ]
    assignment?[exp]  compile assignment[ [exp] [target] [linkage] ]
    definition?[exp]  compile definition[ [exp] [target] [linkage] ]
    if?[exp]  compile if[ [exp] [target] [linkage] ]
    lambda?[exp]  compile lambda[ [exp] [target] [linkage] ]
    begin?[exp]  compile sequence[
      begin actions[exp]
      [target]
      [linkage]
    ]
    cond?[exp]  compile[ cond->if[exp] [target] [linkage] ]
    application?[exp]  compile application[ [exp] [target] [linkage] ]
    error[ ['Unknown expression type -- COMPILE] [exp] ]
  ]
]
```

## 571

```
assign[ [val] const[5] ]

assign[ [val] const[5] ]
goto[reg[continue]]
```

## 572

```
append instruction sequences[ [<seq_1>] [<seq_2>] ]

<seq_1>
<seq_2>

preserving[  list[ [<reg_1>] [<reg_2>] ]  [<seq_1>]  [<seq_2>]  ]

<seq_1>
<seq_2>

save[<reg_1>]
<seq_1>
restore[<reg_1>]
<seq_2>

save[<reg_2>]
<seq_1>
restore[<reg_2>]
<seq_2>

save[<reg_2>]
save[<reg_1>]
<seq_1>
restore[<reg_1>]
restore[<reg_2>]
<seq_2>
```

## 573

```
define[  make instruction sequence[ [needs] [modifies] [statements] ]
  list[ [needs] [modifies] [statements] ]
]

make instruction sequence[
  list'[ [env] [continue] ]
  list'[val]
  '[
    assign[ [val] op[lookup variable value] const[x] reg[env] ]
    goto[reg[continue]]
  ]
]
```

## 574

```
define[  empty instruction sequence[]
  make instruction sequence[ [nil] [nil] [nil] ]
]

f[ ['x] ['y] ]

[f[].[ ['x] ['y] ]]

f[ g['x] [y] ]

f[ g['x] ['y] ]
```

## 575

```
define[  compile linkage[linkage]
  ?[
    eq?[ [linkage] ['return] ]  make instruction[
      list'[continue] 
      [nil]
      '[goto[reg[continue]]]
    ]
    eq?[ [linkage] ['next] ]  empty instruction sequence[]
    make instruction sequence[
      [nil]
      [nil]
      '[goto[label[$[linkage]]]]
    ]
  ]
]

define[  end with linkage[ [linkage] [instruction sequence] ]
  preserving[
    list'[continue]
    [instruction sequence]
    compile linkage[linkage]
  ]
]

define[  compile self evaluating[ [exp] [target] [linkage] ]
  end with linkage[
    [linkage]
    make instruction sequence[
      [nil]
      list[target]
      '[
        assign[ $[target] const[$[exp]] ]
      ]
    ]
  ]
]
```

Using `$[xyz]` as backquote `,xyz`. Just riffing here.

## 576

```
define[  compile quoted[ [exp] [target] [linkage] ]
  end with linkage[
    [linkage]
    make instruction sequence[
      [nil]
      list[target]
      '[
        assign[ $[target] const[$[text of quotation[exp]]] ]
      ]
    ]
  ]
]

define[  compile variable[ [exp] [target] [linkage] ]
  end with linkage[
    [linkage]
    make instruction sequence[
      list'[env]
      list[target]
      '[
        assign[
          $[target]
          op[lookup variable value]
          const[$[exp]]
          reg[env]
        ]
      ]
    ]
  ]
]

define[  compile assignment[ [exp] [target] [linkage] ]
  let[
    [var]  assignment variable[exp]
    [get value code]  compile[
      compile[ assignment value[exp] ['val] ['next] ]
    ]
    end with linkage[
      [linkage]
      preserving[
        list'[env]
        [get value code]
        make instruction sequence[
          list'[ [env] [val] ]
          list[target]
          '[
            perform[
              op[set variable value!]
              const[$[var]]
              reg[val]
              reg[env]
            ]
            assign[ $[target] const[ok] ]
          ]
        ]
      ]
    ]
  ]
]
```

## 577

```
define[  compile definition[ [exp] [target] [linkage] ]
  let[
    [var]  definition variable[exp]
    [get value code]  compile[ definition value[exp] ['val] ['next] ]
    end with linkage[
      [linkage]
      preserving[
        list'[env]
        [get value code]
        make instruction sequence[
          list'[ [env] [val] ]
          list[target]
          '[
            perform[
              op[define variable!]
              const[$[var]]
              reg[val]
              reg[env]
            ]
            assign[ $[target] const[ok] ]
          ]
        ]
      ]
    ]
  ]
]

  <compilation of predicate, target val, linkage next>
  test[ op[false?] reg[val] ]
  branch[label[false branch]]
[true branch]
  <compilation of consequent with given target and given linkage or after if>
[false branch]
  <compilation of alternative with given target and linkage>
[after if]
```

## 578

```
define[  compile if[ [exp] [target] [linkage] ]
  let[
    [t branch]  make label['true branch]
    [f branch]  make label['false branch]
    [after if]  make label['after if]
    let[
      [consequent linkage]  if[ eq?[[linkage]['next]] [after if] [linkage] ]
      let[
        [p code]  compile[ if predicate[exp] ['val] ['next] ]
        [c code]  compile[ if consequent[exp] [target] [consequent linkage] ]
        [a code]  compile[ if alternative[exp] [target] [linkage] ]
        preserving[
          list'[ [env] [continue] ]
          [p code]
          append instruction sequences[
            make instruction sequence[
              list'[val]
              [nil]
              '[
                test[ op[false?] reg[val] ]
                branch[label[$[f branch]]]
              ]
            ]
            parallel instruction sequences[
              append instruction sequences[ [t branch] [c code] ]
              append instruction sequences[ [f branch] [a code] ]
            ]
            [after if]
          ]
        ]
      ]
    ]
  ]
]

define[  [label counter]  [0]  ]

define[  new label number[]
  set![ [label counter] +[[1][label counter]] ]
  [label counter]
]

define[  make label[name]
  string->symbol[
    string append[
      symbol->string[name]
      number->string[new label number[]]
    ]
  ]
]
```

## 579

```
define[  compile sequence[ [seq] [target] [linkage] ]
  ?[
    last exp?[seq]  compile[ first exp[seq] [target] [linkage] ]
    preserving[
      list'[ [env] [continue] ]
      compile[ first exp[seq] [target] ['next] ]
      compile sequence[ rest exps[seq] [target] [linkage] ]
    ]
  ]
]
```

## 580

```
define[  compile lambda[ [exp] [target] [linkage] ]
  let[
    [proc entry]  make label['entry]
    [after lambda]  make label['after lambda]
    let[
      [lambda linkage]  ?[ eq?[[linkage]['next]] [after lambda] [linkage] ]
      append instruction sequences[
        tack on instruction sequence[
          end with linkage[
            [lambda linkage]
            make instruction seqeunce[
              list'[env]
              list[target]
              '[
                assign[
                  $[target]
                  op[make compiled procedure]
                  label[$[proc entry]]
                  reg[env]
                ]
              ]
            ]
          ]
          compile lambda body[ [exp] [proc entry] ]
        ]
        [after lambda]
      ]
    ]
  ]
]

define[  make compiled procedure[ [entry] [env] ]
  list[ ['compiled procedure] [entry] [env] ]
]

define[  compiled procedure?[proc]
  tagged list?[ [proc] ['compiled procedure] ]
]

define[  compiled procedure entry[c proc]
  cadr[c proc]
]

define[  compiled procedure env[c proc]
  caddr[c proc]
]
```

## 581

```
define[  compile lambda body[ [exp] [proc entry] ]
  let[
    [formals]  lambda parameters[exp]
    append instruction sequences[
      make instruction sequence[
        list'[ [env] [proc] [argl] ]
        list'[env]
        '[
          $[proc entry]
            assign[ [env] op[compiled procedure env] reg[proc] ]
            assign[
              [env]
              op[extend environment]
              const[$[formals]]
              reg[argl]
              reg[env]
            ]
        ]
      ]
      compile sequence[ lambda body[exp] ['val] ['return] ]
    ]
  ]
]
```

## 582

```
define[  compile application[ [exp] [target] [linkage] ]
  let[
    [proc code]  compile[ operator[exp] ['proc] ['next] ]
    [operand codes]  map[
      fun[  [operand]
        compile[ [operand] ['val] ['next] ]
      ]
      operands[exp]
    ]
    preserving[
      list'[ [env] [continue] ]
      [proc code]
      preserving[
        list'[ [proc] [continue] ]
        construct arglist[operand codes]
        compile procedure call[ [target] [linkage] ]
      ]
    ]
  ]
]

<compilation of last operand, targeted to val>
assign[ [argl] op[list] reg[val] ]
<compilation of next operand, targeted to val>
assign[ [argl] op[cons] reg[val] reg[argl] ]
...
<compilation of first operand, targeted to val>
assign[ [argl] op[cons] reg[val] reg[argl] ]

assign[ [argl] const[nil] ]
```

Or perhaps the last line should be something like:

```
assign[ [argl] nil[] ]
```

To distinguish `nil` from the string/symbol `"nil"`.

## 583

```
define[  construct arglist[operand codes]
  let[
    [operand codes]  reverse[operand codes]
    ?[
      null?[operand codes]  make instruction sequence[
        list'[]
        list'[argl]
        '[
          assign[ [argl] nil[] ]
        ]
      ]
      let[
        [code to get last arg]  append instruction sequences[
          car[operand codes]
          make instruction sequence[
            list'[val]
            list'[argl]
            '[
              assign[ [argl] op[list] reg[val] ]
            ]
          ]
        ]
        ?[
          null?[cdr[operand codes]]  [code to get last arg]
          preserving[
            list'[env]
            [code to get last arg]
            code to get rest args[cdr[operand codes]]
          ]
        ]
      ]
    ]
  ]
]

define[  code to get rest args[operand codes]
  let[
    [code for next arg]  preserving[
      list'[argl]
      car[operand codes]
      make instruction sequence[
        list'[ [val] [argl] ]
        list'[argl]
        '[
          assign[ [argl] op[cons] reg[val] reg[argl] ]
        ]
      ]
    ]
    ?[
      null?[cdr[operand codes]]  [code for next arg]
      preserving[
        list'[env]
        [code for next arg]
        code to get rest args[cdr[operand codes]]
      ]
    ]
  ]
]
```

## 584

```
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch]]
[compiled branch]
  <code to apply compiled procedure with given target and appropriate linkage>
[primitive branch]
  assign[
    [<target>]
    op[apply primitive procedure]
    reg[proc]
    reg[argl]
  ]
  <linkage>
[after call]

define[  compile procedure call[ [target] [linkage] ]
  let[
    [primitive branch]  make label['primitive branch]
    [compiled branch]  make label['compiled branch]
    [after call]  make label['after call]
    let[
      [compiled linkage]  ?[ eq?[[linkage]['next]] [after call] [linkage] ]
      append instruction sequences[
        make instruction sequence[
          list'[proc]
          list'[]
          '[
            test[ op[primitive procedure?] reg[proc] ]
            branch[label[$[primitive branch]]]
          ]
        ]
        parallel instruction sequences[
          append instruction sequences[
            [compiled branch]
            compile proc appl[ [target] [compiled linkage] ]
          ]
          append instruction sequences[
            [primitive branch]
            end with linkage[
              [linkage]
              make instruction sequence[
                list'[ [proc] [argl] ]
                list[target]
                '[
                  assign[ $[target] op[apply primitive procedure] reg[proc] reg[argl] ]
                ]
              ]
            ]
          ]
        ]
        [after call]
      ]
    ]
  ]
]
```

## 585

```
  assign[ [continue] label[proc return] ]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[proc return]
  assign[ [<target>] reg[val] ]                    included if target is not val
  goto[label[<linkage>]]                           linkage code

  save[continue]
  assign[ [continue] label[proc return]]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[proc return]
  assign[ [<target>] reg[val] ]                    included if target is not val
  restore[continue]
  goto[reg[continue]]                              linkage code
```

## 586

```
<set up continue for linkage>
assign[ [val] op[compiled procedure entry] reg[proc] ]
goto[reg[val]]

assign[ [continue] label[<linkage>] ]
assign[ [val] op[compiled procedure entry] reg[proc] ]
goto[reg[val]]

assign[ [val] op[compiled procedure entry] reg[proc] ]
goto[reg[val]]
```

## 587

```
define[  compile proc appl[ [target] [linkage] ]
  ?[
    and[ 
      eq?[ [target] [val] ] 
      not[eq?[ [linkage] ['return] ]] 
    ]  make instruction sequence[
      list'[proc]
      [all regs]
      '[
        assign[ [continue] label[$[linkage]] ]
        assign[ [val] op[compiled procedure entry] reg[proc] ]
        goto[reg[val]]
      ]
    ]
    and[
      not[eq?[ [target] ['val] ]]
      not[eq?[ [linkage] ['return] ]]
    ]  let[
      [proc return]  make label['proc return]
      make instruction sequence[
        list'[proc]
        [all regs]
        '[
          assign[ [continue] label[$[proc return]] ]
          assign[ [val] op[compiled procedure entry] reg[proc] ]
          goto[reg[val]]
          $[proc return]
          assign[ $[target] reg[val] ]
          goto[label[$[linkage]]]
        ]
      ]
    ]
    and[
      eq?[ [target] ['val] ]
      eq?[ [linkage] ['return] ]
    ]  make instruction sequence[
      list'[ [proc] [continue] ]
      [all regs]
      '[
        assign[ [val] op[compiled procedure entry] reg[proc] ]
        goto[reg[val]]
      ]
    ]
    and[
      not[eq?[ [target] [val] ]]
      eq?[ [linkage] ['return] ]
    ]  error[
      ['return linkage, target not val -- COMPILE]
      [target]
    ]
  ]
]

define[  [all regs]  list'[ [env] [proc] [val] [argl] [continue] ]  ]
```

## 588

```
define[  registers needed[s]
  ?[  symbol?[s]  [nil]  car[s]  ]
]

define[  registers modified[s]
  ?[  symbol?[s]  [nil]  cadr[s]  ]
]

define[  statements[s]
  ?[  symbol?[s]  list[s]  caddr[s]  ]
]

define[  needs register?[ [seq] [reg] ]
  memq[ [reg] registers needed[seq] ]
]

define[  modifies register?[ [seq] [reg] ]
  memq[ [reg] registers modified[seq] ]
]
```

## 589

```
define[  append instruction sequences[...[seqs]]
  define[  append 2 sequences[ [seq1] [seq2] ]
    make instruction sequence[
      list union[
        registers needed[seq1]
        list difference[
          registers needed[seq2]
          registers modified[seq1]
        ]
      ]
      list union[
        registers modified[seq1]
        registers modified[seq2]
      ]
      append[ statements[seq1] statements[seq2] ]
    ]
  ]
  define[  append seq list[seqs]
    ?[
      null?[seqs]  empty instruction sequence[]
      append 2 sequences[
        car[seqs]
        append seq list[cdr[seqs]]
      ]
    ]
  ]
  append seq list[seqs]
]

define[  list union[ [s1] [s2] ]
  ?[
    null?[s1]  [s2]
    memq[ car[s1] [s2] ]  list union[ cdr[s1] [s2] ]
    cons[  
      car[s1]  
      list union[ cdr[s1] [s2] ]  
    ]
  ]
]

define[  list difference[ [s1] [s2] ]
  null?[s1]  [nil]
  memq[ car[s1] [s2] ]  list difference[ cdr[s1] [s2] ]
  cons[
    car[s1]
    list difference[ cdr[s1] [s2] ]
  ]
]
```

## 590

```
define[  preserving[ [regs] [seq1] [seq2] ]
  ?[
    null?[regs]  append instruction sequences[ [seq1] [seq2] ]
    let[
      [first reg]  car[regs]
      ?[
        and[
          needs register?[ [seq2] [first reg] ]
          modifies register?[ [seq1] [first reg] ]
        ]  preserving[
          cdr[regs]
          make instruction sequence[
            list union[
              list[first reg]
              registers needed[seq1]
            ]
            list difference[
              registers modified[seq1]
              list[first reg]
            ]
            append[
              '[save[$[first reg]]]
              statements[seq1]
              '[restore[$[first reg]]]
            ]
          ]
          [seq2]
        ]
        preserving[ cdr[regs] [seq1] [seq2] ]
      ]
    ]
  ]
]

define[  tack on instruction sequence[ [seq] [body seq] ]
  make instruction sequence[
    registers needed[seq]
    registers modified[seq]
    append[ statements[seq] statements[body seq] ]
  ]
]
```

## 591

```
define[  parallel instruction sequences[ [seq1] [seq2] ]
  make instruction sequence[
    list union[
      registers needed[seq1]
      registers needed[seq2]
    ]
    list union[
      registers modified[seq1]
      registers modified[seq2]
    ]
    append[ statements[seq1] statements[seq2] ]
  ]
]

compile[
  '[
    define[  factorial[n]
      ?[
        =[ [n] [1] ]  [1]
        *[  factorial[-[ [n] [1] ]]  [n]  ]
      ]
    ]
  ]
  ['val]
  ['next]
]

<save env if modified by code to compute value>
<compilation of definition value, target val, linkage next>
<restore env if saved above>
perform[
  op[define variable!]
  const[factorial]
  reg[val]
  reg[env]
]
assign[ [val] const[ok] ]
```

## 592

```
  assign[ [val] op[make compiled procedure] label[entry2] reg[env] ]
  goto[label[after lambda1]]
[entry2]
  assign[ [env] op[compiled procedure env] reg[proc] ]
  assign[ [env] op[extend environment]
    const[list[n]]
    reg[argl]
    reg[env]
  ]
  <compilation of procedure body>
[after lambda 1]
  perform[ op[define variable!]
    const[factorial]
    reg[val]
    reg[env]
  ]
  assign[ [val] const[ok] ]

?[
  =[ [n] [1] ]  [1]
  *[  factorial[-[ [n] [1] ]]  [n]  ]
]
```

Note: translated `(const (n))` to `const[list[n]]`. Perhaps that's not the best representation. 

## 593

```
  <save continue, env if modified by predicate and needed by branches>
  <compilation of predicate, target val, linkage next>
  <restore continue, env if saved above>
  test[ op[false?] reg[val] ]
  branch[label[false branch4]]
[true branch5]
  <compilation of true branch, target val, linkage return>
[false branch4]
  <compilation of false branch, target val, linkage return>
[after if3]

  assign[ [proc] op[lookup variable value] const[=] reg[env] ]
  assign[ [val] const[1] ]
  assign[ [argl] op[list] reg[val] ]
  assign[ [val] op[lookup variable value] const[n] reg[env] ]
  assign[ [argl] op[cons] reg[val] reg[argl] ]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch17]]
[compiled branch16]
  assign[ [continue] label[after call15] ]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch17]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]
[after call15]
```

## 594

```
  assign[ [val] const[1] ]
  goto[reg[continue]]

define[  factorial alt[n]
  ?[
    =[ [n] [1] ]  [1]
    *[  [n]  factorial alt[-[ [n] [1] ]]  ]
  ]
]

define[  factorial[n]
  define[  iter[ [product] [counter] ]
    ?[
      >[ [counter] [n] ]  [product]
      iter[
        *[ [counter] [product] ]
        +[ [counter] [1] ]
      ]
    ]
  ]
  iter[ [1] [1] ]
]
```

## 595

```
assign[ [val] op[lookup variable value] const[a] reg[env] ]
assign[ [val] op[+] reg[val] const[1] ]
```

## 596

```
construct the procedure and skip over code for the procedure body
  assign[ [val] op[make compiled procedure] label[entry2] reg[env] ]
  goto[label[after lambda1]]

[entry]         calls to factorial will enter here
  assign[ [env] op[compiled procedure env] reg[proc] ]
  assign[ [env] op[extend environment] const[list[n]] reg[argl] reg[env] ]
begin actual procedure body
  save[continue]
  save[env]

compute (= n 1)
  assign[ [proc] op[lookup variable value] const[=] reg[env] ]
  assign[ [val] const[1] ]
  assign[ [argl] op[list] reg[val] ]
  assign[ [val] op[lookup variable value] const[n] reg[env] ]
  assign[ [argl] op[cons] reg[val] reg[argl] ]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch17]]
[compiled branch16]
  assign[ [continue] label[after call15]]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch17]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]

[after call15]     val now contains result of (= n 1)
  restore[env]
  restore[continue]
  test[ op[false?] reg[val] ]
  branch[label[false branch4]]
[true branch5]     return 1
  assign[ [val] const[1] ]
  goto[reg[continue]]

[false branch4]
compute and return (* (factorial (- n 1)) n)
  assign[ [proc] op[lookup variable value] const[*] reg[env] ]
  save[continue]
  save[proc]       save * procedure
  assign[ [val] op[lookup variable value] const[n] reg[env] ]
  assign[ [argl] op[list] reg[val] ]
  save[argl]       save partial argument list for *

compute (factorial (- n 1)), which is the other argument for *
  assign[ [proc] op[lookup variable value] const[factorial] reg[env] ]
  save[proc]       save factorial procedure
```

## 597

```
compute (- n 1), which is the argument for factorial
  assign[ [proc] op[lookup variable value] const[-] reg[env] ]
  assign[ [val] const[1] ]
  assign[ [argl] op[list] reg[val] ]
  assign[ [val] op[lookup variable value] const[n] reg[env] ]
  assign[ [argl] op[cons] reg[val] reg[argl] ]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch8]]
[compiled branch7]
  assign[ [continue] label[after call6]]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch8]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]

[after call6]       val now contains result of (- n 1)
  assign[ [argl] op[list] reg[val] ]
  restore[proc]     restore factorial
apply factorial
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch11]]
[compiled branch10]
  assign[ [continue] label[after call9] ]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch11]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]

[after call9]       val now contains result of (factorial (- n 1))
  restore[argl]     restore partial argument list for *
  assign[ [argl] op[cons] reg[val] reg[argl] ]
  restore[proc]     restore *
  restore[continue]
apply * and return its value
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch14]]
[compiled branch13]
note that a compound procedure here is called tail-recursively
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch14]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]
  goto[reg[continue]]
[after call12]
[after if3]
[after lambda1]
assign the procedure to the variable factorial
  perform[ op[define variable!] const[factorial] reg[val] reg[env] ]
  assign[ [val] const[ok] ]
```

## 598

```
  assign[ [val] op[make compiled procedure] label[entry16] reg[env] ]
  goto[label[after lambda15]]
[entry16]
  assign[ [env] op[compiled procedure env] reg[proc] ]
  assign[ [env] op[extend environment] const[list[x]] reg[argl] reg[env] ]
  assign[ [proc] op[lookup variable value] const[+] reg[env] ]
  save[continue]
  save[proc]
  save[env]
  assign[ [proc] op[lookup variable value] const[g] reg[env] ]
  save[proc]
  assign[ [proc] op[lookup variable value] const[+] reg[env] ]
  assign[ [val] const[2] ]
  assign[ [argl] op[list] reg[val] ]
  assign[ [val] op[lookup variable value] const[x] reg[env] ]
  assign[ [argl] op[cons] reg[val] reg[argl] ]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch19]]
[compiled branch18]
  assign[ [continue] label[after call17] ]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch19]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]
[after call17]
  assign[ [argl] op[list] reg[val] ]
  restore[proc]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branch22]]
[compiled branch21]
  assign[ [continue] label[after call20] ]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch22]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]
```

## 599

```
[after call20]
  assign[ [argl] op[list] reg[val] ]
  restore[env]
  assign[ [val] op[lookup variable value] const[x] reg[env] ]
  assign[ [argl] op[cons] reg[val] reg[argl] ]
  restore[proc]
  restore[continue]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive branc25]]
[compiled branch24]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
[primitive branch25]
  assign[ [val] op[apply primitive procedure] reg[proc] reg[argl] ]
  goto[reg[continue]]
[after call23]
[after lambda15]
  perform[ op[define variable!] const[f] reg[val] reg[env] ]
  assign[ [val] const[ok] ]
```

## 600

```
let[
  [x]  [3]
  [y]  [4]
  fun[  [ [a] [b] [c] [d] [e] ]
    let[
      [y]  *[ [a] [b] [x] ]
      [z]  +[ [c] [d] [x] ]
      *[ [x] [y] [z] ]
    ]
  ]
]

fun[  [ [x] [y] ]
  fun[  [ [a] [b] [c] [d] [e] ]
    fun[  [ [y] [z] ]
      *[ [x] [y] [z] ]
    ].[
      *[ [a] [b] [x] ]
      *[ [c] [d] [x] ]
    ]
  ]
].[ [3] [4] ]
```

## 601

```
fun[  [ [x] [y] ]
  fun[  [ [a] [b] [c] [d] [e] ]
    fun[  [ [y] [z] ]
      [<e1>]
    ].[
      [<e2>]
      *[ [c] [d] [x] ]
    ]
  ]
].[ [3] [4] ]
```

## 602

```
find variable[  ['c]  list'[ [[y][z]] [[a][b][c][d][e]] [[x][y]] ]  ]

find variable[  ['x]  list'[ [[y][z]] [[a][b][c][d][e]] [[x][y]] ]  ]

find variable[  ['w]  list'[ [[y][z]] [[a][b][c][d][e]] [[x][y]] ]  ]

```

## 603

```
fun[  [ [+] [*] [a] [b] [x] [y] ]
  +[  *[ [a] [x] ]  *[ [b] [y] ]  ]
]
```

## 604

```
compile and go[
  '[
    define[  factorial[n]
      ?[
        =[ [n] [1] ]  [1]
        *[  factorial[-[ [n] [1] ]]  [n]  ]
      ]
    ]
  ]
]

factorial[5]


[apply dispatch]
  test[ op[primitive procedure?] reg[proc] ]
  branch[label[primitive apply]]
  test[ op[compound procedure?] reg[proc] ]
  branch[label[compound apply]]
  test[ op[compiled procedure?] reg[proc] ]
  branch[label[compiled apply]]
  goto[label[unknown procedure type]]

[compiled apply]
  restore[continue]
  assign[ [val] op[compiled procedure entry] reg[proc] ]
  goto[reg[val]]
```

## 605

```
  branch[label[external entry]]       branches if flag is set
[read eval print loop]
  perform[op[initialize stack]]
  ...

[external entry]
  perform[op[initialize stack]]
  assign[ [env] op[get global environment] ]
  assign[ [continue] label[print result] ]
  goto[reg[val]]

define[  start eceval[]
  set![ [the global environment] setup environment[] ]
  set register contents![ [eceval] ['flag] [false] ]
  start[eceval]
]

define[  user print[object]
  ?[
    compound procedure?[object]  display[list[
      ['compound procedure]
      procedure parameters[object]
      procedure body[object]
      ['<procedure env>]
    ]]
    compiled procedure?[object]  display['<compiled procedure>]
    display[object]
  ]
]
```

## 606

```
define[  compile and go[expression]
  let[
    [instructions]  assemble[
      statements[
        compile[ [expression] ['val] ['return] ]
        [eceval]
      ]
    ]
    [
      set![ [the global environment] setup environment[] ]
      set register contents![ [eceval] ['val] [instructions] ]
      set register contents![ [eceval] ['flag] [true] ]
      start[eceval]
    ]
  ]
]

compile and go[
  '[
    define[  factorial[n]
      ?[
        =[ [n] [1] ]  [1]
        *[  factorial[-[ [n] [1] ]]  [n]  ]
      ]
    ]
  ]
]

factorial[5]
```

## 609

```
define[  fib[n]
  ?[
    <[ [n] [2] ]  [n]
    +[
      fib[-[ [n] [1] ]]
      fib[-[ [n] [2] ]]
    ]
  ]
]

  assign[ [compapp] label[compound apply] ]
  branch[label[external entry]]              branches if flag is set
[read eval print loop]
  ...
```

## 610

```
compile and run[
  '[
    define[  factorial[n]
      ?[
        =[ [n] [1] ]  [1]
        *[  factorial[-[ [n] [1] ]]  [n]  ]
      ]
    ]
  ]
]

factorial[5]
```

## Outro

So what have we learned?

Some points:

* We can have a minimal Lisp-like language that supports identifiers with spaces.
* We can use spacing and style to alleviate bracket fatigue.
* Having additional syntax like `f[x].[y]` is very handy. It should probably be highly integrated, i.e. `f[x].[y]` should be one expression in the language, rather than two.
* Sometimes it might be useful to use `[.]` to refer to the result of the previous expression in a block. This obviates the need for pipeline operators, etc.
* Symbols are not strictly necessary -- immutable strings can supplant them.
* Seemingly small tweaks in syntax can have unforseen consequences.
* Lots of things in Lisps are there only because of tradition.
* ...
* SICP is great!
