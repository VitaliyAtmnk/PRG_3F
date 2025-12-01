# **WinForms: TextBox – základní informace**

### **Co je TextBox?**

`TextBox` je vstupní ovládací prvek, který umožňuje uživateli zadávat, upravovat nebo zobrazovat text.  
Podporuje více režimů – jedn řádkový vstup, víceřádkový text, hesla a další.

> Oficiální dokumentace → [TextBox](https://learn.microsoft.com/cs-cz/dotnet/api/system.windows.forms.textbox?view=windowsdesktop-8.0)

---

## **Nejdůležitější vlastnosti (Properties) TextBoxu**

### **Text**

Aktuální text uložený v TextBoxu (to, co uživatel píše).

### **Multiline**

-   `true` → umožňuje více řádků, TextBox se dá zvětšit na výšku

-   `false` → pouze jeden řádek


### **PasswordChar**

Znak, kterým se maskuje text (např. `*` nebo `•`) – používá se pro hesla.

### **UseSystemPasswordChar**

-   `true` → použije výchozí znak systému pro hesla

-   Nahrazuje potřebu ručně nastavovat `PasswordChar`.


### **ReadOnly**

-   `true` → uživatel nemůže měnit text, může ho ale kopírovat

-   `false` → běžné chování


### **ScrollBars**

Typ posuvníků (pouze pokud `Multiline = true`):

-   `None`

-   `Horizontal`

-   `Vertical`

-   `Both`


### **MaxLength**

Maximální počet znaků, které lze do TextBoxu zapsat.

### **CharacterCasing**

Automatické měnění velikosti písmen:

-   `Normal`

-   `Upper`

-   `Lower`


### **TextAlign**

Zarovnání textu:

-   `Left`

-   `Center`

-   `Right`


### **WordWrap**

Zalamování řádků (funguje pouze v `Multiline = true`):

-   `true` → text se zalamuje

-   `false` → text pokračuje na jeden řádek (s posuvníkem)


### **AcceptsReturn**

U víceřádového TextBoxu:

-   `true` → Enter vloží nový řádek

-   `false` → Enter odešle formulář (např. klikne na defaultní tlačítko)


### **AcceptsTab**

Umožní vložit tabulátor do textu.

### **BorderStyle**

Styl okraje:

-   `None`

-   `FixedSingle`

-   `Fixed3D`


### **ShortcutEnabled**

Povolení klávesových zkratek (Ctrl+C, Ctrl+V, Ctrl+Z…).

### **Enabled**

-   `true` → lze psát

-   `false` → TextBox je vypnutý a nereaguje


### **Visible**

Určuje, zda je TextBox viditelný.

### **Location (Left, Top)**

Pozice na formuláři:

-   `Left` → vzdálenost od levé strany

-   `Top` → vzdálenost od horní strany


### **Size (Width, Height)**

Velikost TextBoxu (výšku lze volně měnit jen při `Multiline = true`).

---