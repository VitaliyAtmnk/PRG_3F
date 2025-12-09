## Počítadlo kliknutí

**Cíl:** Seznámit se s `NumericUpDown` a `Label`.

-   Na formuláři:

    -   `NumericUpDown` – určuje, o kolik se má hodnota měnit (krok).

    -   `Label` – zobrazuje aktuální hodnotu.

    -   `Button` „Přičti“.

-   Po kliknutí na tlačítko:

    -   k aktuální hodnotě (třeba uložené v proměnné `int`) přičti číslo z `NumericUpDown.Value`

    -   zobraz výsledek v `Label`.

-   Nastav:

    -   `NumericUpDown.Minimum = 1`

    -   `NumericUpDown.Maximum = 100`


---

## Převod měny – jednoduchá kalkulačka

**Cíl:** Čtení hodnoty z NumericUpDown + výpočet.

-   Na formuláři:

    -   `Label` „Částka v CZK:“

    -   `NumericUpDown` pro zadání částky v Kč (může mít `DecimalPlaces = 2`)

    -   `Button` „Převést na EUR“

    -   `TextBox` jen pro čtení pro výsledek

-   Předpokládej pevný kurz, např. `1 EUR = 25 Kč`.

-   Po kliknutí:

    -   přečti částku z `NumericUpDown`

    -   vypočítej `EUR = CZK / 25m`

    -   zobraz v TextBoxu např. `12,34 EUR`.


---

## Objednávka pizzy (počty kusů)

**Cíl:** Práce s více NumericUpDown najednou.

-   Na formuláři:

    -   `Label` „Počet malých pizz“

    -   `NumericUpDown` (1–10)

    -   `Label` „Počet velkých pizz“

    -   `NumericUpDown` (1–10)

    -   `Button` „Spočítej cenu“

    -   `TextBox` (jen pro čtení) s výslednou cenou.

-   Ceny:

    -   malá pizza = 149 Kč

    -   velká pizza = 199 Kč

-   Po kliknutí:

    -   spočítej celkovou cenu:

        -   `celkem = pocetMalych * 149 + pocetVelkych * 199`

    -   výsledek zobraz jako text, např. `Celkem zaplatíte: 547 Kč`.


---

## Výpočet slevy v procentech

**Cíl:** DecimalPlaces, procenta, formátování.

-   Na formuláři:

    -   `Label` „Původní cena (Kč)“

    -   `NumericUpDown` pro cenu (např. `Minimum = 0`, `Maximum = 100000`, `DecimalPlaces = 2`)

    -   `Label` „Sleva (%)“

    -   `NumericUpDown` pro slevu (0–90, `Increment = 5`)

    -   `Button` „Spočítej slevu“

    -   `TextBox` pro „Nová cena“

-   Po kliknutí:

    -   spočítej slevu: `sleva = cena * (slevaProcent / 100)`

    -   `novaCena = cena - sleva`

    -   zobraz obě hodnoty (sleva + nová cena) buď v jednom TextBoxu na více řádků, nebo ve dvou.


---

##  Kalorie oběda

**Cíl:** Kombinace několika čísel a součet.

-   Na formuláři:

    -   3× řádek:

        -   `Label` (např. „Brambory (g)“, „Maso (g)“, „Omáčka (g)“)

        -   `NumericUpDown` pro gramáž (0–500, `Increment = 50`)

    -   `Button` „Spočítej kalorie“

    -   `TextBox` pro celkový výsledek.

-   Stanov „kalorické hodnoty“:

    -   brambory: 0,8 kcal / g

    -   maso: 2,0 kcal / g

    -   omáčka: 1,0 kcal / g

-   Po kliknutí:

    -   vypočti kalorie za každou složku + celkem

    -   zobraz třeba:

        -   „Brambory: 160 kcal  
            Maso: 300 kcal  
            Omáčka: 100 kcal  
            Celkem: 560 kcal“


---

## Nastavení budíku (čas v minutách)

**Cíl:** Práce s rozsahem a ověřením vstupu.

-   Na formuláři:

    -   `Label` „Za kolik minut se má spustit budík?“

    -   `NumericUpDown` (0–120, `Increment = 5`)

    -   `Button` „Nastavit budík“

    -   `Label` pro výstup.

-   Po kliknutí:

    -   pokud `Value == 0`, zobraz např. „Zadej prosím nenulový čas.“

    -   jinak zobraz třeba „Budík bude nastaven za X minut.“  
        (reálně nic nezvoní, jde jen o práci s hodnotou a podmínkou)


---

## Rozdělení účtu v restauraci

**Cíl:** Dva NumericUpDown + podmínky.

-   Na formuláři:

    -   `Label` „Celková částka (Kč)“

    -   `NumericUpDown` pro částku (0–5000, `DecimalPlaces = 2`)

    -   `Label` „Počet lidí“

    -   `NumericUpDown` (1–20)

    -   `Button` „Spočítej na osobu“

    -   `TextBox` (jen pro čtení) s výsledkem.

-   Po kliknutí:

    -   vypočti `naOsobu = celkem / pocetLidi`

    -   vypiš např. „Každý zaplatí: 123,45 Kč“.


---

##  Odpočet (bez časovače, jen logika)

**Cíl:** Jednoduchá „simulace“ bez Timeru – uživatel ručně odpočítává.

-   Na formuláři:

    -   `NumericUpDown` – „Startovní hodnota odpočtu“ (1–100)

    -   `Label` – zobrazení aktuálního stavu

    -   `Button` „Reset“

    -   `Button` „Odečti 1“

-   Po kliknutí na „Reset“:

    -   nastav proměnnou `aktualni` na `NumericUpDown.Value`

    -   zobraz ji v `Label`.

-   Po kliknutí na „Odečti 1“:

    -   pokud `aktualni > 0`, sniž o 1

    -   pokud `aktualni == 0`, zobraz „Hotovo!“ (nebo nedovol dál odečítat).


---

## Hodnocení testu (počet bodů ➜ známka)

**Cíl:** Podmínky `if` + NumericUpDown jako bodové skóre.

-   Na formuláři:

    -   `Label` „Počet bodů (0–100)“

    -   `NumericUpDown` (0–100)

    -   `Button` „Urči známku“

    -   `Label` / `TextBox` pro výsledek.

-   Po kliknutí:

    -   podle počtu bodů určete známku:

        -   90–100 → 1

        -   75–89 → 2

        -   60–74 → 3

        -   40–59 → 4

        -   0–39 → 5

    -   vypiš text typu „Za 82 bodů máš známku 2.“


---

##  Mini „konfigurátor PC“

**Cíl:** Více NumericUpDown + součet + textové shrnutí.

-   Na formuláři:

    -   `Label` + `NumericUpDown` pro:

        -   „Počet monitorů“ (0–3)

        -   „Počet disků“ (0–4)

        -   „Počet RAM modulů“ (1–4)

    -   `Button` „Spočítej cenu“

    -   `TextBox` (multiline, `ReadOnly = true`) pro shrnutí.

-   Ceník (např.):

    -   monitor: 3000 Kč

    -   disk: 1500 Kč

    -   RAM modul: 800 Kč

-   Po kliknutí:

    -   spočítej cenu za jednotlivé položky + celkem

    -   do TextBoxu napiš něco jako:

        -   ## „Monitory (2×): 6000 Kč
            Disky (1×): 1500 Kč  
            RAM (2×): 1600 Kč

            Celkem: 9100 Kč“
            
