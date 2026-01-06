## 1) Omezení data: „Termín odevzdání“

**Prvky:** `DateTimePicker dtpDeadline`, `Label lblInfo`, `Button btnSetToday`

**Zadání:**  
Vytvoř formulář pro výběr termínu odevzdání s těmito pravidly:

-   Uživatel může vybrat datum **nejdřív od dneška** (minimální datum = dnes).

-   Uživatel může vybrat datum **nejpozději 30 dní dopředu** (maximální datum = dnes + 30).

-   V `lblInfo` se vždy zobrazuje:  
    `Vybráno: dd.MM.yyyy (zbývá X dní)`

-   Tlačítko `btnSetToday` nastaví termín na dnešek.

---

## 2) Rozdíl dat: „Od–Do + validace“

**Prvky:** `DateTimePicker dtpFrom`, `DateTimePicker dtpTo`, `Label lblResult`, `Button btnCount`

**Zadání:**  
Uživatel vybere datum „Od“ a „Do“. Po kliknutí na `btnCount`:

-   Pokud je `Do < Od`, vypiš do `lblResult`:  
    `Chyba: Datum Do nesmí být menší než Od.`

-   Jinak vypiš:

    -   `Počet dní: X`

    -   `Počet týdnů a dnů: Y týdnů a Z dnů`

    -   `Je to pracovní období?` → ANO/NE (ANO, pokud je rozdíl aspoň 5 dní)


**Bonus:**

-   Automaticky nastav `dtpTo.MinDate = dtpFrom.Value` (aby uživatel nemohl vybrat „Do“ před „Od“).

---

## 3) Datum + čas (hod/min/sek): „Stopky do budoucna“

**Prvky:**  
`DateTimePicker dtpStart` (datum+čas), `NumericUpDown nudH`, `nudM`, `nudS`, `Button btnCalculate`, `Label lblOut`

**Zadání:**  
Uživatel nastaví **startovní datum a čas** a k tomu zadá, o kolik se má čas posunout:

-   `dtpStart` musí umožnit zadat **datum i čas včetně sekund** (např. formát `dd.MM.yyyy HH:mm:ss`).

-   `nudH` = hodiny (0–23), `nudM` = minuty (0–59), `nudS` = sekundy (0–59).

-   Po kliknutí na `btnCalculate`:

    1.  Spočítej `cílový okamžik = dtpStart + zadaný posun`

    2.  Vypiš do `lblOut`:

        -   `Start: dd.MM.yyyy HH:mm:ss`

        -   `Cíl: dd.MM.yyyy HH:mm:ss`

        -   `Rozdíl: HH:mm:ss` (celkový rozdíl jako časový úsek)


**Bonus:**

-   Pokud cílový okamžik vyjde na další den (nebo více), vypiš i:  
    `Přesah do dalších dnů: N`