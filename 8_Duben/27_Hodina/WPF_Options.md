# WPF – CheckBox, RadioButton a ComboBox

##  CheckBox
    

CheckBox slouží k výběru možnosti, která může být zapnutá nebo vypnutá. Uživatel může políčko zaškrtnout nebo odškrtnout. Hodí se například pro volby jako „Souhlasím“, „Zapnout zvuk“ nebo „Zobrazit podrobnosti“.

Základní vlastnosti:  
- Content – text zobrazený vedle prvku  
- IsChecked – určuje, zda je políčko zaškrtnuté  
- IsEnabled – určuje, zda je prvek aktivní  
- IsThreeState – povolí třetí stav neurčeno

CheckBox může mít tyto stavy:  
- true – zaškrtnuto  
- false – odškrtnuto  
- null – neurčeno, pokud je IsThreeState nastaveno na true

Jednoduchá ukázka v XAML:

```XML

<CheckBox x:Name\="chbSouhlas"  
          Content\="Souhlasím s podmínkami"  
          Margin\="10" />
```

Kontrola hodnoty v C#:

```Csharp

if (chbSouhlas.IsChecked \== true)  
{  
    MessageBox.Show("CheckBox je zaškrtnutý.");  
}  
else  
{  
    MessageBox.Show("CheckBox není zaškrtnutý.");  
}
```

Ukázka s událostmi:

```XML

<CheckBox x:Name\="chbNotifikace"  
          Content\="Zapnout notifikace"  
          Margin\="10"  
          Checked\="chbNotifikace\_Checked"  
          Unchecked\="chbNotifikace\_Unchecked" />
```

```csharp

private void chbNotifikace\_Checked(object sender, RoutedEventArgs e)  
{  
    MessageBox.Show("Notifikace byly zapnuty.");  
}  
  
private void chbNotifikace\_Unchecked(object sender, RoutedEventArgs e)  
{  
    MessageBox.Show("Notifikace byly vypnuty.");  
}
```

Ukázka tří stavů:

```XML

<CheckBox x:Name\="chbStav"  
          Content\="Neurčený stav"  
          Margin\="10"  
          IsThreeState\="True" />
```

```Csharp

if (chbStav.IsChecked \== true)  
{  
    MessageBox.Show("Zaškrtnuto");  
}  
else if (chbStav.IsChecked \== false)  
{  
    MessageBox.Show("Odškrtnuto");  
}  
else  
{  
    MessageBox.Show("Neurčeno");  
}
```

##  RadioButton
    

RadioButton slouží k výběru právě jedné možnosti z více nabídek. Používá se tam, kde uživatel nemá vybírat více možností najednou, ale pouze jednu.

Typický příklad:  
- výběr pohlaví  
- výběr způsobu dopravy  
- výběr typu platby

Základní vlastnosti:  
- Content – text u prvku  
- IsChecked – určuje, zda je volba vybraná  
- GroupName – spojuje více RadioButtonů do jedné skupiny  
- IsEnabled – určuje, zda je prvek aktivní

Pokud mají RadioButtony stejné GroupName, lze vybrat pouze jeden z nich.

Jednoduchá ukázka v XAML:

```XML

<StackPanel Margin\="10"\>  
    <RadioButton x:Name\="rbMuz"  
                 Content\="Muž"  
                 GroupName\="Pohlavi"  
                 Margin\="0,0,0,5" />  
  
    <RadioButton x:Name\="rbZena"  
                 Content\="Žena"  
                 GroupName\="Pohlavi" />  
</StackPanel>
```

Zjištění vybrané možnosti v C#:

```csharp

if (rbMuz.IsChecked \== true)  
{  
    MessageBox.Show("Vybrána možnost Muž.");  
}  
else if (rbZena.IsChecked \== true)  
{  
    MessageBox.Show("Vybrána možnost Žena.");  
}
```

Ukázka s více možnostmi:

```XML

<StackPanel Margin\="10"\>  
    <TextBlock Text\="Způsob dopravy:" Margin\="0,0,0,5"/>  
  
    <RadioButton x:Name\="rbAuto"  
                 Content\="Auto"  
                 GroupName\="Doprava"  
                 Margin\="0,0,0,5" />  
  
    <RadioButton x:Name\="rbVlak"  
                 Content\="Vlak"  
                 GroupName\="Doprava"  
                 Margin\="0,0,0,5" />  
  
    <RadioButton x:Name\="rbAutobus"  
                 Content\="Autobus"  
                 GroupName\="Doprava" />  
</StackPanel>
```

Událost Checked:

```XML

<RadioButton x:Name\="rbKarta"  
             Content\="Platba kartou"  
             GroupName\="Platba"  
             Checked\="rbKarta\_Checked" />
```

```C#

private void rbKarta\_Checked(object sender, RoutedEventArgs e)  
{  
    MessageBox.Show("Byla vybrána platba kartou.");  
}
```

##  ComboBox
    

ComboBox je rozbalovací seznam. Umožňuje vybrat jednu položku z více možností. Šetří místo v okně, protože zobrazuje jen aktuálně vybranou položku a ostatní zobrazí až po rozkliknutí.

Použití:  
- výběr města  
- výběr třídy  
- výběr jazyka aplikace

Základní vlastnosti:  
- Items – kolekce položek v seznamu  
- SelectedIndex – index vybrané položky  
- SelectedItem – aktuálně vybraná položka  
- IsEditable – určuje, zda může uživatel psát vlastní text  
- IsEnabled – určuje, zda je prvek aktivní

