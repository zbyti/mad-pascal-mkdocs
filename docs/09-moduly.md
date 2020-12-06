# Moduły

Moduły (UNIT) w **MP** składają się z sekcji `INTERFACE` **wymagany**, `IMPLEMENTATION` **wymagany**, `INITIALIZATION` *opcjonalny*.

```pascal
unit test;

interface

type  TUInt24 =
  record
    byte0: byte;
    byte1: byte;
    byte2: byte;
  end;

const
  LoRes = 1;
  MedRes = 2;
  HiRes = 3;

  procedure Print(a: string);

implementation

uses test2;

procedure Print(a: string);
begin

  writeln(a);

end;

end.
```