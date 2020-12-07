#

W katalogu `LIB` **Mad-Pascala** znajdują się potrzebne do kompilacji podstawowe moduły `UNIT`, takie jak `SYSTEM` `CRT` `GRAPH` `SYSUTILS` `MATH` `DOS`. W programie wybierane są przez instrukcję `USES`, np.:

    uses crt, sysutils;

Moduł `SYSTEM` jest domyślnie dopisywany do listy `USES` i kompilowany jako pierwszy.

## [SYSTEM](http://mads.atari8.info/library/doc/system.html)

### Constants

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

### Types

#### `TPoint`

```
    TPoint = record x,y: SmallInt end;
```

Definicja współrzędnych (x,y).

---

#### `TRect`

```
    TRect = record left, top, right, bottom: smallint end;
```

Definicja położenia i rozmiaru czworokąta o parametrach (left, top) - lewy górny narożnik, (right, bottom) - prawy dolny narożnik.

---

#### `TString`

```
    TString = string[32];
```

Definicja krótkiego ciągu znakowego wykorzystywanego do przekazywania nazw plików itp.

---

### Variables

#### `IOResult`

```
    IOResult: byte;
```

Zmienna przechowuje ostatni błąd operacji `I/O`. [Kody błędów I/O](http://atariki.krap.pl/index.php/Kody_statusowe_Atari_OS).

---

#### `ScreenWidth`

```
    ScreenWidth: word = 40
```

Zmienna przechowująca aktualną szerokość ekranu. Domyślnie jest to wartość 40 dla ekranu edytora.

```
    ScreenHeight: word = 24;
```

---

#### `ScreenHeight`

Zmienna przechowująća aktualną wysokość ekranu. Domyślnie jest to wartość 24 dla ekranu edytora.

### Procedures and functions

```pascal
Abs                ArcTan              Assign             BinStr            Concat
Blockread          Blockwrite          Chr                Cos               Close
Dec                DeleteFile          DPeek              DPoke             Eof
Exit               Exp                 FilePos            FileSize          FillChar
Frac               GetIntVec           Halt               Hi                HexStr
Inc                Ln                  Lo                 LowerCase         Move
OctStr             Odd                 Ord                ParamCount        ParamStr
Pause              Peek                Point              PointsEqual       Poke
Pred               Random              ReadConfig         ReadSecto         Rect
RenameFile         Reset               Rewrite            Round             Seek
SetLength          SetIntVec           Sin                Succ              Space
SizeOf             Str                 StringOfChar       Sqr               Sqrt
Trunc              UpCase              Val                WriteSector
```

#### `Abs`

```
    function Abs(x: real): real;
    function Abs(x: integer): integer;
```

Funkcja obliczająca wartość bezwzględną podanej liczby (ang. **Absolute value**). Wartość bezwzględna liczby nieujemnej to ta sama liczba, a liczby ujemnej - liczba do niej przeciwna. Funkcja w przypadku podania jej argumentu całkowitego zwraca wynik również typu całkowitego.

---

#### `ArcTan`

```
    function ArcTan(x: real): real;
```

Funkcja (arcus tangens) zwraca wartość kąta, którego tangens wynosi `x`.

---

#### `Assign`

```
    procedure Assign(var F:File; FileName:string)
```

Procedura przypisuje zmiennej plikowej `F` plik o nazwie `FileName`. Aby móc odwoływać się do jakiegoś pliku, zawsze należy najpierw użyć procedury `Assign`. Przy dalszych operacjach pliki są identyfikowane przy pomocy zmiennej plikowej, a nie nazwy.

---

#### `BinStr`

```
    function BinStr(Value: cardinal; Digits: byte): TString;
```

Funkcja zwraca ciąg znakowy z reprezentacją binarną wartości `Value`. `Digits` określa długość ciągu, który maksymalnie może liczyć 32 znaki.

---

#### `Concat`

```
    function Concat(a,b: string): string; assembler
    function Concat(a: string; b: char): string; assembler;
    function Concat(a: char; b: string): string; assembler;
    function Concat(a,b: char): string;
```

Funkcja łączy dwa ciągi tekstowe w nowy ciąg znakowy.

---

#### `Blockread`

```
    procedure BlockRead(var f: file; var Buf; Count: word; var Result: word);
```

Procedura wczytuje z pliku plik do zmiennej `Buf` nie więcej niż `Count` bajtów i umieszcza w zmiennej `Result` ilość rzeczywiście przeczytanych bajtów (która może być mniejsza od oczekiwanej np. ze względu na rzeczywistą długość pliku).

---

#### `Blockwrite`

```
    procedure BlockWrite(var f: file; var Buf; Count: word; var Result: word);
```

Procedura zapisuje do pliku ze zmiennej `Buf` nie więcej niż `Count` bajtów.

---

#### `Chr`

```
    Chr(65); // Zwraca znak A
    Chr(90); // Zwraca znak Z
    Chr(32); // Zwraca znak spacji

    Writeln(#65);       // Znak A
    Writeln(#65#32#65); // Napisze 'A Z'
```

Funkcja zwraca znak `Char` o odpowiadającym kodzie **ATASCII** podanym w parametrze. Zamiennie z funkcją `Chr`, chcąc uzyskać odpowiedni znak możemy użyć jego kodu **ATASCII** poprzedzając go `#`.

---

#### `Cos`

```
    function Cos(x: real): real;
```

Cosinus kąta, `x` w radianach.

---

#### `Close`

```
    procedure Close(var f: file);
```

Procedura służąca do zamykania otwartego pliku dowolnego typu. Każdy plik otwarty przy pomocy `Reset` lub `Rewrite` powinno się zamknąć przy pomocy `Close`.

---

#### `Dec`

```
    procedure Dec(var X [, N: int]);
```

Procedura zmniejsza wartość parametru `X` o `1` lub wartość parametru `N`. Wartość parametru `X` może być typu `CHAR` `BYTE` `WORD` `CARDINAL`. Procedura `DEC` generuje optymalny kod, jest zalecana do używania w pętlach, zamiast operatora odejmowania `-`.

```
    dec(tmp);
    dec(tmp[2]);
```

---

#### `DeleteFile`

```
    function DeleteFile(FileName: string): Boolean;
```

Funkcja pozwala skasować plik z dysku o nazwie `FileName`, zwraca `TRUE` kiedy operacja powiodła się, `FALSE` w przypadku wystąpienia błędu (najczęściej z powodu zabezpieczenia przed zapisem lub błędnej nazwy pliku).

---

#### `DPeek`

```
    function DPeek(a: word): word;
```

Funkcja zwraca słowo spod adresu `a`.

---

#### `DPoke`

```
    procedure DPoke(a: word; value: word);
```

Procedura zapisuje słowo `value` pod adresem `a`.

---

#### `Eof`

```
    function Eof(var f: file): Boolean;
```

Funkcja zwraca wartość logiczną `TRUE` jeśli osiągnięty został koniec pliku.

---

#### `Exit`

Wywołanie procedury `Exit` powoduje natychmiastowe opuszczenie bloku programu, w którym to wywołanie nastąpiło. Można jej użyć do opuszczenia pętli, wyjścia z **procedury/funkcji** lub programu głównego.

---

#### `Exp`

```
    function Exp(x: real): real;
```

Funkcja podnosząca liczbę e (=2.71) do potęgi podanej przez argument `x`.

---

#### `FilePos`

```
    function FilePos(var f: file): cardinal;
```

Funkcja zwraca aktualną pozycję pliku. Plik nie może być tekstowy i musi być otwarty (np. poleceniem `Reset`). Bity `0..15` zwróconej wartości to numer sektora dysku, bity `16..23` pozycja w sektorze `[0..255]`. Jest to odpowiednik instrukcji `NOTE`.

---

#### `FileSize`

```
    function FileSize(var f: file): cardinal;
```

Funkcja zwraca długość pliku w bajtach (**Sparta DOS X**). Plik nie może być tekstowy i musi być otwarty (np. poleceniem `Reset`).

---

#### `FillChar`

```
    procedure FillChar(x: pointer; count: word; value: char);
```

Procedura wypełnia bufor określony w parametrze `X` identycznymi znakami lub bajtami. Parametr `value` musi określać dane, natomiast `count` - ilość danych jakie zostaną przypisane do bufora.

```
    var
      Buffer : array[0..100] of Char;
    begin
      FillChar(Buffer, SizeOf(Buffer), 'A');
    end.
```

---

#### `Frac`

```
    function Frac(x: real): real;
```

Zwraca część ułamkową liczby `x` w postaci rzeczywistej.

---

#### `GetIntVec`

```
    procedure GetIntVec(intno: byte; var vector: pointer);
```

Procedura odczytuje adres wektora przerwań wg. kodu **INTNO**. Obecnie dopuszczalnymi kodami są: `iDLI` przerwanie DLI, `iVBL` przerwanie VBL.

---

#### `Halt`

```
    procedure halt;
```

Wywołanie powoduje natychmiastowe wyjście z programu. Można (opcjonalnie) podać kod błędu, w przypadku **MP** jest on ignorowany.


---

#### `Hi`

```
    function Hi(x): byte
```

Funkcja zwracająca starszy bajt parametru `x`.

---

#### `HexStr`

```
    function HexStr(Value: cardinal; Digits: byte): TString;
```

Funkcja zwraca ciąg znakowy z reprezentacją heksadecymalną wartości `Value`. `Digits` określa długość ciągu, który maksymalnie może liczyć 32 znaki.

---

#### ` Inc`

```
    Inc procedure Inc(var X [, N: int]);
```

Procedura zwiększa wartość parametru `X` o `1` lub wartość parametru `N`. Wartość parametru `X` może być typu `CHAR` `BYTE` `WORD` `CARDINAL`. Procedura `INC` generuje optymalny kod, jest zalecana do używania w pętlach, zamiast operatora dodawania `+`.

```
    inc(tmp);
    inc(tmp[2]);
```

---

#### `Int`

```
    function Int(x: real): real;
```

Funkcja zwraca część całkowitą argumentu będącego liczbą rzeczywistą.

---

#### `Ln`

```
    function Ln(x: real): real;
```

Funkcja licząca logarytm naturalny (o podstawie e) z podanej liczby. Argument funkcji musi być **dodatni**!

---

#### `Lo`

```
    function Lo(x): byte;
```

Funkcja zwracająca młodszy bajt parametru `X`.

---

#### `LowerCase`

```
    function LowerCase(a: char): char;
```

Funkcja zmieniająca znaki 'A'..'Z' na odpowiednie małe znaki 'a'..'z'.

---

#### `Move`

```
    procedure Move(source, dest: pointer; count: word);
```

Procedura służy do kopiowania danych ze źródła, parametr `Source`, do bufora oznaczonego jako przeznaczenie, parametr `Dest`. Ilość kopiowanych danych określa parametr `Count`.

---

#### `OctStr`

```
    function OctStr(Value: cardinal; Digits: byte): TString;
```

Funkcja zwraca ciąg znakowy z reprezentacją ósemkową wartości `Value`. `Digits` określa długość ciągu, który maksymalnie może liczyć 32 znaki.

---

#### `Odd`

```
    function Odd(x: cardinal): Boolean;
    function Odd(x: integer): Boolean;
```

Funkcja zwraca wartość `True` jeżeli liczba określona w parametrze `X` jest nieparzysta, `False` jeżeli jest parzysta.

---

#### `Ord`

```
    function Ord(X);
```

Funkcja ta działa odwrotnie do `Chr`. Z podanego znaku jako parametr zwraca nam jego kod w **ATASCII**.

```
    Ord('A'); // Zwraca 65
    Ord('Z'); // Zwraca 90
    Ord(' '); // Zwraca 32
```

---

#### `ParamCount`

```
    function ParamCount: byte;
```

Funkcja zwraca ilość dostępnych argumentów (**Sparta Dos X**, **BWDos**), tzn. maksymalny indeks dla procedury `ParamStr`. `ParamCount` określa ilość parametrów przekazanych do programu z linii poleceń.

---

#### `ParamStr`

```
    function ParamStr(Index: byte): TString;
```

Funkcja zwraca parametry programu (**Sparta Dos X**, **BWDos**). `Index` to numer parametru, czyli ciągu znaków oddzielonego spacją.

Jeżeli uruchomimy program `TEST.EXE` w taki sposób:


```
    TEST.EXE parametr1 parametr2 parametr3
```

To aby uzyskać `parametr3` należy podać `Index=3`, zaś aby uzyskać `parametr1` należy `Index=1`. `Index=0` to specjalny argument, wtedy funkcja zwraca napęd z którego został uruchomiony programu, np. `D1:`.

---

#### `Pause`

```
    procedure Pause;
    procedure Pause(n: word);
```

Procedura zatrzymuje działanie programu na `N * 1.50` sek.

---

#### `Peek`

```
    function Peek(a: word): byte;
```

Funkcja zwraca bajt spod adresu `a`.

---

#### `Point`

```
    function Point(AX, AY: smallint): TPoint;
```

Funkcja na podstawie parametrów `AX` oraz `AY` tworzony jest rekord typu `TPoint`.

---

#### `PointsEqual`

```
    function PointsEqual(const P1, P2: TPoint): Boolean;
```

Funkcja sprawdza czy wartości współrzędnych określone w parametrach `P1` oraz `P2` są sobie równe. W takim wypadku funkcja zwraca wartość `True`.

---

#### `Poke`

```
    procedure Poke(a: word; value: byte);
```

Procedura zapisuje bajt `value` pod adresem `a`.

---

#### `Pred`

```
    function Pred(X: TOrdinal): TOrdinal;
```

Poprzednik elementu `X`.

---

#### `Random`

```
    function Random: Real; assembler;
```

Funkcja zwraca losową wartość z przedziału `<0 .. 1>`.

```
    function Random(range: byte): byte; assembler;
```

Funkcja zwraca losową wartość z przedziału `<0 .. range-1>`, w przypadku Range=0 zwraca wartość losową z przedziału `<0 .. 255 >`.

```
    function Random(range: smallint): smallint;
```

Funkcja zwraca losową wartość z przedziału `<0 .. range-1>`.

---

#### `ReadConfig`

```
    function ReadConfig(devnum: byte): cardinal;
```

Odczyt statusu stacji `devnum`. Wynikiem są cztery bajty `DVSTAT ($02EA..$02ED)`.

```
    Byte 0 ($02ea):
    Bit 0:Indicates the last command frame had an error.
    Bit 1:Checksum, indicates that there was a checksum error in the last command or data frame
    Bit 2:Indicates that the last operation by the drive was in error.
    Bit 3:Indicates a write protected diskette. 1=Write protect
    Bit 4:Indicates the drive motor is on. 1=motor on
    Bit 5:A one indicates MFM format (double density)
    Bit 6:Not used
    Bit 7:Indicates Density and a Half if 1

    Byte 1 ($02eb):
    Bit 0:FDC Busy should always be a 1
    Bit 1:FDC Data Request should always be 1
    Bit 2:FDC Lost data should always be 1
    Bit 3:FDC CRC error, a 0 indicates the last sector read had a CRC error
    Bit 4:FDC Record not found, a 0 indicates last sector not found
    Bit 5:FDC record type, a 0 indicates deleted data mark
    Bit 6:FDC write protect, indicates write protected disk
    Bit 7:FDC door is open, 0 indicates door is open

    Byte 2 ($2ec):
    Timeout value for doing a format.

    Byte 3 ($2ed):
    not used, should be zero
```

---

#### `ReadSector`

```
    procedure ReadSector(devnum: byte; sector: word; var buf);
```

Procedura odczytuje sektora `sector` dyskietki w stacji dysków `devnum` i zapisanie go w buforze `buf`.

---

#### `Rect`

```
    function Rect(ALeft, ATop, ARight, ABottom: smallint): TRect;
```

Funckja na podstawie parametrów tworzy rekord typu `TRect`.

---

#### `RenameFile`

```
    function RenameFile(OldName, NewName: string): Boolean;
```
Funkcja pozwala zmienić nazwę pliku `OldName` na nową nazwę `NewName`, zwraca `TRUE` kiedy operacja powiodła się, `FALSE` w przypadku wystąpienia błędu (najczęściej z powodu zabezpieczenia przed zapisem lub błędnej nazwy pliku).


```
    RenameFile('D:OLDNAME.TMP', 'NEWNAME.TMP');
```

---

#### `Reset`


```
    procedure Reset(var f: file; l: Word);
```

Procedura otwiera istniejący plik z nazwą przekazaną do `F` poleceniem `Assign`. Opcjonalnie możemy podać rozmiar rekordu w bajtach `L`, domyślnie jest to wartość 128.

---

#### `Rewrite`

```
    procedure Rewrite(var f: file; l: Word);
```

Procedura tworzy i otwiera nowy plik. `f` jest nazwą przekazaną za pomocą polecenia `Assign`. Opcjonalnie możemy podać rozmiar rekordu w bajtach `l`, domyślnie jest to wartość 128.

---

#### `Round`

```
    function Round(x: real): integer;
```

Funkcja dokonuje zaokrąglenia podanej liczby rzeczywistej do najbliższej liczby całkowitej.

---

#### `Seek`

```
    procedure Seek(var f: file; N: cardinal);
```

Procedura ustawia pozycję w pliku na `N`. `N` powinno być wartością zwróconą przez `FilePos`. Jest to odpowiednik instrukcji `POINT`.

---

#### `SetLength`

```
    procedure SetLength(var S: string; Len: byte);
```

Procedura ustawia długość ciągu `S` na `LEN`.

---

#### `SetIntVec`

```
    procedure SetIntVec(intno: Byte; vector: pointer);
```

Procedura ustawia adres wektora przerwań wg. kodu **INTNO**. Obecnie dopuszczalnymi kodami są: `iDLI` przerwanie DLI, `iVBL` przerwanie VBL.

---

#### `Sin`

```
    function Sin(x: real): real;
```

Sinus kąta. `x` w radianach.

---

#### `Succ`

```
    function Succ(X: TOrdinal): TOrdinal;
```

Następnik elementu `X`.

---

#### `Space`

```
    function Space(Len: Byte): ^char;
```

Funkcja generuje nowy ciąg znakowy o długości `Len` wypełniony znakami spacji.

---

#### `SizeOf`

```
    function SizeOf(X: AnyType): byte;
```

Funkcja zwraca rozmiar podanej zmiennej (lub typu) w bajtach.

---

#### `Str`

```
    procedure Str(var X: TNumericType; var S: string);
```

Procedura zamienia liczbę `X` na łańcuch znaków `S`.

---

#### `StringOfChar`

```
    procedure StringOfChar(ch: Char; len: byte): ^char;
```

Funkcja generuje nowy ciąg znakowy o długości `len` wypełniony znakami `ch`.

---

#### `Sqr`

```
    function Sqr(x: real): real;
    function Sqr(x: integer): integer;
```

Funkcja obliczająca kwadrat podanej liczby (ang. **Square**).

---

#### `Sqrt`

```
    function Sqrt(x: real): real;
    function Sqrt(x: single): single;
    function Sqrt(x: integer): single;
```

Funkcja obliczająca pierwiastek kwadratowy podanej liczby (ang. **Square root**).

---

#### `Trunc`

```
    function Trunc(x: real): integer;
```

Funkcja zwraca część całkowitą liczby rzeczywistej w postaci liczby całkowitej.

---

#### `UpCase`

```
    function UpCase(a: char): char;
```

Funkcja zmieniająca znaki `'a'..'z'` na odpowiednie duże znaki `'A'..'Z'`.

---

#### `Val`

```
    procedure Val(const S: string; var V; var Code: Byte);
```

Procedura przekształca ciąg znaków `S` na liczbę `V`. Code przyjmie wartość `0` jeśli nie było błędnych znaków, w przeciwnym wypadku przyjmie numer znaku który spowodował błąd konwersji.

---

#### `WriteSector`

```
    procedure WriteSector(devnum: byte; sector: word; var buf);
```

Procedura zapisuje sektora `sector` dyskietki w stacji `devnum` na podstawie bufora `buf`.

## [CRT](http://mads.atari8.info/library/doc/crt.html)

### Constants

```
CN_START_SELECT_OPTION  = 0;
CN_SELECT_OPTION        = 1;
CN_START_OPTION         = 2;
CN_OPTION               = 3;
CN_START_SELECT         = 4;
CN_SELECT               = 5;
CN_START                = 6;
CN_NONE                 = 7;
```

### Variables

#### `Consol`

```
    Consol: byte absolute $d01f
```

Zmienna zwraca kod naciśniętego klawisza/klawiszy konsoli.

---

#### `TextAttr`

```
    TextAttr: byte = 0
```

Zmienna przechowuje wartość jaka jest dodawana do każdego wyświetlanego znaku, np. `TextAttr = $80` spowoduje że znaki będą wyświetlane w inwersie.

---

#### `WhereX`

```
    WhereX: byte absolute $54;
```

Zmienna przechowuje aktualną poziomą pozycję kursora.

---

#### `WhereY`

```
    WhereY: byte absolute $55;
```

Zmienna przechowuje aktualną pionową pozycję kursora.

### Procedures and functions

```pascal
ClrEol             ClrScr              CursorOff          CursorOn          Delay
DelLine            GotoXY              InsLine            Keypressed        NoSound
ReadKey            Sound               TextBackground     TextColor
```

#### `ClrEol`

```
    procedure ClrEol;
```

Procedura czyści wiersz od aktualnej pozycji kursora do prawej strony krawędzi ekranu. Pozycja kursora nie ulega zmianie.

---

#### `ClrScr`

```
    procedure ClrScr;
```

Procedura czyści ekran edytora, wykonuje kod znaku `CH_CLR`.

---

#### `CursorOff`

```
    procedure CursorOff;
```

Procedura wyłącza kursor.

---

#### `CursorOn`

```
    procedure CursorOn;
```

Procedura włącza kursor.

---

#### `Delay`

```
    procedure Delay(MS: Word);
```

Procedura czeka zadaną ilość milisekund `MS`. W przybliżeniu `Delay(1000)` generuje opóźnienie jednej sekundy.

---

#### `DelLine`

```
    procedure DelLine;
```

Procedura kasuje wiersz na aktualnej pozycji kursora, wykonuje kod znaku `CH_DELLINE`.

---

#### `GotoXY`

```
    procedure GotoXY(x, y: byte);
```

Procedura ustawia nową pozycję kursora.

---

#### `InsLine`

```
    procedure InsLine;
```

Procedura wstawia pusty wiersz na aktualnej pozycji kursora, wykonuje kod znaku `CH_INSLINE`.

---

#### `Keypressed`

```
    function Keypressed: Boolean;
```

Funkcja zwraca `TRUE` gdy został naciśnięty jakiś klawisz klawiatury, w przeciwnym razie zwraca `FALSE`.

---

#### `NoSound`

```
    procedure NoSound;
```

Procedura wycisza kanały obu **POKEY-i** `$D200` `$D210)`.

---

#### `ReadKey`

```
    function ReadKey: char;
```

Funkcja zwraca kod naciśniętego klawisza klawiatury.

---

#### `Sound`

```
    procedure Sound(Chan,Freq,Dist,Vol: byte);
```

Procedura odtwarza dźwięk na kanale **POKEY-a** `CHAN (0..3, 4..7)`, o częstotliwości `FREQ (0..255)`, filtrach `DIST (0..7)`, głośności `VOL (0..15)`.

---

#### `TextBackground`

```
    procedure TextBackground(a: byte);
```

Procedura ustawia nowy kolor tła znaków (działa najlepiej z włączonym **VBXE**).

---

#### `TextColor`

```
    procedure TextColor(a: byte);
```

Procedura ustawia nowy kolor znaków (działa najlepiej z włączonym **VBXE**).

## [GRAPH](http://mads.atari8.info/library/doc/graph.html)

### Constants

```
{ graphic drivers }
D1bit   = 11;
D2bit   = 12;
D4bit   = 13;
D6bit   = 14;       // 64 colors Half-brite mode - Amiga
D8bit   = 15;
D12bit  = 16;       // 4096 color modes HAM mode - Amiga

m640x480 = 8 + 16;

{ error codes }
grOK             = 0;
grNoInitGraph    = -1;
grNotDetected    = -2;
grFileNotFound   = -3;
grInvalidDriver  = -4;
grNoLoadMem      = -5;
grNoScanMem      = -6;
grNoFloodMem     = -7;
grFontNotFound   = -8;
grNoFontMem      = -9;
grInvalidMode    = -10;
grError          = -11;
grIOerror        = -12;
grInvalidFont    = -13;
grInvalidFontNum = -14;
grInvalidVersion = -18;
```

### Variables

#### `GraphResult`

```
    GraphResult : byte
```

### Procedures and functions

```pascal
Bar                Bar3D               Circle             ClipLine          Ellipse
FillEllipse        FillRect            FloodFill          GetColor          GetMaxX
GetMaxY            GetPixel            GetX               GetY              InitGraph
Line               LineTo              MoveRel            MoveTo            PutPixel
Rectangle          SetBkColor          SetClipRect        SetColor          SetColorMapEntry
SetColorMapDimensions
```

#### `Bar`

```
    procedure Bar(x1, y1, x2, y2: Smallint);
```

Prostokąt, np. dla wykresów słupkowych.

---

#### `Bar3D`

```
    procedure Bar3D(x1, y1, x2, y2: smallint; depth: word; top: boolean);
```

Słupek dla wykresów trójwymiarowych.

---

#### `Circle`

```
    procedure Circle(x0,y0,radius: word);
```

Okrąg.

---

#### `ClipLine`

```
    procedure ClipLine(x1, y1, x2, y2: smallint);
```

---

#### `Ellipse`

```
    procedure Ellipse(x0, y0, a, b: word);
```

Elipsa.

---

#### `FillEllipse`

```
    procedure FillEllipse(x0, y0, a, b: word);
```

Elipsa wypełniona wewnątrz.

---

#### `FillRect`

```
    procedure FillRect(Rect: TRect);
```

Prostokąt wypełniony wewnątrz.

---

#### `FloodFill`

```
    procedure FloodFill(x, y: smallint; color: byte);
```

Wypełnienie zamkniętego obszaru ekranu.

---

#### `GetColor`

```
    function GetColor: byte; assembler;
```

Podaj bieżący kolor rysowania.

---

#### `GetMaxX`

```
    function GetMaxX: word;
```

Podaj najwyższą wartość współrzędnej X na ekranie.

---

#### `GetMaxY`

```
    function GetMaxY: word;
```

Podaj najwyższą wartość współrzędnej Y na ekranie.

---

#### `GetPixel`

```
    function GetPixel(x,y: smallint): byte;
```

Podaj kolor danego punktu na ekranie.

---

#### `GetX`

```
    function GetX: smallint;
```

Podaj bieżącą współrzędną X kursora graficznego.

---

#### `GetY`

```
    function GetY: smallint;
```

Podaj bieżącą współrzędną Y kursora graficznego.

---

#### `InitGraph`

```
    procedure InitGraph(mode: byte);
    procedure InitGraph(driver, mode: byte; pth: TString);
```

Zainicjuj tryb graficzny.

---

#### `Line`

```
    procedure Line(x0, y0, x1, y1: smallint);
```

Linia prosta.

---

#### `LineTo`

```
    procedure LineTo(x, y: smallint);
```

Linia od bieżącej pozycji kursora do wskazanego punktu.

---

#### `MoveRel`

```
    procedure MoveRel(Dx, Dy: smallint);
```

Przesuń kursor graficzny.

---

#### `MoveTo`

```
    procedure MoveTo(x, y: smallint);
```

Przesuń kursor graficzny do wskazanego punktu.

---

#### `PutPixel`

```
    procedure PutPixel(x,y: smallint);
    procedure PutPixel(x,y: smallint; color: byte);
```

Zapal punkt na ekranie.

---

#### `Rectangle`

```
    procedure Rectangle(x1, y1, x2, y2: smallint);
    procedure Rectangle(Rect: TRect);
```

Prostokąt.

---

#### `SetBkColor`

```
    procedure SetBkColor(color: byte);
```

Ustaw kolor tła.

---

#### `SetClipRect`

```
    procedure SetClipRect(x0,y0,x1,y1: smallint);
    procedure SetClipRect(Rect: TRect);
```

---

#### `SetColor`

```
    procedure SetColor(color: byte);
```

Ustaw kolor pisaka.

---

#### `SetColorMapEntry`

```
    procedure SetColorMapEntry;
    procedure SetColorMapEntry(a,b,c: byte);
```

---

#### `SetColorMapDimensions`

```
    procedure SetColorMapDimensions(w,h: byte);
```

## [SYSUTILS](http://mads.atari8.info/library/doc/strutils.html)

### Constants

```
faReadOnly  = $01;
faHidden    = $02;
faSysFile   = $04;
faVolumeID  = $08;
faDirectory = $10;
faArchive   = $20;
faAnyFile   = $3f;
```

### Types

#### `TSearchRec`

```
    TSearchRec = record
            Attr: Byte;
            Name: TString;
            FindHandle: Pointer;
             end;
```

### Procedures and functions

```pascal
AnsiUpperCase      Beep                Click              DeleteFile        ExtractFileExt
FileExists         FindFirst           FindNext           FindClose         GetTickCount
IntToHex           IntToStr            RenameFile         StrToFloat        StrToInt
```

#### `AnsiUpperCase`

```
    function AnsiUpperCase(const a: string): string;
```

Funkcja konwertuje znaki z łańcucha `a` na wielkie.

---

#### `Beep`

```
    procedure Beep;
```

Sygnał brzęczka (buzzer).

---

#### `Click`

```
    procedure Click;
```

Sygnał klawiatury.

---

#### `DeleteFile`

```
    function DeleteFile(var FileName: TString): Boolean;
```

Funkcja kasuje plik określony w parametrze `FileName`, zwraca `TRUE` gdy operacja się powiodła.

---

#### `ExtractFileExt`

```
    function ExtractFileExt(const FileName: string): TString;
```

Na podstawie nazwy pliku lub pełnej ścieżki do pliku określonej w parametrze `FileName`, funkcja zwraca rozszerzenie (poprzedzone kropką - np. `.txt`).

---

#### `FileExists`

```
    function FileExists(const FileName: string): Boolean;
```

Funkcja sprawdza czy plik określony w parametrze `FileName`, istnieje `True` czy też nie `False`.

---

#### `FindFirst`

```
    function FindFirst(const FileMask: TString; Attributes: Byte; var SearchResult: TSearchRec): byte;
```

Funkcja wyszukuje pliki pasujące do wzorca `FileMask` i posiadające atrybuty określone w `Attributes`. Jeśli zostały znalezione pliki pasujące do szablonu to pierwszy z nich jest zwracany w zmiennej `SerchResult`.

---

#### `FindNext`

```
    function FindNext(var f: TSearchRec): byte;
```

Funkcja przechodzi do następnego rekordu znalezionego wcześniej przy pomocy `FindFirst`. W parametrze musi zostać przekazane wskazanie na rekord, który wcześniej został użyty w funkcji `FindFirst`.

---

#### `FindClose`

```
    procedure FindClose(var f: TSearchRec);
```

Procedura zwalnia zasoby (pamięć) zaalokowaną przez funkcję `FindFirst`. Procedura ta powinna być wywoływana za każdym razem po zakończeniu procesu wyszukiwania.

---

#### `GetTickCount`

```
    function GetTickCount: cardinal;
```

GetTickCount zwraca 24-bitowy licznik czasu `(PEEK(RTCLOK+2) + PEEK(RTCLOK+1)*256 + PEEK(RTCLOK)*65536)`. Jest to przydatne do pomiaru czasu.

---

#### `IntToHex`

```
    function IntToHex(Value: cardinal; Digits: byte): TString;
```

Funkcja konwertuje wartość liczbową na jej odpowiednik łańcuchowy w systemie szesnastkowym.

---

#### `IntToStr`

```
    function IntToStr(a: integer): ^char;
```

Funkcja służy do konwersji liczby całkowitej podanej w parametrze do postaci łańcuchowej.

---

#### `RenameFile`

```
    function RenameFile(var OldName,NewName: TString): Boolean;
```

Funkcja próbuje zmienić nazwę pliku określonego w parametrze `OldName` na `NewName`. Jeżeli operacja się powiedzie, funkcja zwróci wartość `True` w przeciwnym wypadku `False`. Może się zdarzyć, że funkcja nie będzie mogła zmienić nazwy (np. gdy aplikacja nie ma prawa do tego) - wówczas funkcja zwróci `False`.

---

#### `StrToFloat`

```
    function StrToFloat(var s: TString): real;
```

Funkcja konwertuje łańcuch do postaci zmiennoprzenkowej typu `Real`.

---

#### `StrToInt`

```
    function StrToInt(const S: char): byte;
    function StrToInt (const S: TString): integer;
```

Funkcja służy do konwersji tekstu zapisanego w zmiennej S na liczbę całkowitą - o ile to możliwe.