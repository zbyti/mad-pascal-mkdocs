# Biblioteka podstawowa

W katalogu `LIB` **Mad-Pascala** znajdują się potrzebne do kompilacji podstawowe moduły `unit`, takie jak `SYSTEM` `CRT` `GRAPH` `SYSUTILS` `MATH` `DOS`. W programie wybierane są przez instrukcję `USES`, np.:

    uses crt, sysutils;

Moduł `SYSTEM` jest domyślnie dopisywany do listy `USES` i kompilowany jako pierwszy.

## SYSTEM

**Constants**

```
M_PI_2           = 6.283285;  // pi * 2
D_PI_2           = 1.570796;  // pi / 2
D_PI_180         = 0.017453;  // pi / 180

mGTIA            = 0;
mVBXE            = $80;
WINDOW           = $10;
NARROW           = $20;


VBXE_XDLADR      = $0000;     // XDLIST
VBXE_MAPADR      = $1000;     // COLOR MAP ADDRESS
VBXE_BCBADR      = $0100;     // BLITTER LIST ADDRESS
VBXE_OVRADR      = $5000;     // OVERLAY ADDRESS
VBXE_WINDOW      = $B000;     // 4K WINDOW $B000..$BFFF

iDLI             = 0;
iVBL             = 1;

CH_DELCHR        = $FE;
CH_ENTER         = $9B;
CH_ESC           = $1B;
CH_CURS_UP       = 28;
CH_CURS_DOWN     = 29;
CH_CURS_LEFT     = 30;
CH_CURS_RIGHT    = 31;

CH_TAB           = $7F;
CH_EOL           = $9B;
CH_CLR           = $7D;
CH_BEL           = $FD;
CH_DEL           = $7E;
CH_DELLINE       = $9C;
CH_INSLINE       = $9D;

COLOR_BLACK      = $00;
COLOR_WHITE      = $0e;
COLOR_RED        = $32;
COLOR_CYAN       = $96;
COLOR_VIOLET     = $68;
COLOR_GREEN      = $c4;
COLOR_BLUE       = $74;
COLOR_YELLOW     = $ee;
COLOR_ORANGE     = $4a;
COLOR_BROWN      = $e4;
COLOR_LIGHTRED   = $3c;
COLOR_GRAY1      = $04;
COLOR_GRAY2      = $06;
COLOR_GRAY3      = $0a;
COLOR_LIGHTGREEN = $cc;
COLOR_LIGHTBLUE  = $7c;
```

**Types**

* `TPoint` definicja współrzędnych (x,y).

```
    TPoint = record x,y: SmallInt end;
```

* `TRect` definicja położenia i rozmiaru czworokąta o parametrach (left, top) - lewy górny narożnik, (right, bottom) - prawy dolny narożnik.

```
    TRect = record left, top, right, bottom: smallint end;
```

* `TString` definicja krótkiego ciągu znakowego wykorzystywanego do przekazywania nazw plików itp.

```
    TString = string[32];
```

**Variables**

* `IOResult` kod błędu (>127) dla ostatnio przeprowadzonej operacji I/O.

```
    IOResult: byte;
```

* `ScreenWidth` zmienna przechowująca aktualną szerokość ekranu. Domyślnie jest to wartość 40 dla ekranu edytora.

```
    ScreenWidth: word = 40
```

* `ScreenHeight` zmienna przechowująća aktualną wysokość ekranu. Domyślnie jest to wartość 24 dla ekranu edytora.

```
    ScreenHeight: word = 24;
```

**Procedures and functions**

* `Abs` funkcja obliczająca wartość bezwzględną podanej liczby (ang. **Absolute value**). Wartość bezwzględna liczby nieujemnej to ta sama liczba, a liczby ujemnej - liczba do niej przeciwna. Funkcja w przypadku podania jej argumentu całkowitego zwraca wynik również typu całkowitego.

```
    function Abs(x: real): real;
    function Abs(x: integer): integer;
```

* `ArcTan` funkcja (arcus tangens) zwraca wartość kąta, którego tangens wynosi x.

```
    function ArcTan(x: real): real;
```

* `Assign` procedura przypisuje zmiennej plikowej `F` plik o nazwie `FileName`. Aby móc odwoływać się do jakiegoś pliku, zawsze należy najpierw użyć procedury `Assign`. Przy dalszych operacjach pliki są identyfikowane przy pomocy zmiennej plikowej, a nie nazwy.

```
    procedure Assign(var F:File; FileName:string)
```

* `BinStr` funkcja zwraca ciąg znakowy z reprezentacją binarną wartości `Value`. `Digits` określa długość ciągu, który maksymalnie może liczyć 32 znaki.

