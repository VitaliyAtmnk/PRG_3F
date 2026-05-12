# WPF: práce s více okny – základní informace

## Co je okno ve WPF?

Ve WPF se okno vytváří pomocí třídy `Window`. Okno slouží jako hlavní kontejner aplikace – obsahuje ovládací prvky, zobrazuje data a umožňuje uživateli pracovat s aplikací. Třída `Window` se používá pro běžná aplikační okna i dialogová okna. [Microsoft Learn](https://learn.microsoft.com/cs-cz/dotnet/desktop/wpf/windows/)

> Oficiální dokumentace: [Window](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window?view=windowsdesktop-10.0), [WPF windows](https://learn.microsoft.com/cs-cz/dotnet/desktop/wpf/windows/) a [dialogová okna](https://learn.microsoft.com/cs-cz/dotnet/desktop/wpf/windows/dialog-boxes-overview).

---

## Více oken ve WPF

Aplikace ve WPF může obsahovat více samostatných oken.

Typicky máme:

- hlavní okno aplikace, například `MainWindow`,
- další okna, například nastavení, detail záznamu, přihlašovací okno nebo dialog.

Každé okno je většinou samostatná třída dědící z `Window`.

Příklad:

```csharp
public partial class SecondWindow : Window
{
    public SecondWindow()
    {
        InitializeComponent();
    }
}
```

---

## Vytvoření nového okna

### 1. Přidání nového okna do projektu

Ve Visual Studiu:

1. Pravým tlačítkem klikněte na projekt.
2. Vyberte **Add**.
3. Vyberte **Window (WPF)**.
4. Zadejte například název `SecondWindow.xaml`.

Vzniknou dva soubory:

```text
SecondWindow.xaml
SecondWindow.xaml.cs
```

---

### 2. Otevření dalšího okna

Nové okno se otevře tak, že vytvoříme jeho instanci a zavoláme metodu `Show()` nebo `ShowDialog()`.

```csharp
SecondWindow window = new SecondWindow();
window.Show();
```

Metoda `Show()` otevře okno nemodálně – uživatel může pracovat i s ostatními okny aplikace. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/how-to-open-window-dialog-box)

---

## Show vs. ShowDialog

### Show

`Show()` otevře nové okno jako běžné samostatné okno.

```csharp
SecondWindow window = new SecondWindow();
window.Show();
```

Po zavolání `Show()` program pokračuje dál. Uživatel může přepínat mezi hlavním a novým oknem. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/how-to-open-window-dialog-box)

Používá se například pro:

- okno s nastavením,
- okno s detailem položky,
- náhled,
- pomocné okno aplikace.

---

### ShowDialog

`ShowDialog()` otevře okno modálně. To znamená, že uživatel musí toto okno nejdříve zavřít, než bude pokračovat práce s původním oknem. Volající kód čeká, dokud se dialog nezavře. [Microsoft Learn](https://learn.microsoft.com/cs-cz/dotnet/desktop/wpf/windows/dialog-boxes-overview)

```csharp
SecondWindow window = new SecondWindow();
window.ShowDialog();
```

Používá se například pro:

- potvrzovací dialog,
- přihlašovací okno,
- formulář, kde uživatel musí potvrdit nebo zrušit akci,
- výběr hodnoty.

---

## DialogResult

`DialogResult` slouží k tomu, aby dialogové okno vrátilo informaci, zda uživatel akci potvrdil nebo zrušil. Hodnota `true` obvykle znamená potvrzení, hodnota `false` zrušení. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window.dialogresult?view=windowsdesktop-10.0)

Příklad v dialogovém okně:

```csharp
private void OkButton_Click(object sender, RoutedEventArgs e)
{
    DialogResult = true;
}

private void CancelButton_Click(object sender, RoutedEventArgs e)
{
    DialogResult = false;
}
```

Použití v hlavním okně:

```csharp
SecondWindow window = new SecondWindow();

bool? result = window.ShowDialog();

if (result == true)
{
    MessageBox.Show("Uživatel potvrdil akci.");
}
else
{
    MessageBox.Show("Uživatel akci zrušil.");
}
```

`DialogResult` lze nastavit pouze u okna otevřeného pomocí `ShowDialog()`. Po nastavení hodnoty `DialogResult` se dialog zavře. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/dialog-boxes-overview)

---

## Předání dat do nového okna

Data lze do dalšího okna předat například přes konstruktor.

### MainWindow.xaml.cs

```csharp
private void OpenWindow_Click(object sender, RoutedEventArgs e)
{
    SecondWindow window = new SecondWindow("Ahoj z hlavního okna");
    window.Show();
}
```

### SecondWindow.xaml.cs

```csharp
public partial class SecondWindow : Window
{
    public SecondWindow(string message)
    {
        InitializeComponent();

        MessageTextBlock.Text = message;
    }
}
```

### SecondWindow.xaml

```xml
<Grid>
    <TextBlock x:Name="MessageTextBlock"
               FontSize="20"
               HorizontalAlignment="Center"
               VerticalAlignment="Center" />
</Grid>
```

