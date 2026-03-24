# Test Winforms

Povolené zdroje
- [PRG_3F](https://github.com/VitaliyAtmnk/PRG_3F/)
- [Microsoft_Winforms](https://learn.microsoft.com/en-us/dotnet/desktop/winforms/)

## Odevzdání:

- Email: atamanjuk@infis.cz
- Předmět: 3F_Test_WF_A{Číslo skupiny (1/2)} // Příklad 3F_Test_WF_A1 
- Název projektu: {Prijmeni}\_Test\_{Zadani} // Příklad Atamanjuk_Test_B
- Poslat projekt jako zip - {Prijmeni}.zip // Příklad Atamanjuk.zip

### Známkování

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


## Zadání A: „Nákupní košík (sleva + DPH) + historie objednávek“

### 1) Prvky a vlastnosti

Vytvořte:

* `nudPrice` (NumericUpDown): Min 0, Max 100000, DecimalPlaces 2, Increment 1
* `nudQty` (NumericUpDown): Min 1, Max 1000, Value 1
* `nudDiscount` (NumericUpDown): Min 0, Max 80, Value 10 (procenta)
* `nudVat` (NumericUpDown): Min 0, Max 30, Value 21 (procenta)
* Button `btnCalc` („Spočítat“)

Labely pro výsledky:

* `lblSubtotal` (mezisoučet bez slevy)
* `lblAfterDiscount` (po slevě, bez DPH)
* `lblTotalWithVat` (celkem s DPH)

### 2) Základní logika

Po kliknutí na `btnCalc`:

* `subtotal = price * qty`
* `afterDiscount = subtotal * (1 - discount/100)`
* `total = afterDiscount * (1 + vat/100)`
* vše zobrazte do labelů a formátujte na **2 desetinná místa**

> format string ${cislo:F2}

### 3) Složitější funkcionalita

Přidejte:

* Button `btnAddToHistory` („Uložit objednávku“)
* TextBox `txtHistory` (Multiline = true, ReadOnly = true, ScrollBars = Vertical)
* Label `lblOrdersCount` („Počet objednávek: 0“)

Po kliknutí na `btnAddToHistory`:

* do `txtHistory` přidejte řádek ve stylu:
  `19.01.2026 14:30 | Cena 199,90 | Ks 3 | Sleva 10% | DPH 21% | Celkem 653,67`
* aktualizujte `lblOrdersCount` (počet uložených objednávek)

---

## Zadání B: „Rezervace učebny (od–do) + kontrola kolizí a seznam rezervací“

### 1) Prvky a vlastnosti

Vytvořte:

* `dtpFrom` (DateTimePicker): Format = Custom, CustomFormat = `dd.MM.yyyy HH:mm`, ShowUpDown = true
* `dtpTo` (DateTimePicker): Format = Custom, CustomFormat = `dd.MM.yyyy HH:mm`, ShowUpDown = true
* `txtTitle` (TextBox) + Label „Název/účel:“
* Button `btnCheck` („Zkontrolovat“)
* Button `btnAdd` („Přidat rezervaci“)

Labely:

* `lblDuration` („Délka: …“)
* `lblStatus` (např. „OK“ / „Chyba: …“)

### 2) Základní logika

Po kliknutí na `btnCheck`:

* ověřte, že `dtpTo.Value > dtpFrom.Value`

  * pokud ne, vypište do `lblStatus` chybu a nastavte délku na 0
* spočítejte délku rezervace a zobrazte ji do `lblDuration`

  * např. `Délka: 1 h 30 min`

### 3) Složitější funkcionalita

Přidejte:

* TextBox `txtReservations` (Multiline = true, ReadOnly = true, ScrollBars = Vertical) jako seznam rezervací
* Label `lblReservationsCount` („Rezervací: 0“)
* Button `btnFillNowPlusHour` („Teď + 1 hod“) – nastaví From = nyní a To = From + 1 hodina

Funkce `btnAdd`:

* nejdříve proveďte stejné ověření jako v `btnCheck`
* následně zkontrolujte **kolizi** s existujícími rezervacemi

  * kolize nastane, pokud se nový interval překrývá s existujícím (např. `newFrom < oldTo && newTo > oldFrom`)
* pokud kolize existuje: vypište do `lblStatus` „Nelze přidat – koliduje s existující rezervací“ a nepřidávejte
* pokud je vše v pořádku: přidejte do `txtReservations` řádek ve stylu:
  `19.01.2026 10:00–11:30 | Konzultace | 90 min`
* aktualizujte `lblReservationsCount`

---
