# Składnia

## [Komentarze](http://www.freepascal.org/docs-html/ref/refse2.html)

W **MP** do oznaczenia komentarza jednoliniowego służą znaki `//`, dla wieloliniowego klamry `{ }`, lub `(* *)`.

```pascal
// to jest komentarz
inc(a); // to jest komentarz

(* komentarz *)

(*
  komentarz
*)

{ to
  jest
  komentarz
}
```

## Zarezerwowane słowa

### rozkazy

```pascal
absolute           and                 array              asm               begin
case               const               div                do                downto
else               end                 file               for               function
if                 implementation      interface          main              mod
not                of                  or                 procedure         program
record             repeat              shl                shr               stack
string             then                to                 type              unit
until              uses                var                while             xor
```

### stałe

```pascal
pi
true
false
```

## Wyrażenia

### [Liczby](http://www.freepascal.org/docs-html/ref/refse6.html)

#### zapis decymalny
```pascal
-100
-2437325
1743
```
#### zapis hexadecymalny
```pascal
$100
$e430
$000001
```
#### zapis binarny
```pascal
%0001001010
%000000001
%001000
```
#### zapis kodami ATASCII
```pascal
'a'
'fds'
'W'
#65#32#65
#$9b
```

### Operatory

#### arytmetyczne

```pascal
+   Addition
-   Subtraction
*   Multiplication
/   Division
DIV Integer division
MOD Remainder
```

#### bitowe

```pascal
NOT Bitwise negation (unary)
AND Bitwise and
OR  Bitwise or
XOR Bitwise xor
SHL Bitwise shift to the left
SHR Bitwise shift to the right
```

#### logiczne

```pascal
NOT logical negation (unary)
AND logical and
OR  logical or
XOR logical xor
```

#### relacji

```pascal
=   Equal
<>  Not equal
<   Less than
>   Greater than
<=  Less than or equal
>=  Greater than or equal
```

## [Dyrektywy kompilatora](http://www.freepascal.org/docs-html/prog/progch1.html#x5-40001)

Zapis dyrektyw kompilatora ma postać:

    {$dyrektywa parametry}
    {$lista_dyrektyw_przełącznikowych}

Dyrektywa stanowi komentarz, w którym pierwszy znak $ odróżnia zwykły komentarz, od dyrektywy kompilatora.

### [CONDITIONAL](https://wiki.freepascal.org/Conditional_compilation)

```
CONDITIONAL {$IFDEF label}, {$IFNDEF label}, {$ELSE}, {$ENDIF}, {$DEFINE label}, {$UNDEF label}
```

```
{$define test}

const
  {$ifdef test}
  a=1;
  {$else}
  a=2;
  {$endif}
```

Z poziomu assemblera dostęp do zdefiniowanych etykiet `$DEFINE` możliwy jest przez `MAIN.@DEFINES.label`

### [FASTMUL](https://codebase64.org/doku.php?id=base:seriously_fast_multiplication)

```
{$f $70}  // fastmul at $7000
```

Alternatywne procedury szybkiego mnożenia dla typu `BYTE` `SHORTINT` `WORD` `SMALLINT` `SHORTREAL`. Procedury zajmują **2KB** i są umieszczane od adresu __PAGE*256__.

### [IOCHECK](https://www.freepascal.org/docs-html/prog/progsu38.html#x45-440001.2.38)

```
IOCHECK {$I+} {$I-}

{i+}  IOCHECK ON  default
{i-}  IOCHECK OFF
```

Dla {$i+} w przypadku wystąpienia błędów transmisji **I/O** dla: `RESET` `REWRITE` `BLOCKREAD` `BLOCKWRITE` `CLOSE`, wykonywany program zostaje zatrzymany, generowany jest komunikat błędu `ERROR xxx`. Wyłączenie `IOCHECK {$i-}` przydaje się gdy chcemy sprawdzić istnienie pliku na dysku, np.:

```pascal
function FileExists(name: TString): Boolean;
var f: file;
begin

  {$I-}     // io check off
  Assign (f, name);
  Reset (f);
  Result:=(IoResult<128) and (length(name)>0);
  Close (f);
  {$I+}     // io check

end;
```

W blokach `PROCEDURE`, `FUNCTION` dyrektywa `IOCHECK` jest zasięgu lokalnego, po zakończeniu kompilacji takiego bloku przywracana jest wartość `IOCHECK`, która została określona poza takim blokiem.