---

## Předání dat zpět do hlavního okna

Pokud má dialog vracet hodnotu, můžeme vytvořit veřejnou vlastnost.

### SecondWindow.xaml.cs

```csharp
public partial class SecondWindow : Window
{
    public string UserName { get; private set; }

    public SecondWindow()
    {
        InitializeComponent();
    }

    private void OkButton_Click(object sender, RoutedEventArgs e)
    {
        UserName = NameTextBox.Text;
        DialogResult = true;
    }
}
```

### MainWindow.xaml.cs

```csharp
private void OpenDialog_Click(object sender, RoutedEventArgs e)
{
    SecondWindow window = new SecondWindow();

    if (window.ShowDialog() == true)
    {
        string name = window.UserName;
        MessageBox.Show($"Zadané jméno: {name}");
    }
}
```

---

## Vlastnost Owner

Vlastnost `Owner` určuje, které okno je vlastníkem jiného okna. To je užitečné hlavně u dialogů, protože dialog se potom chová jako součást hlavního okna. Třída `Window` podporuje správu vlastněných oken pomocí vlastností jako `Owner` a `OwnedWindows`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window?view=windowsdesktop-10.0)

```csharp
SecondWindow window = new SecondWindow();
window.Owner = this;
window.ShowDialog();
```

Výhody použití `Owner`:

- dialog se lépe váže k hlavnímu oknu,
- minimalizace hlavního okna ovlivní i vlastněné okno,
- dialog se zobrazuje logičtěji vůči hlavnímu oknu,
- pomáhá správnému chování modálních oken.

---

## Nejdůležitější vlastnosti okna

### Title

Text v titulku okna.

```xml
<Window Title="Nastavení aplikace">
</Window>
```

---

### Width a Height

Určují šířku a výšku okna.

```xml
<Window Width="400" Height="300">
</Window>
```

---

### WindowStartupLocation

Určuje, kde se okno zobrazí při otevření.

Nejčastější hodnoty:

- `Manual`,
- `CenterScreen`,
- `CenterOwner`.

```xml
<Window WindowStartupLocation="CenterOwner">
</Window>
```

---

### ResizeMode

Určuje, zda může uživatel měnit velikost okna.

Nejčastější hodnoty:

- `CanResize`,
- `NoResize`,
- `CanMinimize`,
- `CanResizeWithGrip`.

```xml
<Window ResizeMode="NoResize">
</Window>
```

---

### WindowState

Určuje stav okna.

Hodnoty:

- `Normal`,
- `Minimized`,
- `Maximized`.

```xml
<Window WindowState="Maximized">
</Window>
```

---

### Topmost

Pokud je `true`, okno zůstává nad ostatními okny.

```xml
<Window Topmost="True">
</Window>
```

---

### ShowInTaskbar

Určuje, zda se okno zobrazí na hlavním panelu Windows.

```xml
<Window ShowInTaskbar="False">
</Window>
```

---

### Owner

Vlastník okna. Často se nastavuje v C# kódu:

```csharp
window.Owner = this;
```

---

## Nejdůležitější metody okna

### Show

Otevře okno nemodálně.

```csharp
window.Show();
```

---

### ShowDialog

Otevře okno modálně a vrací hodnotu `bool?`.

```csharp
bool? result = window.ShowDialog();
```

---

### Close

Zavře okno.

```csharp
this.Close();
```

---

### Hide

Skryje okno, ale nezničí ho.

```csharp
this.Hide();
```

---

### Activate

Pokusí se aktivovat okno a přesunout na něj fokus.

```csharp
this.Activate();
```

Třída `Window` podporuje správu životního cyklu okna pomocí metod a událostí jako `Show`, `Close`, `Hide`, `Activate`, `Closing` nebo `Closed`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window?view=windowsdesktop-10.0)

---

## Nejdůležitější události okna

### Loaded

Spustí se po načtení okna.

```csharp
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Okno bylo načteno.");
}
```

---

### Closing

Spustí se ve chvíli, kdy se okno zavírá. Zavření je možné zrušit nastavením `e.Cancel = true`. Událost `Closing` se vyvolá například při zavolání `Close()`, kliknutí na zavírací tlačítko nebo stisknutí `Alt + F4`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.windows.window.closing?view=windowsdesktop-10.0)

```csharp
private void Window_Closing(object sender, CancelEventArgs e)
{
    MessageBoxResult result = MessageBox.Show(
        "Opravdu chcete zavřít okno?",
        "Potvrzení",
        MessageBoxButton.YesNo);

    if (result == MessageBoxResult.No)
    {
        e.Cancel = true;
    }
}
```

---

### Closed

Spustí se po úplném zavření okna.

```csharp
private void Window_Closed(object sender, EventArgs e)
{
    MessageBox.Show("Okno bylo zavřeno.");
}
```

---

### Activated

Spustí se, když se okno stane aktivním.

```csharp
private void Window_Activated(object sender, EventArgs e)
{
    // Okno získalo fokus.
}
```

---

### Deactivated

Spustí se, když okno přestane být aktivní.

