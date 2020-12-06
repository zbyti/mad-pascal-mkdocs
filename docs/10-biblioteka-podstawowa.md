# Biblioteka podstawowa

W katalogu `LIB` **Mad-Pascala** znajdują się potrzebne do kompilacji podstawowe moduły `unit`, takie jak `SYSTEM` `CRT` `GRAPH` `SYSUTILS` `MATH` `DOS`. W programie wybierane są przez instrukcję `USES`, np.:

    uses crt, sysutils;

Moduł `SYSTEM` jest domyślnie dopisywany do listy `USES` i kompilowany jako pierwszy.

## SYSTEM

**Constants**

```
PI               = 3.1406     // write(pi)
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

* `IOResult` zmienna przechowuje ostatni błąd operacji `I/O`. [Kody błędów I/O](http://atariki.krap.pl/index.php/Kody_statusowe_Atari_OS).

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

* `GetIntVec` procedura odczytuje adres wektora przerwań wg. kodu **INTNO**. Obecnie dopuszczalnymi kodami są: `iDLI - przerwanie DLI` i `iVBL - przerwanie VBL`.

```
    procedure GetIntVec(intno: Byte; var vector: pointer);
```

* `Halt` wywołanie powoduje natychmiastowe wyjście z programu. Można (opcjonalnie) podać kod błędu, w przypadku **MP** jest on ignorowany.

```
    procedure halt;
```

* `Hi` funkcja zwracająca starszy bajt parametru `X`.

```
    function Hi(x): byte
```

* `HexStr` funkcja zwraca ciąg znakowy z reprezentacją heksadecymalną wartości `Value`. `Digits` określa długość ciągu, który maksymalnie może liczyć 32 znaki.

```
    function HexStr(Value: cardinal; Digits: byte): TString;
```

* `Inc` procedura zwiększa wartość parametru `X` o `1` lub wartość parametru `N`. Wartość parametru `X` może być typu `CHAR` `BYTE` `WORD` `CARDINAL`. Procedura `INC` generuje optymalny kod, jest zalecana do używania w pętlach, zamiast operatora dodawania `+`.

```
    Inc procedure Inc(var X [, N: int]);

    inc(tmp);
    inc(tmp[2]);
```

* `Int` funkcja zwraca część całkowitą argumentu będącego liczbą rzeczywistą.

```
    function Int(x: real): real;
```

* `Ln` funkcja licząca logarytm naturalny (o podstawie e) z podanej liczby. Argument funkcji musi być **dodatni**!

```
    function Ln(x: real): real;
```

* `Lo` funkcja zwracająca młodszy bajt parametru `X`.

```
    function Lo(x): byte;
```

* `LowerCase` funkcja zmieniająca znaki 'A'..'Z' na odpowiednie małe znaki 'a'..'z'.

```
    function LowerCase(a: char): char;
```

* `Move` Procedura służy do kopiowania danych ze źródła, parametr `Source`, do bufora oznaczonego jako przeznaczenie, parametr `Dest`. Ilość kopiowanych danych określa parametr `Count`.

```
    procedure Move(source, dest: pointer; count: word);
```

* `OctStr` funkcja zwraca ciąg znakowy z reprezentacją ósemkową wartości `Value`. `Digits` określa długość ciągu, który maksymalnie może liczyć 32 znaki.

```
    function OctStr(Value: cardinal; Digits: byte): TString;
```

* `Odd` funkcja zwraca wartość `True` jeżeli liczba określona w parametrze `X` jest nieparzysta, `False` jeżeli jest parzysta.

```
    function Odd(x: cardinal): Boolean;
    function Odd(x: integer): Boolean;
```

* `Ord` funkcja ta działa odwrotnie do `Chr`. Z podanego znaku jako parametr zwraca nam jego kod w **ATASCII**.

```
    function Ord(X);

    Ord('A'); // Zwraca 65
    Ord('Z'); // Zwraca 90
    Ord(' '); // Zwraca 32
```

* `ParamCount` funkcja zwraca ilość dostępnych argumentów (**Sparta Dos X**, **BWDos**), tzn. maksymalny indeks dla procedury `ParamStr`. `ParamCount` określa ilość parametrów przekazanych do programu z linii poleceń.

```
    function ParamCount: byte;
```


* `ParamStr` funkcja zwraca parametry programu (**Sparta Dos X**, **BWDos**). `Index` to numer parametru, czyli ciągu znaków oddzielonego spacją.

```
    function ParamStr(Index: byte): TString;
```

Jeżeli uruchomimy program `TEST.EXE` w taki sposób:


```
    TEST.EXE parametr1 parametr2 parametr3
```

To aby uzyskać `parametr3` należy podać `Index=3`, zaś aby uzyskać `parametr1` należy `Index=1`. `Index=0` to specjalny argument, wtedy funkcja zwraca napęd z którego został uruchomiony programu, np. `D1:`.


* `Pause` zatrzymuje działanie programu na `N * 1.50` sek.

```
    procedure Pause;
    procedure Pause(n: word);
```

* `Peek` funkcja zwraca bajt spod adresu `A`.

```
    function Peek(a: word): byte;
```

* `Point` na podstawie parametrów `AX` oraz `AY` tworzony jest rekord typu `TPoint`.


```
    function Point(AX, AY: smallint): TPoint;
