#

## [Ordinary](https://www.freepascal.org/docs-html/ref/refse9.html)

Do deklaracji stałych `CONST` służy znak `=`. Dopuszczalne jest użycie operatorów, nektórych funkcji i stałych:

`+` `-` `*` `/` `not` `and` `or` `div` `mod` `ord` `chr` `sizeof` `pi`


```pascal
const
  e = 2.7182818;       { Real type constant }
  f : single = 3.14;   { Single type constant }
  a = 2;               { Ordinal BYTE type constant }
  c = '4';             { Character type constant }
  s = 'atari';         { String type constant }
  sc = chr(32);
  ls = SizeOf(cardinal);

  x: word = 5;         { wymuszenie typu stałej }
```