Jednoduchá ukázka v XAML:

```XML

<ComboBox x:Name\="cmbMesto" Width\="150" Margin\="10"\>  
    <ComboBoxItem Content\="Praha" />  
    <ComboBoxItem Content\="Brno" />  
    <ComboBoxItem Content\="Ostrava" />  
</ComboBox>
```

Zjištění vybrané položky v C#:

```csharp

ComboBoxItem vybraneMesto \= (ComboBoxItem)cmbMesto.SelectedItem;  
  
if (vybraneMesto != null)  
{  
    MessageBox.Show("Vybrané město: " + vybraneMesto.Content.ToString());  
}
```

Výběr položky podle indexu:

```csharp

cmbMesto.SelectedIndex \= 0;
```

To znamená, že se vybere první položka v seznamu.

Přidání položek v C#:

```csharp
cmbMesto.Items.Add("Plzeň");  
cmbMesto.Items.Add("Liberec");  
cmbMesto.Items.Add("Olomouc");
```

V tomto případě budou položky typu string, takže čtení hodnoty bude jednodušší:

```csharp
if (cmbMesto.SelectedItem != null)  
{  
    MessageBox.Show("Vybrané město: " + cmbMesto.SelectedItem.ToString());  
}
```

Ukázka události SelectionChanged:

```XML

<ComboBox x:Name\="cmbJazyk"  
          Width\="150"  
          Margin\="10"  
          SelectionChanged\="cmbJazyk\_SelectionChanged"\>  
    <ComboBoxItem Content\="Čeština" />  
    <ComboBoxItem Content\="Angličtina" />  
    <ComboBoxItem Content\="Němčina" />  
</ComboBox>
```

```csharp

private void cmbJazyk\_SelectionChanged(object sender, SelectionChangedEventArgs e)  
{  
    ComboBoxItem vybranyJazyk \= (ComboBoxItem)cmbJazyk.SelectedItem;  
  
    if (vybranyJazyk != null)  
    {  
        MessageBox.Show("Vybraný jazyk: " + vybranyJazyk.Content.ToString());  
    }  
}
```

##  Srovnání prvků
    

### CheckBox:  
Používá se tehdy, když lze možnost zapnout nebo vypnout.  
Uživatel může vybrat i více CheckBoxů současně.

### RadioButton:  
Používá se tehdy, když se má vybrat právě jedna možnost z více variant.  
Ve stejné skupině lze vybrat jen jeden prvek.

### ComboBox:  
Používá se tehdy, když je více možností a chceme šetřit místo v okně.  
Uživatel vybírá jednu položku z rozbalovacího seznamu.

5.  Společná ukázka XAML:

```XML

<Window x:Class\="WpfApp1.MainWindow"  
        xmlns\="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x\="http://schemas.microsoft.com/winfx/2006/xaml"  
        Title\="Ukázka prvků" Height\="300" Width\="300"\>  
    <StackPanel Margin\="10"\>  
  
        <CheckBox x:Name\="chbDarkMode"  
                  Content\="Tmavý režim"  
                  Margin\="0,0,0,10"/>  
  
        <TextBlock Text\="Velikost písma:" Margin\="0,0,0,5"/>  
  
        <RadioButton x:Name\="rbMale"  
                     Content\="Malé"  
                     GroupName\="Velikost"  
                     Margin\="0,0,0,5"/>  
  
        <RadioButton x:Name\="rbStredni"  
                     Content\="Střední"  
                     GroupName\="Velikost"  
                     Margin\="0,0,0,5"/>  
  
        <RadioButton x:Name\="rbVelke"  
                     Content\="Velké"  
                     GroupName\="Velikost"  
                     Margin\="0,0,0,10"/>  
  
        <ComboBox x:Name\="cmbBarva" Width\="120" Margin\="0,0,0,10"\>  
            <ComboBoxItem Content\="Červená"/>  
            <ComboBoxItem Content\="Modrá"/>  
            <ComboBoxItem Content\="Zelená"/>  
        </ComboBox>  
  
        <Button Content\="Zobrazit volby"  
                Click\="Button\_Click"  
                Width\="120"/>  
    </StackPanel>  
</Window>
```

C#:

```Csharp

private void Button\_Click(object sender, RoutedEventArgs e)  
{  
    string darkMode \= chbDarkMode.IsChecked \== true ? "Ano" : "Ne";  
  
    string velikost \= "";  
    if (rbMale.IsChecked \== true)  
        velikost \= "Malé";  
    else if (rbStredni.IsChecked \== true)  
        velikost \= "Střední";  
    else if (rbVelke.IsChecked \== true)  
        velikost \= "Velké";  
  
    string barva \= "";  
    ComboBoxItem vybranaBarva \= (ComboBoxItem)cmbBarva.SelectedItem;  
    if (vybranaBarva != null)  
        barva \= vybranaBarva.Content.ToString();  
  
    MessageBox.Show(  
        "Tmavý režim: " + darkMode +  
        "\\nVelikost písma: " + velikost +  
        "\\nBarva: " + barva  
    );  
}
```

##  Shrnutí
    

- CheckBox je vhodný pro zapnutí nebo vypnutí jedné volby.  
- RadioButton je vhodný pro výběr jedné možnosti ze skupiny.  
- ComboBox je vhodný pro výběr jedné položky z většího seznamu.