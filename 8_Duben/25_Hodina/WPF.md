# Úvod do WPF (Windows Presentation Foundation)

## Co je WPF?

**WPF (Windows Presentation Foundation)** je moderní framework pro tvorbu desktopových aplikací ve Windows pomocí platformy .NET.

Na rozdíl od Windows Forms se WPF zaměřuje na:

-   oddělení vzhledu a logiky aplikace
    
-   flexibilní rozvržení prvků
    
-   pokročilé datové vazby (data binding)
    
-   lepší práci s grafikou
    

---

## Srovnání: Windows Forms vs WPF

| Vlastnost    | Windows Forms | WPF       |
| ------------ | ------------- | --------- |
| Návrh UI     | Drag & Drop   | XAML      |
| Rozvržení    | Pevné pozice  | Dynamické |
| Stylování    | Omezené       | Pokročilé |
| Data binding | Základní      | Pokročilý |
| Vykreslování | GDI+          | DirectX   |

Hlavní rozdíl:  
WPF odděluje **uživatelské rozhraní (UI)** od **aplikační logiky**.

---

## Základní struktura aplikace

WPF používá jazyk **XAML (Extensible Application Markup Language)** pro definici UI.

### Příklad:

```XML

<Window x:Class="MyApp.MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        Title="Moje první WPF aplikace" Height="300" Width="400">  
  
    <Grid>  
        <Button Content="Klikni na mě" Width="120" Height="40"/>  
    </Grid>  
  
</Window>
```

### Code-behind (C#):

```Csharp

private void Button_Click(object sender, RoutedEventArgs e)  
{  
    MessageBox.Show("Ahoj WPF");  
}
```

---

## Rozvržení (Layout systém)

Ve WPF se prvky neumisťují pomocí přesných souřadnic jako ve Windows Forms.

Používají se tzv. **layout panely**:

-   **Grid** – rozdělení do řádků a sloupců
    
-   **StackPanel** – skládání prvků pod sebe nebo vedle sebe
    
-   **WrapPanel** – automatické zalamování
    
-   **DockPanel** – přichycení k okrajům
    

### Příklad Gridu:

```XML

<Grid>  
    <Grid.RowDefinitions>  
        <RowDefinition/>  
        <RowDefinition/>  
    </Grid.RowDefinitions>  
  
    <TextBox Grid.Row="0" />  
    <Button Grid.Row="1" Content="Odeslat"/>  
</Grid>
```

---

## Ovládací prvky (Controls)

| Windows Forms     | WPF                                                                    |
| ----------------- | ---------------------------------------------------------------------- |
| Button            | Button                                                                 |
| Label             | TextBlock / Label                                                      |
| TextBox           | TextBox                                                                |
| TextBox pro heslo | PasswordBox                                                            |
| NumericUpDown     | Není standardně (lze nahradit např. Sliderem nebo vlastní komponentou) |

### Příklad:

```XML

<StackPanel>  
    <TextBlock Text="Zadej jméno:"/>  
    <TextBox Name="NameBox"/>  
    <Button Content="Pozdrav" Click="SayHello_Click"/>  
</StackPanel>
```

---

## Události (Events)

Princip je stejný jako ve Windows Forms.

```XML

<Button Content="Klikni" Click="Button_Click"/>
```

```Csharp

private void Button_Click(object sender, RoutedEventArgs e)  
{  
    MessageBox.Show("Kliknuto");  
}
```

---

## Data Binding (datové vazby)

Jedna z nejdůležitějších vlastností WPF.

Umožňuje propojit UI přímo s daty bez nutnosti ručního nastavování hodnot.

### Příklad:

```XML

<TextBox Text="{Binding UserName}" />
```

```Csharp

public string UserName { get; set; }
```

Výhody:

-   automatická aktualizace UI
    
-   méně kódu
    
-   přehlednější aplikace
    

---

## Architektura MVVM

Ve WPF se často používá návrhový vzor **MVVM (Model-View-ViewModel)**:

-   **Model** – data (např. databáze)
    
-   **View** – uživatelské rozhraní (XAML)
    
-   **ViewModel** – logika a datové vazby
    

Tento přístup zlepšuje strukturu a udržovatelnost aplikace.

---

## Práce s databází

Připojení k databázi funguje stejně jako ve Windows Forms.
Ukážeme si později

---

## Shrnutí

-   WPF používá XAML místo klasického návrháře
    
-   rozvržení je dynamické (Grid, StackPanel)
    
-   silný důraz na data binding
    
-   podporuje čistou architekturu (MVVM)
    

---

## Cvičení

1.  Vytvoř formulář:
    
    -   TextBox (Email)
        
    -   Button
        
    -   TextBlock zobrazující zadaný text