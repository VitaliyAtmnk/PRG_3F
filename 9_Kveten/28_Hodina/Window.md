# **WPF: práce s více okny – základní informace**

### **Co je okno ve WPF?**

Ve WPF se okno vytváří pomocí třídy `Window`. Okno slouží jako hlavní kontejner aplikace – obsahuje ovládací prvky, zobrazuje data a umožňuje uživateli pracovat s aplikací. Třída `Window` se používá pro běžná aplikační okna i dialogová okna. [Microsoft Learn+1](https://learn.microsoft.com/cs-cz/dotnet/desktop/wpf/windows/)

> Oficiální dokumentace → Window, WPF windows, dialogová okna [Microsoft Learn+2Microsoft Learn+2](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window?view=windowsdesktop-10.0)

---

## **Více oken ve WPF**

Aplikace ve WPF může obsahovat více samostatných oken.  
Typicky máme:

-   hlavní okno aplikace, například `MainWindow`
    
-   další okna, například nastavení, detail záznamu, přihlašovací okno nebo dialog
    

Každé okno je většinou samostatná třída dědící z `Window`.

Příklad:

```
C#

```
publicpartialclassSecondWindow : Window  
{  
publicSecondWindow()  
    {  
InitializeComponent();  
    }  
}
```
```

---

# **Vytvoření nového okna**

## **1\. Přidání nového okna do projektu**

Ve Visual Studiu:

1.  Pravým tlačítkem na projekt
    
2.  **Add**
    
3.  **Window (WPF)**
    
4.  Například název `SecondWindow.xaml`
    

Vzniknou dva soubory:

```
```
SecondWindow.xaml  
SecondWindow.xaml.cs
```
```

---

## **2\. Otevření dalšího okna**

Nové okno se otevře tak, že vytvoříme jeho instanci a zavoláme metodu `Show()` nebo `ShowDialog()`.

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.Show();
```
```

Metoda `Show()` otevře okno nemodálně – uživatel může pracovat i s ostatními okny aplikace. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/how-to-open-window-dialog-box)

---

# **Show vs. ShowDialog**

## **Show**

`Show()` otevře nové okno jako běžné samostatné okno.

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.Show();
```
```

Po zavolání `Show()` program pokračuje dál.  
Uživatel může přepínat mezi hlavním a novým oknem. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/how-to-open-window-dialog-box)

Používá se například pro:

-   okno s nastavením
    
-   okno s detailem položky
    
-   náhled
    
-   pomocné okno aplikace
    

---

## **ShowDialog**

`ShowDialog()` otevře okno modálně.  
To znamená, že uživatel musí toto okno nejdříve zavřít, než bude pokračovat práce s původním oknem. Volající kód čeká, dokud se dialog nezavře. [Microsoft Learn+1](https://learn.microsoft.com/cs-cz/dotnet/desktop/wpf/windows/dialog-boxes-overview)

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.ShowDialog();
```
```

Používá se například pro:

-   potvrzovací dialog
    
-   přihlašovací okno
    
-   formulář, kde uživatel musí potvrdit nebo zrušit akci
    
-   výběr hodnoty
    

---

# **DialogResult**

`DialogResult` slouží k tomu, aby dialogové okno vrátilo informaci, zda uživatel akci potvrdil nebo zrušil. Hodnota `true` obvykle znamená potvrzení, hodnota `false` zrušení. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window.dialogresult?view=windowsdesktop-10.0)

Příklad v dialogovém okně:

```
C#

```
privatevoidOkButton_Click(objectsender, RoutedEventArgse)  
{  
DialogResult=true;  
}  
  
privatevoidCancelButton_Click(objectsender, RoutedEventArgse)  
{  
DialogResult=false;  
}
```
```

Použití v hlavním okně:

```
C#

```
SecondWindowwindow=newSecondWindow();  
  
bool?result=window.ShowDialog();  
  
if (result==true)  
{  
MessageBox.Show("Uživatel potvrdil akci.");  
}  
else  
{  
MessageBox.Show("Uživatel akci zrušil.");  
}
```
```

