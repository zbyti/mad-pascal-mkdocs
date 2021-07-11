#

## [Komentarze](http://www.freepascal.org/docs-html/ref/refse2.html)

W **MP** do oznaczenia komentarza jednoliniowego służą znaki `//`, dla wieloliniowego klamry `{ }`, lub `(* *)`.

```delphi
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

```delphi
absolute           and                 array              asm               assembler
begin              case                const              div               do
downto             else                end                file              for
forward            function            if                 implementation    interrupt
interface          main                mod                not               of
or                 overload            pascal             procedure         program
record             register            repeat             shl               shr
string             then                to                 type              unit
until              uses                var                while             xor
```

### stałe

```delphi
pi
true
false
nil
eol
nan
infinity
neginfinity
```

## Wyrażenia

### [Liczby](http://www.freepascal.org/docs-html/ref/refse6.html)

#### zapis decymalny
```delphi
-100
-2437325
1743
```
#### zapis hexadecymalny
```delphi
$100
$e430
$000001
```
#### zapis binarny
```delphi
%0001001010
%000000001
%001000
```
#### zapis kodami ATASCII
```delphi
'a'
'fds'
'W'
#65#32#65
#$9b
```

### Operatory

#### arytmetyczne

```delphi
+   Addition
-   Subtraction
*   Multiplication
/   Division
DIV Integer division
MOD Remainder
```

#### bitowe

```delphi
NOT Bitwise negation (unary)
AND Bitwise and
OR  Bitwise or
XOR Bitwise xor
SHL Bitwise shift to the left
SHR Bitwise shift to the right
```

#### logiczne

```delphi
NOT logical negation (unary)
AND logical and
OR  logical or
XOR logical xor
```

#### relacji

```delphi
=   Equal
<>  Not equal
<   Less than
>   Greater than
<=  Less than or equal
>=  Greater than or equal
```

## [Dyrektywy kompilatora](http://www.freepascal.org/docs-html/prog/progch1.html#x5-40001)

Zapis dyrektyw kompilatora ma postać:

```delphi
{$dyrektywa parametry}
{$lista_dyrektyw_przełącznikowych}
```

Dyrektywa stanowi komentarz, w którym pierwszy znak $ odróżnia zwykły komentarz, od dyrektywy kompilatora.

### [WARUNKOWE](https://wiki.freepascal.org/Conditional_compilation)

```delphi
{$IFDEF label}
{$IFNDEF label}
{$ELSE}
{$ENDIF}
{$DEFINE label}
{$UNDEF label}
```

```delphi
{$define test}

const
  {$ifdef test}
  a=1;
  {$else}
  a=2;
  {$endif}
```

Z poziomu assemblera dostęp do zdefiniowanych etykiet `$DEFINE` możliwy jest przez `MAIN.@DEFINES.label`

### [$CODEALIGN PROC = value](https://www.freepascal.org/docs-html/prog/progsu9.html)

Dyrektywa `$CODEALIGN PROC` pozwala wyrównać generowany kod wynikowy do `VALUE` bajtów strony pamięci. Przed każdym blokiem `PROCEDURE`, `FUNCTION` wstawiany jest kod `.ALIGN VALUE`. Aby wyłączyć wyrównywanie należy ustawić `{$CODEALIGN PROC = 0}`

### [$CODEALIGN LOOP = value](https://www.freepascal.org/docs-html/prog/progsu9.html)

Dyrektywa `$CODEALIGN LOOP` pozwala wyrównać generowany kod wynikowy do `VALUE` bajtów strony pamięci. Przed każdą instrukcją iteracyjną `FOR`, `WHILE`, `REPEAT` wstawiany jest kod `.ALIGN VALUE`. Aby wyłączyć wyrównywanie należy ustawić `{$CODEALIGN LOOP = 0}`

### [$F, $FASTMUL](https://codebase64.org/doku.php?id=base:seriously_fast_multiplication)

```delphi
{$fastmul page}   // fastmul at page*256
{$f $70}          // fastmul at $7000
```

Alternatywne procedury szybkiego mnożenia dla typu `BYTE` `SHORTINT` `WORD` `SMALLINT` `SHORTREAL`. Procedury zajmują **2KB** i są umieszczane od adresu __PAGE*256__.

### [$I+, $I-, IOCHECK](https://www.freepascal.org/docs-html/prog/progsu38.html#x45-440001.2.38)

```delphi
{$I+}
{$I-}
```
    {i+}  IOCHECK ON  default
    {i-}  IOCHECK OFF


Dla `{$i+}` w przypadku wystąpienia błędów transmisji **I/O** dla: `RESET` `REWRITE` `BLOCKREAD` `BLOCKWRITE` `CLOSE`, wykonywany program zostaje zatrzymany, generowany jest komunikat błędu `ERROR xxx`.

Wyłączenie `IOCHECK {$i-}` przydaje się gdy chcemy sprawdzić istnienie pliku na dysku, np.:

```delphi
function FileExists(name: TString): Boolean;
var f: file;
begin

  {$I-}     // io check off
  Assign (f, name);
  Reset (f);
  Result:=(IoResult<128) and (length(name)>0);
  Close (f);
  {$I+}     // io check on

