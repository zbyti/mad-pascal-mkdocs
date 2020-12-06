# Procedury, funkcje, modyfikatory

## Procedury

**MP** pozwala na przekazanie do procedury maksymalnie `8` parametrów. Są dostępne trzy sposoby przekazywania parametrów - przez wartość, stałą `CONST` i zmienną `VAR`. Możliwe jest użycie modyfikatora `OVERLOAD` w celu przeciążenia procedur.

Dostępne modyfikatory procedur: `OVERLOAD` `ASSEMBLER` `FORWARD` `REGISTER` `INTERRUPT`.

Możliwa jest rekurencja procedur, pod warunkiem że parametry procedury będą przekazywane przez wartość, będą typu prostego - porządkowego. Typ rekordowy, wskaźnikowy nie będzie właściwie alokowany w pamięci.

## Funkcje

**MP** pozwala na przekazanie do funkcji maksymalnie `8 `parametrów. Są dostępne trzy sposoby przekazywania parametrów - przez wartość, stałą `CONST` i zmienną `VAR`. Wynik funkcji zwracamy przypisując go do nazwy funkcji lub korzystając z automatycznie deklarowanej zmiennej `RESULT`, np.:

```pascal
function add(a,b: word): cardinal;
begin
  Result := a+b;
end;

function mul(a,b: word): cardinal;
begin
  mul := a*b;
end;
```

Dostępne modyfikatory funkcji: `OVERLOAD` `ASSEMBLER` `FORWARD` `REGISTER` `INTERRUPT`.  `INTERRUPT` nie jest zalecane dla funkcji.

Możliwa jest rekurencja funkcji, pod warunkiem, że parametry funkcji będą przekazywane przez wartość, będą typu prostego - porządkowego. Typ rekordowy, wskaźnikowy nie będzie właściwie alokowany w pamięci.

## Modyfikatory

#### assembler

**Procedury/Funkcje** oznaczona przez ASSEMBLER mogą składać się tylko z bloku ASM. Kompilator nie dokonuje analizy składni takich bloków, traktuje je jak komentarz, ewentualne błędy zostaną wychwycone dopiero podczas asemblacji.

    procedure color(a: byte); assembler;
    asm
    {   mva a 712
    };
    end;

#### overload

**Procedury/Funkcje** przeciążone rozpoznawane są na podstawie listy parametrów.

```pascal
procedure suma(var i: integer; a,b: integer); overload;
begin
 i := a+b;
end;

procedure suma(var i: integer; a,b,c: integer); overload;
begin
 i := a+b+c;
end;

function fsuma(a,b: word): cardinal; assembler; overload;
asm
{
 adw a b result
};
end;

function fsuma(a,b: real): real; overload;
begin
 Result := a+b;
end;
```

#### forward

Jeżeli chcemy aby **procedura/funkcja** była zadeklarowana za miejscem jej pierwszego wywołania, należy użyć modyfikator FORWARD.

```
procedure nazwa [(lista-parametrów-formalnych)]; forward;

...
...
...

procedure nazwa;
begin
end;
```

#### register

Użycie modyfikatora `REGISTER` spowoduje że trzy pierwsze parametry formalne **procedury/funkcji** będą umieszczone na stronie zerowej, w 32-bitowych rejestrach programowych, odpowiednio `EDX`, `ECX`, `EAX`.

    procedure nazwa (a,b,c: cardinal); register;
    // a = edx
    // b = ecx
    // c = eax

#### interrupt

**Procedury/Funkcje** oznaczone przez `INTERRUPT` kompilator będzie kończył rozkazem `RTI` (standardowo `RTS`). Niezależnie czy w programie wystąpi wywołanie takiej **procedury/funkcji** kompilator zawsze wygeneruje dla niej kod. Zaleca się używanie bloku `ASM` w przypadku takich **procedur/funkcji**, w innym przypadku stos programowy Mad Pascala zostanie zniszczony, co może doprowadzić do niestabilnego działania programu, łącznie z zawieszeniem się komputera. Na wejściu **procedury/funkcji** oznaczonej przez `INTERRUPT` programista musi zadbać o zachowanie rejestrów **CPU** `A` `X` `Y`, na wyjściu o przywrócenie stanu takich rejestrów, kompilator ogranicza się tylko do wstawienia końcowego rozkazu `RTI`.

```
procedure dli; interrupt;
asm
{   pha

    lda #$c8
    sta wsync
    sta $d01a

    pla
};
end;             // rozkaz RTI zostanie wstawiony automatycznie
```
