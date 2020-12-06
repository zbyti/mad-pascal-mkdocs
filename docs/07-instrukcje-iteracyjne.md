# Instrukcje interacyjne

## [for to downto do](https://www.freepascal.org/docs-html/ref/refsu57.html)

    FOR zmienna := { wartość początkowa } TO { wartość końcowa } DO { instrukcje do wykonania }
    FOR zmienna := { wartość końcowa } DOWNTO { wartość początkowa } DO { instrukcje do wykonania }

Instrukcja ta służy do organizacji obliczeń, które będą wykonywane z góry określoną liczbę razy. Zmienna sterująca musi być identyfikatorem typu porządkowego, a oba wyrażenia powinny być zgodne w sensie przypisania z typem zmiennej sterującej. W czasie realizacji pętli `TO` zmiennej sterującej przypisywana jest następna wartość w danym typie, w pętli `DOWNTO` poprzednia. Zabroniona jest *ręczna* zmiana wartości zmiennej sterującej. W przypadku takiej próby **MP** nie zasygnalizuje błędu.

Kompilator dba o to aby nie wystąpiła pętla bez końca, dlatego można bez obaw stosować taką pętlę:

    for i:=0 to 255 do writeln(i);    // dla zmiennej I typu BYTE

## while do

    while { warunek } do { instrukcja do wykonania }

Konstrukcja ta służy do organizacji obliczeń, które będą wykonywane tak długo jak wyrażenie znajdujące się po słowie WHILE jest prawdą. Tak skonstruowana pętla może nie zostać wykonana ani razu.

    while BlitterBusy do;   // oczekiwanie na zakończenie działania blittera VBXE

Ograniczenia dla instrukcji WHILE:

    while i<=255 do inc(i); // pętla bez końca gdy zmienna I typu BYTE

## [repeat until](https://www.freepascal.org/docs-html/ref/refsu59.html)

    repeat
      { instrukcje do wykonania }
    until { warunek zakończenia }

Instrukcja ta wykonuje cyklicznie inne instrukcje zawarte pomiędzy słowami `REPEAT` i `UNTIL` do momentu gdy wyrażenie znajdujące się za słowem `UNTIL` nie przyjmie wartości **PRAWDA** (czyli `TRUE`).

Efekt zastosowania pętli `REPEAT` jest bardzo podobny do działania pętli `WHILE`. Pętla ta także może być wykonywana ogromną liczbę razy. Jedyna różnica polega na tym, że w pętli `REPEAT` warunek zakończenia sprawdzany jest dopiero po wykonaniu instrukcji. Oznacza to, że pętla `REPEAT` zawsze będzie wykonana co najmniej raz. Dopiero po tej iteracji program sprawdzi, czy można zakończyć działanie pętli. W przypadku pętli `WHILE` warunek jest sprawdzany bezpośrednio przed jej wykonaniem, co w rezultacie może spowodować, że taka pętla nigdy niezostanie wykonana.

    i:=0;
    repeat
      inc(i);
    until i=0;      // pętla wykona się 256 razy
