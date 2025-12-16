## Úkol: „Vánoční seznam dárků“

Vytvoř aplikaci, která umožní uživateli přidávat dárky do seznamu, počítat cenu a na konci vypsat shrnutí pro Ježíška.

### Rozložení formuláře (doporučení)

**Labely:**

-   „Název dárku:“

-   „Cena za kus (Kč):“

-   „Počet kusů:“

-   „Seznam dárků:“

-   „Celkem položek: 0“

-   „Celková cena: 0 Kč“


**TextBoxy:**

-   `txtNazev` (název dárku)


-   `txtSeznam` (multiline, ReadOnly = true) – sem budeš přidávat řádky se seznamem


**NumericUpDown:**

-   `numCena` (cena za kus)

-   `numPocet` (min 1, max třeba 99)


**Buttony:**

-   `btnPridat` (Přidat dárek)

-   `btnSmazatVse` (Vymazat seznam)

-   `btnShrnuti` (Odeslat Ježíškovi / Shrnutí)


---

## Funkčnost

### 1) Přidání dárku

Po kliknutí na **Přidat dárek**:

-   Zkontroluj, že `txtNazev` není prázdný.

-   Spočítej **mezisoučet**: `cena * počet`.

-   Přidej do `txtSeznam` nový řádek ve formátu např.:

    -   `Plyšový sob – 3 ks × 199 Kč = 597 Kč`

-   Aktualizuj Labely:

    -   **Celkem položek** (součet kusů všech dárků)

    -   **Celková cena** (součet mezisoučtů)


Po přidání můžeš vyčistit `txtNazev`, `numCena` a vrátit `numPocet` na 1.

---

### 2) Vymazání seznamu

**Vymazat seznam**:


-   vymaž `txtSeznam`

-   nastav součty na 0

-   aktualizuj labely


---

### 3) Shrnutí „Ježíškovi“

**Shrnutí / Odeslat Ježíškovi**:

-   Pokud je seznam prázdný → MessageBox: „Nemáš žádné dárky v seznamu.“

-   Jinak MessageBox s textem třeba:

    -   „Hotovo! Připraveno X dárků za Y Kč. Veselé Vánoce!“


---

## Bonus (pokud zbude čas)

-   Přidej „vánoční pravidlo“: pokud **celková cena > 5000 Kč**, zobraz varování: „Pozor, Ježíšek bude potřebovat větší sáně (a vánoční prémie)!“
    
-   Pokud uživatel zadá cenu 0 → ber to jako „dárek vyrobený doma“ a do seznamu přidej text „(ruční výroba)“.
    
