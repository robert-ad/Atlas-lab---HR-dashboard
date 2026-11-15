# Atlas Labs — HR dashboard

Interaktywny raport HR na fikcyjnych danych Atlas Labs: **1470 pracowników i 6709 ocen okresowych**. Projekt łączy modelowanie danych, 35 miar DAX i dynamiczne zabezpieczenia RLS z jasnym, miętowym interfejsem w języku polskim.

## Strony raportu

### 1. Przegląd HR
U góry znajdują się karty aktywnych pracowników, udziału odejść, średniego stażu i nadgodzin. Poniżej widać porównanie działów, wykres pierścieniowy statusu odejścia, strukturę wieku oraz tabelę wyników.

### 2. Zatrudnienia
Karty pokazują zatrudnienia w wybranym okresie i rok wcześniej, liczbę osób ze statusem odejścia oraz aktywnych pracowników bez awansu od co najmniej pięciu lat. Wykresy prezentują trend zatrudnień i udział odejść w działach. Filtr roku dotyczy daty zatrudnienia.

### 3. Oceny i bąbelki
Wykres bąbelkowy porównuje stanowiska: oś X pokazuje średni staż ocenionych osób, oś Y ich satysfakcję, a wielkość bąbla liczbę ocenionych pracowników. Obok znajdują się trend satysfakcji i rozkład ocen kierownika, a pod wykresem tabela wartości. Filtr roku dotyczy daty oceny.

### 4. Zespoły
Struktura wykształcenia i płci, porównanie działów oraz szczegóły pracowników. Filtry pozwalają zawęzić analizę do działu, stanowiska i płci.

## Model danych

**8 tabel i 6 aktywnych relacji 1:* z filtrowaniem jednokierunkowym.** Model płatka śniegu obejmuje:

- `Działy` i `Wykształcenie` → `Pracownicy` → `Oceny`.
- `Kalendarz`, `Skala ocen` i `Skala satysfakcji` → `Oceny`.
- Oddzielną tabelę `Uprawnienia`, odczytywaną przez regułę RLS.

## Dynamiczny RLS

Rola `DostepDynamiczny` wykorzystuje `USERPRINCIPALNAME()` oraz mapowanie loginu do działów. Scenariusz zakłada dostęp kierownika do jednego działu, dyrektora do dwóch, a HR do całej firmy. Brak przypisania oznacza brak danych. Przykładowe loginy i scenariusze testowe opisano w dokumentacji projektu.

## Technologie i DAX

**Power BI Desktop, Power Query, DAX, CSV.**

35 miar obejmuje m.in. aktywnych pracowników, udział odejść, zatrudnienia rok wcześniej, średni staż, nadgodziny, satysfakcję, ocenę kierownika i lukę samooceny.

Zastosowane techniki: `CALCULATE`, `KEEPFILTERS`, `DIVIDE`, `DATEADD`, `TREATAS`, `AVERAGEX`, `DISTINCTCOUNT`, `REMOVEFILTERS`, `CONCATENATEX` i `USERPRINCIPALNAME`.

Pełne definicje: [miary DAX](dokumentacja/miary.dax). Relacje, reguły dostępu i zakres weryfikacji: [opis techniczny](dokumentacja/opis-techniczny.md).

## Dane źródłowe
[DataCamp — Case Study: HR Analytics in Power BI](https://www.datacamp.com/courses/case-study-hr-analytics-in-power-bi). Dane dotyczą fikcyjnej firmy. Model, miary, RLS i wygląd raportu opracowano w ramach tego projektu.

[DataCamp — Case Study: HR Analytics in Power BI](https://www.datacamp.com/courses/case-study-hr-analytics-in-power-bi). Dane dotyczą fikcyjnej firmy. Model, miary, RLS i wygląd raportu opracowano w ramach tego projektu.
