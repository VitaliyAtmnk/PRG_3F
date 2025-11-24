# **WinForms: Label – základní informace**

### **Co je Label?**

`Label` je ovládací prvek používaný k zobrazování textu nebo obrázků.  
Neslouží k interakci (nelze na něj kliknout jako na tlačítko), je to čistě informační prvek.

> Officiální dokumentace -> [Label](https://learn.microsoft.com/cs-cz/dotnet/api/system.windows.forms.label?view=windowsdesktop-8.0)
---

## **Nejdůležitější vlastnosti (Properties) Labelu**

### **Text**

Text, který se zobrazuje uvnitř labelu.

### **Font**

Písmo (velikost, typ, tučné, kurzíva).

### **ForeColor**

Barva textu.

### **BackColor**

Barva pozadí.

### **AutoSize**

-   `true` → label se automaticky roztáhne podle textu

-   `false` → fixní rozměry, text může být zalomen nebo oříznut


### **BorderStyle**

Okraj kolem labelu:

-   `None`

-   `FixedSingle`

-   `Fixed3D`


### **TextAlign**

Zarovnání textu uvnitř labelu (např. střed, vlevo nahoře, vpravo dole…).

### **Image**

Zobrazení obrázku místo (nebo společně s) textem.

### **ImageAlign**

Pozice obrázku uvnitř labelu.

### **Padding**

Vnitřní odsazení textu od okrajů labelu.

### **Visible**

Určuje, zda je label vidět.

### **Enabled**

U Labelu nemá funkční vliv (nelze na něj kliknout), ale může být použit pro vizuální účely.

### **Location (Left, Top)**

Pozice na formuláři.

- `Left` -> odsazení od levé strany formuláře v pixelech
- `Top` -> odsazení od vrcholu formuláře v pixelech

### **Size (Width, Height)**

Velikost labelu (pokud AutoSize = false).