`DialogResult` lze nastavit pouze u okna otevřeného pomocí `ShowDialog()`. Po nastavení hodnoty `DialogResult` se dialog zavře. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/dialog-boxes-overview)

---

# **Předání dat do nového okna**

Data lze do dalšího okna předat například přes konstruktor.

## **MainWindow.xaml.cs**

```
C#

```
privatevoidOpenWindow_Click(objectsender, RoutedEventArgse)  
{  
SecondWindowwindow=newSecondWindow("Ahoj z hlavního okna");  
window.Show();  
}
```
```

## **SecondWindow.xaml.cs**

```
C#

```
publicpartialclassSecondWindow : Window  
{  
publicSecondWindow(stringmessage)  
    {  
InitializeComponent();  
  
MessageTextBlock.Text=message;  
    }  
}
```
```

## **SecondWindow.xaml**

```
XML

```
<Grid>  
<TextBlockx:Name="MessageTextBlock"  
FontSize="20"  
HorizontalAlignment="Center"  
VerticalAlignment="Center"/>  
</Grid>
```
```

---

# **Předání dat zpět do hlavního okna**

Pokud má dialog vracet hodnotu, můžeme vytvořit veřejnou vlastnost.

## **SecondWindow.xaml.cs**

```
C#

```
publicpartialclassSecondWindow : Window  
{  
publicstringUserName { get; privateset; }  
  
publicSecondWindow()  
    {  
InitializeComponent();  
    }  
  
privatevoidOkButton_Click(objectsender, RoutedEventArgse)  
    {  
UserName=NameTextBox.Text;  
DialogResult=true;  
    }  
}
```
```

## **MainWindow.xaml.cs**

```
C#

```
privatevoidOpenDialog_Click(objectsender, RoutedEventArgse)  
{  
SecondWindowwindow=newSecondWindow();  
  
if (window.ShowDialog() ==true)  
    {  
stringname=window.UserName;  
MessageBox.Show($"Zadané jméno: {name}");  
    }  
}
```
```

---

# **Vlastnost Owner**

Vlastnost `Owner` určuje, které okno je vlastníkem jiného okna.  
To je užitečné hlavně u dialogů, protože dialog se potom chová jako součást hlavního okna. Třída `Window` podporuje správu vlastněných oken pomocí vlastností jako `Owner` a `OwnedWindows`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window?view=windowsdesktop-10.0)

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.Owner=this;  
window.ShowDialog();
```
```

Výhody použití `Owner`:

-   dialog se lépe váže k hlavnímu oknu
    
-   minimalizace hlavního okna ovlivní i vlastněné okno
    
-   dialog se zobrazuje logičtěji vůči hlavnímu oknu
    
-   pomáhá správnému chování modálních oken
    

---

# **Nejdůležitější vlastnosti okna**

## **Title**

Text v titulku okna.

```
XML

```
<WindowTitle="Nastavení aplikace">  
</Window>
```
```

---

## **Width a Height**

Určují šířku a výšku okna.

```
XML

```
<WindowWidth="400"Height="300">  
</Window>
```
```

---

## **WindowStartupLocation**

Určuje, kde se okno zobrazí při otevření.

Nejčastější hodnoty:

-   `Manual`
    
-   `CenterScreen`
    
-   `CenterOwner`
    

```
XML

```
<WindowWindowStartupLocation="CenterOwner">  
</Window>
```
```

---

## **ResizeMode**

Určuje, zda může uživatel měnit velikost okna.

Nejčastější hodnoty:

-   `CanResize`
    
-   `NoResize`
    
-   `CanMinimize`
    
-   `CanResizeWithGrip`
    

```
XML

```
<WindowResizeMode="NoResize">  
</Window>
```
```

---

## **WindowState**

Určuje stav okna.

Hodnoty:

-   `Normal`
    
-   `Minimized`
    
-   `Maximized`
    

```
XML

```
<WindowWindowState="Maximized">  
</Window>
```
```

---

## **Topmost**

Pokud je `true`, okno zůstává nad ostatními okny.

```
XML

```
<WindowTopmost="True">  
</Window>
```
```

