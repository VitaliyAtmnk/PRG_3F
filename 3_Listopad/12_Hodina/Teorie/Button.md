# **WinForms: Button – základní informace**

### **Co je Button?**

`Button` je ovládací prvek, na který může uživatel kliknout.  
Používá se ke spouštění akcí, potvrzení voleb, zavírání oken atd.

> Officiální
> dokumentace -> [Button](https://learn.microsoft.com/cs-cz/dotnet/api/system.windows.forms.button?view=windowsdesktop-8.0)

---

## **Nejdůležitější vlastnosti Buttonu**

### **Text**

Text na tlačítku.

### **Font**

Písmo textu.

### **ForeColor**

Barva textu.

### **BackColor**

Barva pozadí tlačítka.

### **Image**

Obrázek zobrazený na tlačítku.

### **ImageAlign**

Umístění obrázku uvnitř tlačítka.

### **TextAlign**

Zarovnání textu v tlačítku (střed, vlevo, vpravo…).

### **TextImageRelation**

Vztah mezi textem a obrázkem:

- TextBeforeImage

- ImageBeforeText

- ImageAboveText

- TextAboveImage

- Overlay

### **FlatStyle**

Celkový vzhled tlačítka:

- `Standard`

- `Flat`

- `Popup`

- `System`

### **Enabled**

Určuje, zda lze na tlačítko kliknout (neaktivní tlačítko šedé).

### **Visible**

Určuje, zda je tlačítko vidět.

### **DialogResult**

Používá se u modálních oken (`ShowDialog()`):  
Kliknutí na tlačítko automaticky zavře okno a vrátí výsledek (`OK`, `Cancel`, `Yes`, `No`…).
> Budeme využívat později, teď není třeba si pamatovat

### **TabStop**

Zda je možné tlačítko vybrat pomocí klávesy TAB.

### **TabIndex**

Pořadí, ve kterém kontrolky dostávají fokus při použití TAB.

### **Anchor**

Určuje, jak se tlačítko chová při změně velikosti okna  
(např. ukotvení k pravému dolnímu rohu).

### **Dock**

Připnutí tlačítka k okraji okna (Top/Bottom/Left/Right/Fill).

### **Location (Left / X, Top / Y)**

Pozice tlačítka.

### **Size (Width, Height)**

Velikost tlačítka.