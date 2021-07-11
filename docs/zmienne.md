#

## [VAR](https://www.freepascal.org/docs-html/ref/refse22.html#x53-730004.2)

Słowo `VAR` rozpoczyna sekcję deklaracji zmiennych.

```delphi
var
    label: type;
    label: type = value;
```

```delphi
var
    a: word;
    b: byte = 1;
    c: Boolean = true;

    s: string = 'Atari';

    tb: array [0..3] of byte = (0,1,2,3);
```

## [ABSOLUTE]()

Modyfikator `ABSOLUTE` pozwala ustalić adres w pamięci dla zmiennych `VAR`.

```delphi
var
   a: byte absolute $0600;
   tb: array [0..255] of byte absolute $a000;
```

## [REGISTER]()

Modyfikator `REGISTER` ustala adres pamięci dla zmiennych `VAR` na stronie zerowej.

```delphi
var
   a: byte register;
   c: integer register;
```

	!!! UWAGA !!!

	Z tego samego obszaru 16 bajtów strony zerowej korzysta kompilator alokując tam swoje
	programowe rejestry `EDX` `ECX` `EAX` dlatego użycie modyfikatora `REGISTER` nie jest
	możliwe kiedy procedura lub funkcja też używa `REGISTER`.


```delphi
procedure test(a,b,c: integer); register;
```