---

## **ShowInTaskbar**

Určuje, zda se okno zobrazí na hlavním panelu Windows.

```
XML

```
<WindowShowInTaskbar="False">  
</Window>
```
```

---

## **Owner**

Vlastník okna.  
Často se nastavuje v C# kódu:

```
C#

```
window.Owner=this;
```
```

---

# **Nejdůležitější metody okna**

## **Show**

Otevře okno nemodálně.

```
C#

```
window.Show();
```
```

---

## **ShowDialog**

Otevře okno modálně a vrací hodnotu `bool?`.

```
C#

```
bool?result=window.ShowDialog();
```
```

---

## **Close**

Zavře okno.

```
C#

```
this.Close();
```
```

---

## **Hide**

Skryje okno, ale nezničí ho.

```
C#

```
this.Hide();
```
```

---

## **Activate**

Pokusí se aktivovat okno a přesunout na něj fokus.

```
C#

```
this.Activate();
```
```

Třída `Window` podporuje správu životního cyklu okna pomocí metod a událostí jako `Show`, `Close`, `Hide`, `Activate`, `Closing` nebo `Closed`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window?view=windowsdesktop-10.0)

---

# **Nejdůležitější události okna**

## **Loaded**

Spustí se po načtení okna.

```
C#

```
privatevoidWindow_Loaded(objectsender, RoutedEventArgse)  
{  
MessageBox.Show("Okno bylo načteno.");  
}
```
```

---

## **Closing**

Spustí se ve chvíli, kdy se okno zavírá.  
Zavření je možné zrušit nastavením `e.Cancel = true`. Událost `Closing` se vyvolá například při zavolání `Close()`, kliknutí na zavírací tlačítko nebo stisknutí `Alt + F4`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window.closing?view=windowsdesktop-10.0)

```
C#

```
privatevoidWindow_Closing(objectsender, CancelEventArgse)  
{  
MessageBoxResultresult=MessageBox.Show(  
"Opravdu chcete zavřít okno?",  
"Potvrzení",  
MessageBoxButton.YesNo);  
  
if (result==MessageBoxResult.No)  
    {  
e.Cancel=true;  
    }  
}
```
```

---

## **Closed**

Spustí se po úplném zavření okna.

```
C#

```
privatevoidWindow_Closed(objectsender, EventArgse)  
{  
MessageBox.Show("Okno bylo zavřeno.");  
}
```
```

---

## **Activated**

Spustí se, když se okno stane aktivním.

```
C#

```
privatevoidWindow_Activated(objectsender, EventArgse)  
{  
// Okno získalo fokus  
}
```
```

---

## **Deactivated**

Spustí se, když okno přestane být aktivní.

```
C#

```
privatevoidWindow_Deactivated(objectsender, EventArgse)  
{  
// Uživatel přešel na jiné okno  
}
```
```

---

# **Životnost aplikace a ShutdownMode**

U aplikací s více okny je důležité, kdy se celá aplikace ukončí.  
Chování řídí vlastnost `ShutdownMode`. Výchozí chování WPF je ukončit aplikaci po zavření posledního okna. Aplikaci lze také nastavit tak, aby se ukončila už při zavření hlavního okna. [Microsoft Learn+1](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/app-development/application-management-overview)

## **App.xaml**

```
XML

```
<Applicationx:Class="WpfApp.App"  
StartupUri="MainWindow.xaml"  
ShutdownMode="OnMainWindowClose">  
</Application>
```
```

Časté hodnoty:

-   `OnLastWindowClose` → aplikace skončí po zavření posledního okna
    
-   `OnMainWindowClose` → aplikace skončí po zavření hlavního okna
    
-   `OnExplicitShutdown` → aplikace skončí až po ručním zavolání `Shutdown()`
    

---

# **Příklad: hlavní okno otevírá druhé okno**

## **MainWindow.xaml**

```
XML

```
<Windowx:Class="WpfApp.MainWindow"  
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
Title="Hlavní okno"  
Width="400"  
Height="250">  
  
<StackPanelHorizontalAlignment="Center"  
VerticalAlignment="Center">  
  
