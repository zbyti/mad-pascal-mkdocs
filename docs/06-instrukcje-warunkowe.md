# Instrukcje warunkowe

## case of else

Obecnie **Mad Pascal** akceptuje dla zmiennej `CASE` typy tylko o długości 1 bajta: `SHORTINT` `BYTE` `CHAR` `BOOLEAN`.

```pascal
 case a of             // dla zmiennej A typu CHAR
  'A'..'Z': begin end;
  '0'..'9': begin end;
   '+','*': begin end;
 end;
```

## if then else

Instrukcje warunkowe `IF` mogą być zagnieżdżane. Wykorzystywane jest to przy budowie bardziej złożonych warunków.