### `INCLUDE DATE`

```
    {$INCLUDE %DATE%}, {$I %DATE%}
```

Dyrektywa dołączenia tekstu z aktualną datą kompilacji.

---

### `INCLUDE TIME`

```
    {$INCLUDE %TIME%}, {$I %TIME%}
```

Dyrektywa dołączenia tekstu z aktualnym czasem kompilacji.

---

### `INCLUDE filename`

```
    {$INCLUDE filename}, {$I filename}
```

Dyrektywa dołączenia tekstu zawartego w pliku.

---

### `LIBRARY PATH`

```
{$LIBRARYPATH path1;path2;...}
```

Dyrektywa pozwalająca wskazać dodatkowe ścieżki poszukiwań dla bibliotek `unit`.

---

### INFO

```
{$INFO user_defined}
```

---

### WARNING

```
{$WARNING user_defined}
```

---

### ERROR

```
{$ERROR user_defined}
```

---

### DEFINE BASICOFF

```
    {$DEFINE BASICOFF}
```

Dodatkowy blok programu realizujący wyłączenie BASIC-a.

---

### DEFINE ROMOFF

```
    {$DEFINE ROMOFF}
```

Zyskujemy dostęp do pamięci *pod ROM-em*, `$C000..$CFFF`, `$D800..$FFFF`.

Zestaw znaków z **ROM** `$E000..$E3FF` zostaje przepisany pod ten sam adres w **RAM**, zostaje zainstalowany handler przerwań `NMI`, `IRQ`. System operacyjny działa normalnie, można z poziomu **ASM** wywoływać procedury w nim zawarte poprzez makro `m@call`.

---

### RESOURCE

```
{$R filename}, {$RESOURCE filename}

RCLABEL RCTYPE RCFILE [PAR0 PAR1 PAR2 PAR3 PAR4 PAR5 PAR6 PAR7]
```

Dyrektywa dołączenia pliku z zasobami. Plik zasobów jest plikiem tekstowym, każdy jego kolejny wiersz powinien składać się z trzech pól rozdzielonych "białym znakiem": etykieta `RCLABEL` (jej deklaracja musi znaleźć się także w programie), typ zasobów `RCTYPE`, lokalizacja pliku `RCFILE`. Aktualnie w pliku `BASE\RES6502.ASM` znajdują się makra do obsługi 10 typów zasobów `RCTYPE`:

#### `RCDATA`

Dowolny typ danych.

#### `RCASM`

Plik w assemlerze, który zostanie dołączony i zasemblowany.

#### `DOSFILE`

Plik z nagłówkiem **Atari DOS**, adres ładowania takiego pliku powiniem być identyczny jak `RCLABEL`.

#### `RELOC`

Plik relokowalny w formacie **MadAssemblera**, plik zostanie poddany relokacji pod wskazany adres `RCLABEL`.

#### `RMT`

Plik modułu Raster Music Tracker-a, plik zostanie poddany relokacji pod wskazany adres `RCLABEL`.

#### `MPT`

Plik modułu Music ProTracker-a, plik zostanie poddany relokacji pod wskazany adres `RCLABEL`.

#### `CMC`

Plik modułu **Chaos Music Composer-a**, plik zostanie poddany relokacji pod wskazany adres `RCLABEL`.

#### `RMTPLAY`

Player dla modułu **RMT**, jako `RCFILE` podajemy plik `*.FEAT` oraz dodatkowo `PAR0` tryb playera `0..3`.

```
    0 => compile RMTplayer for 4 tracks mono
    1 => compile RMTplayer for 8 tracks stereo
    2 => compile RMTplayer for 4 tracks stereo L1 R2 R3 L4
    3 => compile RMTplayer for 4 tracks stereo L1 L2 R3 R4
```

#### `MPTPLAY`

Player dla modułu **MPT**.

#### `CMCPLAY`

Player dla modułu **CMC**.

#### `XBMP`

Plik **Windows Bitmap** (8 BitsPerPixel) ładowany do pamięci **VBXE** pod wskazany adres `RCLABEL` od indeksu koloru `PAR0` w palecie kolorów **VBXE nr 1**

Przykład:

```
bmp1  RCDATA   'pic.mic'
msx   MPT      'porazka.mpt'
play  RMTPLAY  'modul.feat' 1
bmp   XBMP     'pic.bmp' 80
```