```

* `PointsEqual` funkcja sprawdza czy wartości współrzędnych określone w parametrach `P1` oraz `P2` są sobie równe. W takim wypadku funkcja zwraca wartość `True`.

```
    function PointsEqual(const P1, P2: TPoint): Boolean;
```

* `Poke` procedura zapisuje bajt `Value` pod adresem `A`.

```
    procedure Poke(a: word; value: byte);
```

* `Pred` poprzednik elementu `X`.

```
    function Pred(X: TOrdinal): TOrdinal;
```

* `Random`

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

* `ReadConfig` odczyt statusu stacji `DEVNUM`. Wynikiem są cztery bajty `DVSTAT ($02EA..$02ED)`.

```
    function ReadConfig(devnum: byte): cardinal;

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

* `ReadSector` odczyt sektora `SECTOR` dyskietki w stacji dysków `DEVNUM` i zapisanie go w buforze `BUF`.

```
    procedure ReadSector(devnum: byte; sector: word; var buf);
```

* `Rect` na podstawie parametrów tworzony jest rekord typu `TRect`.

```
    function Rect(ALeft, ATop, ARight, ABottom: smallint): TRect;
```

* `RenameFile` funkcja pozwala zmienić nazwę pliku `OldName` na nową nazwę `NewName`, zwraca `TRUE` kiedy operacja powiodła się, `FALSE` w przypadku wystąpienia błędu (najczęściej z powodu zabezpieczenia przed zapisem lub błędnej nazwy pliku).

```
    function RenameFile(OldName, NewName: string): Boolean;

    RenameFile('D:OLDNAME.TMP', 'NEWNAME.TMP');
```

* `Reset` otwiera istniejący plik z nazwą przekazaną do `F` poleceniem `Assign`. Opcjonalnie możemy podać rozmiar rekordu w bajtach `L`, domyślnie jest to wartość 128.

```
    procedure Reset(var f: file; l: Word);
```

* `Rewrite` tworzy i otwiera nowy plik. `F` jest nazwą przekazaną za pomocą polecenia `Assign`. Opcjonalnie możemy podać rozmiar rekordu w bajtach `L`, domyślnie jest to wartość 128.

```
    procedure Rewrite(var f: file; l: Word);
```

* `Round` funkcja dokonuje zaokrąglenia podanej liczby rzeczywistej do najbliższej liczby całkowitej.

```
    function Round(x: real): integer;
```

* `Seek` ustawia pozycję w pliku na `N`. `N` powinno być wartością zwróconą przez `FilePos`. Jest to odpowiednik instrukcji `POINT`.

```
    procedure Seek(var f: file; N: cardinal);
```

* `SetLength` ustawia długość ciągu `S` na `LEN`.

```
    procedure SetLength(var S: string; Len: byte);
```

* `SetIntVec` procedura ustawia adres wektora przerwań wg. kodu **INTNO**. Obecnie dopuszczalnymi kodami są: `iDLI - przerwanie DLI` oraz `iVBL - przerwanie VBL`.

```
    procedure SetIntVec(intno: Byte; vector: pointer);
```

* `Sin` sinus kąta (x w radianach).

```
    function Sin(x: real): real;
```

* `Succ` następnik elementu `X`.

```
    function Succ(X: TOrdinal): TOrdinal;
```

* `Space` funkcja generuje nowy ciąg znakowy o długości `LEN` wypełniony znakami spacji.

```
    function Space(Len: Byte): ^char;
```

* `SizeOf` funkcja zwraca rozmiar podanej zmiennej (lub typu) w bajtach.

```
    function SizeOf(X: AnyType): byte;
```

* `Str` instrukcja zamienia liczbę `X` na łańcuch znaków `S`.

```
    procedure Str(var X: TNumericType; var S: string);
```

* `StringOfChar` funkcja generuje nowy ciąg znakowy o długości `LEN` wypełniony znakami `CH`.

```
    procedure StringOfChar(ch: Char; len: byte): ^char;
```

* `Sqr` funkcja obliczająca kwadrat podanej liczby (ang. **Square**).

```
    function Sqr(x: real): real;
    function Sqr(x: integer): integer;
```

* `Sqrt` funkcja obliczająca pierwiastek kwadratowy podanej liczby (ang. *Square root*).

```
    function Sqrt(x: real): real;
    function Sqrt(x: single): single;
    function Sqrt(x: integer): single;
```

* `Trunc` funkcja zwraca część całkowitą liczby rzeczywistej w postaci liczby całkowitej.

```
    function Trunc(x: real): integer;
```

* `UpCase` funkcja zmieniająca znaki `'a'..'z'` na odpowiednie duże znaki `'A'..'Z'`.

```
    function UpCase(a: char): char;
```

* `Val` procedura przekształca ciąg znaków `S` na liczbę `V`. Code przyjmie wartość `0` jeśli nie było błędnych znaków, w przeciwnym wypadku przyjmie numer znaku który spowodował błąd konwersji.

```
    procedure Val(const S: string; var V; var Code: Byte);
```

* `WriteSector` zapis sektora `SECTOR` dyskietki w stacji `DEVNUM` na podstawie bufora `BUF`.

```
    procedure WriteSector(devnum: byte; sector: word; var buf);
```