end;
```

W blokach `PROCEDURE`, `FUNCTION` dyrektywa `IOCHECK` jest zasięgu lokalnego, po zakończeniu kompilacji takiego bloku przywracana jest wartość `IOCHECK`, która została określona poza takim blokiem.

### [$I, $INCLUDE](https://www.freepascal.org/docs-html/prog/progsu41.html)

#### `%DATE%`

```delphi
{$INCLUDE %DATE%}
{$I %DATE%}
```

Parametr `%DATE%` pozwala dołączyć tekst z aktualną datą kompilacji.

#### `%TIME%`

```delphi
{$INCLUDE %TIME%}
{$I %TIME%}
```

Parametr `%TIME%` pozwala dołączyć tekst z aktualnym czasem kompilacji.

#### `FILENAME`

```delphi
{$INCLUDE filename}
{$I filename}
```

Parametr `FILENAME` pozwala dołączyć tekst zawarty w pliku.

### [$LIBRARYPATH](https://www.freepascal.org/docs-html/prog/progsu99.html)

```delphi
{$LIBRARYPATH path1;path2;...}
```

Dyrektywa `$LIBRARYPATH` pozwala wskazać dodatkowe ścieżki poszukiwań dla bibliotek `unit`.

### [$INFO](https://www.freepascal.org/docs-html/prog/progsu35.html#x42-410001.2.35)

```delphi
{$INFO user_defined}
```
Wygenerowanie komunikatu z informacją `INFO`.

### [$WARNING](https://www.freepascal.org/docs-html/prog/progsu81.html#x88-870001.2.81)

```delphi
{$WARNING user_defined}
```
Wygenerowanie komunikatu z ostrzeżeniem `WARNING`.

### [$ERROR](https://www.freepascal.org/docs-html/prog/progsu17.html#x24-230001.2.17)

```delphi
{$ERROR user_defined}
```
Wygenerowanie komunikatu z błędem `ERROR`.

### [$DEFINE](https://www.freepascal.org/docs-html/prog/progsu11.html#x18-170001.2.11)

#### `BASICOFF`

```delphi
{$DEFINE BASICOFF}
```
Powoduje utworzenie dodatkowego bloku programu, realizującego wyłączenie BASIC-a.

#### `ROMOFF`

```delphi
{$DEFINE ROMOFF}
```
Zyskujemy dostęp do pamięci *pod ROM-em*, `$C000..$CFFF`, `$D800..$FFFF`.

Zestaw znaków z **ROM** `$E000..$E3FF` zostaje przepisany pod ten sam adres w **RAM**, zostaje zainstalowany handler przerwań `NMI`, `IRQ`. System operacyjny działa normalnie, można z poziomu **ASM** wywoływać procedury w nim zawarte poprzez makro `m@call`.

    !!! UWAGA !!!

    W przypadku umieszczenia programu ANTIC-a Display List pod ROM-em każde naciśnięcie
    klawisza będzie powodować wywołanie przerwania IRQ obsługującego klawiaturę.

    Program ANTIC-a będzie zakłócany poprzez przełączanie ROM - RAM, w przypadku gdy
    korzystamy z przerwania Display Listy (DLI) może dojść do uszkodzenia stosu
    i wyłożenia się systemu.

### [$R, $RESOURCE](https://www.freepascal.org/docs-html/prog/progsu67.html#x74-730001.2.67)

```delphi
{$R filename}
{$RESOURCE filename}

RCLABEL RCTYPE RCFILE [PAR0 PAR1 PAR2 PAR3 PAR4 PAR5 PAR6 PAR7]
```

Dyrektywa dołączenia pliku z zasobami. Plik zasobów jest plikiem tekstowym, każdy jego kolejny wiersz powinien składać się z trzech pól rozdzielonych "białym znakiem": etykieta `RCLABEL` (jej deklaracja musi znaleźć się także w programie), typ zasobów `RCTYPE`, lokalizacja pliku `RCFILE`. Aktualnie w pliku `BASE\RES6502.ASM` znajdują się makra do obsługi 10 typów zasobów `RCTYPE`:

#### `RCDATA`

Dowolny typ danych.

#### `RCASM`

Plik w assemblerze, który zostanie dołączony i zasemblowany.

#### `DOSFILE`

Plik z nagłówkiem **Atari DOS**, adres ładowania takiego pliku powinien być identyczny jak `RCLABEL`.

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

```none
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

```none
bmp1  RCDATA   'pic.mic'
msx   MPT      'porazka.mpt'
play  RMTPLAY  'modul.feat' 1
bmp   XBMP     'pic.bmp' 80
```
