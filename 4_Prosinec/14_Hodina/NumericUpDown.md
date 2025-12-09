# **WinForms: NumericUpDown – základní informace**

### **Co je NumericUpDown?**

`NumericUpDown` je vstupní ovládací prvek, který umožňuje uživateli zadávat **číselnou hodnotu** – buď přímým psaním, nebo pomocí **šipek nahoru/dolů** (tzv. „spin box“ / „up-down“).  
Hodnota je vždy číslo v daném rozsahu a mění se po zadaném kroku.

> Oficiální dokumentace → [NumericUpDown](https://learn.microsoft.com/cs-cz/dotnet/api/system.windows.forms.numericupdown?view=windowsdesktop-8.0&utm_source=chatgpt.com) [Microsoft Learn](https://learn.microsoft.com/cs-cz/dotnet/api/system.windows.forms.numericupdown?view=windowsdesktop-8.0&utm_source=chatgpt.com)

---

## **Nejdůležitější vlastnosti (Properties) NumericUpDown**

### **Value**

Aktuální číselná hodnota ovládacího prvku.

-   Typ: `decimal`

-   Musí být mezi `Minimum` a `Maximum`

-   Při změně vyvolá událost `ValueChanged`

---

### **Minimum**

Nejmenší povolená hodnota.

-   Typ: `decimal`

-   Výchozí hodnota je obvykle `0`

-   Při nastavení `Value` mimo rozsah se hodnota ořízne na `Minimum` nebo `Maximum`

---

### **Maximum**

Největší povolená hodnota.

-   Typ: `decimal`

-   Výchozí hodnota je obvykle `100`

-   Mělo by být ≥ `Minimum`


---

### **Increment**

O kolik se hodnota změní při jednom kliknutí na šipku nahoru/dolů.

-   Typ: `decimal`

-   Např. `Increment = 0.5m;` → hodnoty: 0.0, 0.5, 1.0, 1.5, …


---

### **DecimalPlaces**

Počet desetinných míst, které se zobrazují.

-   Typ: `int`

-   Neovlivňuje přesnost `Value`, jen formát zobrazení 

---

### **ThousandsSeparator**

Zobrazení oddělovače tisíců (podle národní konfigurace systému).

-   Typ: `bool`

-   `true` → 1 000,00

-   `false` → 1000,00 

---

### **Hexadecimal**

Zobrazení hodnoty v šestnáctkové soustavě.

-   Typ: `bool`

-   `true` → hodnota se zobrazí jako hex (např. 15 → `F`)

-   Použitelné hlavně pro technické nástroje (např. adresy, bity) 

---

### **ReadOnly**

Určuje, zda může uživatel hodnotu psát ručně z klávesnice.

-   `true` → lze měnit jen šipkami nahoru/dolů (text nejde přepsat)

-   `false` → lze psát i přímo číslo do pole 

---

### **InterceptArrowKeys**

Zda NumericUpDown „pohlcuje“ šipky nahoru/dolů z klávesnice.

-   `true` → šipky mění hodnotu v NumericUpDown

-   `false` → šipky se předají formuláři / jiným ovládacím prvkům 

---

### **TextAlign**

Zarovnání textu (čísla) uvnitř pole.

-   Hodnoty: `Left`, `Right`, `Center`

-   Typicky se používá `Right` (zarovnání čísel vpravo)

---

### **UpDownAlign**

Zarovnání tlačítek (šipek) vůči textovému poli.

-   Hodnoty: `Left`, `Right`

-   Umožňuje mít šipky vlevo nebo vpravo od čísla 

---

### **BorderStyle**

Styl rámečku kolem ovládacího prvku.

-   `None`

-   `FixedSingle`

-   `Fixed3D` (výchozí) 

---

### **Enabled**

-   `true` → uživatel může měnit hodnotu

-   `false` → ovládací prvek je „zašedlý“ a nelze s ním pracovat


---

### **Visible**

Určuje, zda je NumericUpDown viditelný na formuláři.

---

### **Location (Left, Top)**

Pozice na formuláři:

-   `Left` → vzdálenost od levého okraje formuláře

-   `Top` → vzdálenost od horního okraje formuláře


---

### **Size (Width, Height)**

Velikost ovládacího prvku:

-   `Width` → šířka (důležitá pro délku čísla)

-   `Height` → výška (většinou se příliš nemění)
    
