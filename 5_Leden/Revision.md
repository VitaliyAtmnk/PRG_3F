# Opakování na test

- možnost získat **3** známky před testem

- za každý vypracovaný úkol ze zadání lze získat jednu známku s váhou 2

- test bude mít váhu 6

## Informace k testu

- test proběhne 20.1.2026 na půlených hodinách
- na vypracování bude cca 45 minut (2-3 minuty na odevzdání na moodle)

### Povolené pomůcky

- poznámky z hodin
- oficiální dokumentace microsoftu
- příklady z hodin (<span style="color:red">Vypracovány Vámi (jedincem)</span>.)

### Přísně zakázáno

- generativní AI
- opisování od spolužáků
- cizí řešení

### Obsah

- Základní prvky winforms
    - Label, Button, NumericUpDown, TextBox, DateTimePicker

- Test se skládá ze 3 částí
    1. Vytvoření prvků a nastavení vlastností
    2. Doplnění základní logiky prvků (jednoduchý kód)
    3. Vytvoření složitější funkcionality (těžší kód + vytvoření a použití dalšího prvku)

- Známkování:

| Známka | Požadavky                                                  |
|--------|------------------------------------------------------------|
| 5      | Prázdný projekt, nebo existuje jen pár ovládácích pvků     | 
| 4-     | Je splněna jen 1. polovina 1. části                        | 
| 4      | Je splněna pouze 1. část                                   | 
| 3-     | Není splněna 3. část a jsou větší nedostatky ve 2. části   | 
| 3      | Není splněna 3. část a jsou střední nedostatky ve 2. části | 
| 2-     | Není splněna 3. část a jsou drobné nedostatky ve 2. části  | 
| 2      | Je splněna 1. a 2. část                                    | 
| 1-     | Téměř vše funguje, drobné nedostatky                       | 
| 1      | Vše funguje dle požadavků                                  | 

## Příklady:

### Příklad 1

#### 1) Prvky a vlastnosti

Vytvoř:

- `nudPrice` (NumericUpDown): Min 0, Max třeba 100000, DecimalPlaces 2, Increment 10

- `nudTip` (NumericUpDown): Min 0, Max 100, Value 10

- `nudPeople` (NumericUpDown): Min 1, Max 20, Value 2

- Button `btnCacl` („Spočítat“)

- Labely pro popisky a výsledky: `lblTipAmount`, `lblTotal`, `lblPerPerson`

#### 2) Základní logika

Po kliknutí na `btnCalc`:

- vypočti **tip částku**, **celkem**, **na osobu**

- zobraz to do labelů (formátuj na 2 desetinná místa)

#### 3) Složitější funkcionalita + další prvek

- Přidej Button `btnSave` („Uložit do historie“)

- Přidej TextBox `txtHistory` (Multiline = true, ReadOnly = true)

- Při ukládání přidej řádek do `txtHistory` ve stylu:  
  `12.01.2026 14:30 | Cena 520 | Tip 10% | Celkem 572 | Na osobu 286`

![img.png](img.png)

---

### Příklad 2:

#### 1) Prvky a vlastnosti

Vytvoř:

- `dtpNarozeni` (DateTimePicker) – Format Short

- Button `btnVypocitej` („Vypočítat“)

- Labely: `lblVekRoky`, `lblVekDny`, `lblDoNarozenin`

- TextBox `txtJmeno` (volitelné) + Label „Jméno:“

#### 2) Základní logika

Po kliknutí:

- Spočti věk v **letech** (správně i když narozeniny letos ještě nebyly)

- Spočti, kolik dní uplynulo od narození (zhruba `DateTime.Now - dtpNarozeni.Value`)

#### 3) Složitější funkcionalita + další prvek

- Vytvoř **Button `btnDnes`** („Nastav narození na dnešek“).

- Doplň „dny do příštích narozenin“:

    - pokud už letos narozeniny byly, počítej do příštího roku

---

### Příklad 3: „Převodník jednotek (tlačítka místo comboboxu) + poslední převody“

#### 1) Prvky a vlastnosti

Vytvoř:

- `nudVstup` (NumericUpDown): Min -100000, Max 100000, DecimalPlaces 2

- TextBox `txtVystup` (ReadOnly = true)

- Buttony:

    - `btnCtoF` („°C → °F“)

    - `btnFtoC` („°F → °C“)

    - `btnKmToMi` („km → míle“)

    - `btnMiToKm` („míle → km“)

- TextBox `txtLog` (Multiline + ReadOnly) pro historii převodů

#### 2) Základní logika

Každé tlačítko vezme hodnotu z `nudVstup`, provede převod a dá výsledek do `txtVystup`.

#### 3) Složitější funkcionalita + další prvek

- Vytvoř Label `lblCounter` (např. „Záznamů v logu: X“) a po každém převodu ho aktualizuj.

- Udržuj v `txtLog`  záznamy převodů.

- {input_val} → {calculated_val}
- 0°C → 32°F // jednotky je potřeba zjistít podle tlačítka

---