<ButtonContent="Otevřít druhé okno"  
Width="180"  
Height="35"  
Click="OpenWindow_Click"/>  
  
</StackPanel>  
</Window>
```
```

## **MainWindow.xaml.cs**

```
C#

```
privatevoidOpenWindow_Click(objectsender, RoutedEventArgse)  
{  
SecondWindowwindow=newSecondWindow();  
window.Owner=this;  
window.Show();  
}
```
```

---

# **Příklad: modální dialog s potvrzením**

## **SecondWindow.xaml**

```
XML

```
<Windowx:Class="WpfApp.SecondWindow"  
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
Title="Dialog"  
Width="300"  
Height="180"  
WindowStartupLocation="CenterOwner"  
ResizeMode="NoResize">  
  
<StackPanelMargin="20">  
<TextBlockText="Chcete pokračovat?"  
FontSize="16"  
Margin="0,0,0,20"/>  
  
<StackPanelOrientation="Horizontal"  
HorizontalAlignment="Right">  
<ButtonContent="OK"  
Width="80"  
Margin="0,0,10,0"  
Click="OkButton_Click"/>  
  
<ButtonContent="Zrušit"  
Width="80"  
Click="CancelButton_Click"/>  
</StackPanel>  
</StackPanel>  
</Window>
```
```

## **SecondWindow.xaml.cs**

```
C#

```
privatevoidOkButton_Click(objectsender, RoutedEventArgse)  
{  
DialogResult=true;  
}  
  
privatevoidCancelButton_Click(objectsender, RoutedEventArgse)  
{  
DialogResult=false;  
}
```
```

## **MainWindow.xaml.cs**

```
C#

```
privatevoidOpenDialog_Click(objectsender, RoutedEventArgse)  
{  
SecondWindowdialog=newSecondWindow();  
dialog.Owner=this;  
  
if (dialog.ShowDialog() ==true)  
    {  
MessageBox.Show("Uživatel klikl na OK.");  
    }  
else  
    {  
MessageBox.Show("Uživatel dialog zrušil.");  
    }  
}
```
```

---

# **Časté chyby při práci s více okny**

### **Zapomenuté vytvoření instance okna**

Špatně:

```
C#

```
SecondWindow.Show();
```
```

Správně:

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.Show();
```
```

---

### **Použití DialogResult bez ShowDialog**

Špatně:

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.Show();  
window.DialogResult=true;
```
```

Správně:

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.ShowDialog();
```
```

`DialogResult` patří hlavně k modálním dialogům otevřeným přes `ShowDialog()`. [Microsoft Learn+1](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/dialog-boxes-overview)

---

### **Otevírání mnoha stejných oken**

Při každém kliknutí vznikne nové okno:

```
C#

```
SecondWindowwindow=newSecondWindow();  
window.Show();
```
```

Pokud chceme mít pouze jedno pomocné okno, můžeme si ho uložit do proměnné:

```
C#

```
privateSecondWindowsecondWindow;  
  
privatevoidOpenWindow_Click(objectsender, RoutedEventArgse)  
{  
if (secondWindow==null)  
    {  
secondWindow=newSecondWindow();  
secondWindow.Closed+= (s, args) =>secondWindow=null;  
secondWindow.Show();  
    }  
else  
    {  
secondWindow.Activate();  
    }  
}
```
```

---

# **Shrnutí**

-   Ve WPF se okna vytvářejí pomocí třídy `Window`.
    
-   Další okno se otevře pomocí `Show()` nebo `ShowDialog()`.
    
-   `Show()` otevře běžné nemodální okno.
    
-   `ShowDialog()` otevře modální dialog a čeká na jeho zavření.
    
-   Data lze předávat do okna přes konstruktor nebo vlastnosti.
    
-   Data zpět lze vracet přes veřejné vlastnosti a `DialogResult`.
    
-   Vlastnost `Owner` pomáhá správně propojit dialog s hlavním oknem.
    
-   Událost `Closing` lze použít k potvrzení zavření okna.
    
-   U více oken je důležité nastavit správný `ShutdownMode`.