```
    function BinStr(Value: cardinal; Digits: byte): TString;
```

* `Concat` funkcja łączy dwa ciągi tekstowe w nowy ciąg znakowy.

```
    function Concat(a,b: string): string; assembler
    function Concat(a: string; b: char): string; assembler;
    function Concat(a: char; b: string): string; assembler;
    function Concat(a,b: char): string;
```

* `Blockread` `Blockwrite` procedura `BlockRead` wczytuje z pliku plik do zmiennej `Buf` nie więcej niż `Count` bajtów i umieszcza w zmiennej `Result` ilość rzeczywiście przeczytanych bajtów (która może być mniejsza od oczekiwanej np. ze względu na rzeczywistą długość pliku). Procedura `BlockWrite` działa tak samo, tylko zapisuje do pliku.

```
    procedure BlockRead(var f: file; var Buf; Count: word; var Result: word);
    procedure BlockWrite(var f: file; var Buf; Count: word; var Result: word);
```

* `Chr` funkcja zwraca znak `Char` o odpowiadającym kodzie **ATASCII** podanym w parametrze. Zamiennie z funkcją `Chr`, chcąc uzyskać odpowiedni znak możemy użyć jego kodu **ATASCII** poprzedzając go `#`.

```
    Chr(65); // Zwraca znak A
    Chr(90); // Zwraca znak Z
    Chr(32); // Zwraca znak spacji

    Writeln(#65);       // Znak A
    Writeln(#65#32#65); // Napisze 'A Z'
```

* `Cos` cosinus kąta (x w radianach).

```
    function Cos(x: real): real;
```

* `Close` procedura służąca do zamykania otwartego pliku dowolnego typu. Każdy plik otwarty przy pomocy `Reset` lub `Rewrite` powinno się zamknąć przy pomocy `Close`.

```
    procedure Close(var f: file);
```

* `Dec` procedura zmniejsza wartość parametru `X` o `1` lub wartość parametru `N`. Wartość parametru `X` może być typu `CHAR` `BYTE` `WORD` `CARDINAL`. Procedura `DEC` generuje optymalny kod, jest zalecana do używania w pętlach, zamiast operatora odejmowania `-`.

```
    procedure Dec(var X [, N: int]);

    dec(tmp);
    dec(tmp[2]);
```

* `DeleteFile` funkcja pozwala skasować plik z dysku o nazwie `FileName`, zwraca `TRUE` kiedy operacja powiodła się, `FALSE` w przypadku wystąpienia błędu (najczęściej z powodu zabezpieczenia przed zapisem lub błędnej nazwy pliku).

```
    function DeleteFile(FileName: string): Boolean;
```

* `DPeek` funkcja zwraca słowo spod adresu `A`.

```
    function DPeek(a: word): word;
```

* `DPoke` procedura zapisuje słowo `Value` pod adresem `A`.

```
    procedure DPoke(a: word; value: word);
```

* `Eof` Funkcja zwraca wartość logiczną True jeśli osiągnięty został koniec pliku.

```
    function Eof(var f: file): Boolean;
```

* `Exit` wywołanie procedury `Exit` powoduje natychmiastowe opuszczenie bloku programu, w którym to wywołanie nastąpiło. Można jej użyć do opuszczenia pętli, wyjścia z **procedury/funkcji** lub programu głównego.

* `Exp` funkcja podnosząca liczbę e (=2.71) do potęgi podanej przez argument.

```
    function Exp(x: real): real;
```

* `FilePos` funkcja zwraca aktualną pozycję pliku. Plik nie może być tekstowy i musi być otwarty (np. poleceniem `Reset`). Bity `0..15` zwróconej wartości to numer sektora dysku, bity `16..23` pozycja w sektorze `[0..255]`. Jest to odpowiednik instrukcji `NOTE`.

```
    function FilePos(var f: file): cardinal;
```

* `FileSize` funkcja zwraca długość pliku w bajtach (**Sparta DOS X**). Plik nie może być tekstowy i musi być otwarty (np. poleceniem `Reset`).

```
    function FileSize(var f: file): cardinal;
```

* `FillChar` procedura wypełnia bufor określony w parametrze `X` identycznymi znakami lub bajtami. Parametr `Value` musi określać dane, natomiast `Count` - ilość danych jakie zostaną przypisane do bufora.

```
    procedure FillChar(a: pointer; count: word; value: char);

    var
      Buffer : array[0..100] of Char;
    begin
      FillChar(Buffer, SizeOf(Buffer), 'A');
    end.
```

* `Frac` zwraca część ułamkową liczby x w postaci rzeczywistej.

```
    function Frac(x: real): real;
```
