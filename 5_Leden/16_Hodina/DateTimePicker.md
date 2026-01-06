# **WinForms: DateTimePicker – základní informace**

### **Co je DateTimePicker?**

`DateTimePicker` je ovládací prvek pro výběr **data** (a případně i **času**) ve Windows Forms. Standardně vypadá jako textové pole s šipkou, po kliknutí se otevře rozbalovací kalendář. Ovládací prvek sám hlídá validitu a umožňuje omezit rozsah na `MinDate`/`MaxDate`. 

> Oficiální dokumentace → `DateTimePicker` (Microsoft Learn) [Microsoft Learn+1](https://learn.microsoft.com/cs-cz/dotnet/api/system.windows.forms.datetimepicker?view=windowsdesktop-8.0)

---

## **Nejdůležitější vlastnosti (Properties) DateTimePicker**

### **Value**

Aktuálně vybrané datum/čas.

-   Typ: `DateTime`

-   Při změně vyvolá událost `ValueChanged`

-   Pozor: hodnota musí být v rozsahu `MinDate`–`MaxDate` (jinak přiřazení může skončit výjimkou / ořezem dle situace)


---

### **Format**

Určuje, jak se datum/čas **zobrazuje**.

-   Typ: `DateTimePickerFormat`

-   Hodnoty typicky: `Long`, `Short`, `Time`, `Custom`

-   Formátování respektuje regionální nastavení OS

-   Aby fungoval `CustomFormat`, musí být `Format = Custom`

---

### **CustomFormat**

Vlastní formátovací řetězec (pouze když `Format = Custom`).

-   Typ: `string`

-   Příklad: `dd.MM.yyyy HH:mm`

-   Textové literály je potřeba uzavřít do apostrofů (např. `"MMMM dd 'at' t:mm tt"`) [Pro zájemce](https://learn.microsoft.com/en-us/dotnet/api/system.windows.forms.datetimepicker.customformat?view=windowsdesktop-10.0)


---

### **MinDate**

Nejmenší povolené datum/čas, které lze vybrat.

-   Typ: `DateTime`

-   Užitečné pro validaci „od–do“ (např. datum narození, plánování) 

---

### **MaxDate**

Největší povolené datum/čas, které lze vybrat.

-   Typ: `DateTime`

-   Společně s `MinDate` omezuje výběr v kalendáři 

---

### **ShowUpDown**

Přepne ovládací prvek z rozbalovacího kalendáře na „spinner“ (šipky nahoru/dolů).

-   Typ: `bool`

-   `true` → **neotevírá se kalendář**, měníš hodnotu šipkami po jednotlivých částech (den/měsíc/rok/čas)

-   Typické použití pro čas: `Format = Time` + `ShowUpDown = true`

---

### **ShowCheckBox**

Zobrazí vlevo **checkbox**, kterým uživatel určí, zda je datum „zapnuté“.

-   Typ: `bool`

-   Hodí se pro „volitelné datum“ (např. datum ukončení, datum odeslání…)

-   Skutečný stav pak čteš přes `Checked` (viz níže)


(Checkbox je součástí DateTimePickeru – běžná praxe je kombinovat `ShowCheckBox` + `Checked`.)

---

### **Checked**

Platí hlavně, když je `ShowCheckBox = true`.

-   Typ: `bool`

-   `true` → hodnota se bere jako zadaná

-   `false` → datum je „nezvolené“ (v aplikaci často mapované na `null`)


---

### **DropDownAlign**

Zarovnání rozbalovacího kalendáře vůči ovládacímu prvku.

-   Typicky: `Left` / `Right`

-   Užitečné, když je DateTimePicker blízko pravého okraje okna (aby kalendář „neutíkal“ mimo)


---

### **Text**

Textová reprezentace vybraného data/času podle formátu.

-   Typ: `string`

-   Praktické pro rychlé zobrazení/diagnostiku, ale pro logiku používej radši `Value`

---

## **Nejdůležitější události (Events)**

### **ValueChanged**

Vyvolá se při změně `Value` (uživatel i program).

-   Typické použití: okamžitá reakce UI, přepočty, validace rozsahu.


---

### **DropDown / CloseUp**

-   `DropDown` – když se otevře kalendář

-   `CloseUp` – když se kalendář zavře


Hodí se pro logování, doplnění nápovědy, dočasné zvýraznění, apod.