```csharp
private void Window_Deactivated(object sender, EventArgs e)
{
    // Uživatel přešel na jiné okno.
}
```

---

## Životnost aplikace a ShutdownMode

U aplikací s více okny je důležité, kdy se celá aplikace ukončí. Chování řídí vlastnost `ShutdownMode`. Výchozí chování WPF je ukončit aplikaci po zavření posledního okna. Aplikaci lze také nastavit tak, aby se ukončila už při zavření hlavního okna. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/app-development/application-management-overview)

### App.xaml

```xml
<Application x:Class="WpfApp.App"
             StartupUri="MainWindow.xaml"
             ShutdownMode="OnMainWindowClose">
</Application>
```

Časté hodnoty:

- `OnLastWindowClose` → aplikace skončí po zavření posledního okna,
- `OnMainWindowClose` → aplikace skončí po zavření hlavního okna,
- `OnExplicitShutdown` → aplikace skončí až po ručním zavolání `Shutdown()`.

---

## Příklad: hlavní okno otevírá druhé okno

### MainWindow.xaml

```xml
<Window x:Class="WpfApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Hlavní okno"
        Width="400"
        Height="250">

    <StackPanel HorizontalAlignment="Center"
                VerticalAlignment="Center">

        <Button Content="Otevřít druhé okno"
                Width="180"
                Height="35"
                Click="OpenWindow_Click" />

    </StackPanel>
</Window>
```

### MainWindow.xaml.cs

```csharp
private void OpenWindow_Click(object sender, RoutedEventArgs e)
{
    SecondWindow window = new SecondWindow();
    window.Owner = this;
    window.Show();
}
```

---

## Příklad: modální dialog s potvrzením

### SecondWindow.xaml

```xml
<Window x:Class="WpfApp.SecondWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Dialog"
        Width="300"
        Height="180"
        WindowStartupLocation="CenterOwner"
        ResizeMode="NoResize">

    <StackPanel Margin="20">
        <TextBlock Text="Chcete pokračovat?"
                   FontSize="16"
                   Margin="0,0,0,20" />

        <StackPanel Orientation="Horizontal"
                    HorizontalAlignment="Right">
            <Button Content="OK"
                    Width="80"
                    Margin="0,0,10,0"
                    Click="OkButton_Click" />

            <Button Content="Zrušit"
                    Width="80"
                    Click="CancelButton_Click" />
        </StackPanel>
    </StackPanel>
</Window>
```

### SecondWindow.xaml.cs

```csharp
private void OkButton_Click(object sender, RoutedEventArgs e)
{
    DialogResult = true;
}

private void CancelButton_Click(object sender, RoutedEventArgs e)
{
    DialogResult = false;
}
```

### MainWindow.xaml.cs

```csharp
private void OpenDialog_Click(object sender, RoutedEventArgs e)
{
    SecondWindow dialog = new SecondWindow();
    dialog.Owner = this;

    if (dialog.ShowDialog() == true)
    {
        MessageBox.Show("Uživatel klikl na OK.");
    }
    else
    {
        MessageBox.Show("Uživatel dialog zrušil.");
    }
}
```

---

## Časté chyby při práci s více okny

### Zapomenuté vytvoření instance okna

Špatně:

```csharp
SecondWindow.Show();
```

Správně:

```csharp
SecondWindow window = new SecondWindow();
window.Show();
```

---

### Použití DialogResult bez ShowDialog

Špatně:

```csharp
SecondWindow window = new SecondWindow();
window.Show();
window.DialogResult = true;
```

Správně:

```csharp
SecondWindow window = new SecondWindow();
window.ShowDialog();
```

`DialogResult` patří hlavně k modálním dialogům otevřeným přes `ShowDialog()`. [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/windows/dialog-boxes-overview)

---

### Otevírání mnoha stejných oken

Při každém kliknutí vznikne nové okno:

```csharp
SecondWindow window = new SecondWindow();
window.Show();
```

Pokud chceme mít pouze jedno pomocné okno, můžeme si ho uložit do proměnné:

```csharp
private SecondWindow secondWindow;

private void OpenWindow_Click(object sender, RoutedEventArgs e)
{
    if (secondWindow == null)
    {
        secondWindow = new SecondWindow();
        secondWindow.Closed += (s, args) => secondWindow = null;
        secondWindow.Show();
    }
    else
    {
        secondWindow.Activate();
    }
}
```

---

## Shrnutí

- Ve WPF se okna vytvářejí pomocí třídy `Window`.
- Další okno se otevře pomocí `Show()` nebo `ShowDialog()`.
- `Show()` otevře běžné nemodální okno.
- `ShowDialog()` otevře modální dialog a čeká na jeho zavření.
- Data lze předávat do okna přes konstruktor nebo vlastnosti.
- Data zpět lze vracet přes veřejné vlastnosti a `DialogResult`.
- Vlastnost `Owner` pomáhá správně propojit dialog s hlavním oknem.
- Událost `Closing` lze použít k potvrzení zavření okna.
- U více oken je důležité nastavit správný `ShutdownMode`.