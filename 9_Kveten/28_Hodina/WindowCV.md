# WPF: práce s okny – cvičení

## Cvičení 1: Okno nápovědy

### Zadání

Vytvořte WPF aplikaci, která bude obsahovat hlavní okno a samostatné okno s nápovědou.

V hlavním okně vytvořte:

- nadpis aplikace,
- krátký popis aplikace,
- tlačítko **Zobrazit nápovědu**.

Po kliknutí na tlačítko se otevře nové okno `HelpWindow`.

Okno `HelpWindow` bude obsahovat:

- text s jednoduchou nápovědou,
- tlačítko **Zavřít**.

### Požadavky

- Okno nápovědy otevřete jako nemodální okno.
- Uživatel může po otevření nápovědy stále pracovat s hlavním oknem.
- Okno nápovědy se nebude otevírat opakovaně ve více kopiích.
- Pokud je okno nápovědy již otevřené, pouze se aktivuje.
- Okno nápovědy nastavte tak, aby mělo vhodný titulek, velikost a nebylo možné měnit jeho velikost.

### Doporučené prvky

- `Button`
- `TextBlock`
- `Window`

### Drobná nápověda

Pro otevření nemodálního okna použijte metodu:

```csharp
window.Show();
```

Pro aktivaci již otevřeného okna lze použít:

```csharp
window.Activate();
```

---

## Cvičení 2: Výběr obtížnosti

### Zadání

Vytvořte WPF aplikaci, ve které si uživatel vybere obtížnost pomocí dialogového okna.

V hlavním okně vytvořte:

- tlačítko **Vybrat obtížnost**,
- textový prvek, ve kterém se zobrazí aktuálně vybraná obtížnost.

Po kliknutí na tlačítko se otevře dialogové okno `DifficultyWindow`.

Dialogové okno bude obsahovat:

- tři možnosti výběru:
  - **Lehká**,
  - **Střední**,
  - **Těžká**,
- tlačítko **OK**,
- tlačítko **Zrušit**.

### Požadavky

- Dialog otevřete jako modální okno.
- Po otevření dialogu nesmí být možné pracovat s hlavním oknem, dokud není dialog zavřen.
- Po kliknutí na **OK** se vybraná obtížnost zobrazí v hlavním okně.
- Po kliknutí na **Zrušit** se hodnota v hlavním okně nezmění.
- Dialogové okno nastavte tak, aby se zobrazovalo uprostřed hlavního okna.
- Dialogové okno se nemá zobrazovat na hlavním panelu Windows.

### Doporučené prvky

- `Button`
- `TextBlock`
- `RadioButton`

### Drobná nápověda

Pro otevření modálního dialogu použijte:

```csharp
window.ShowDialog();
```

Pro zjištění, zda uživatel dialog potvrdil, lze použít návratovou hodnotu metody `ShowDialog()`.

---

## Cvičení 3: Nastavení profilu

### Zadání

Vytvořte WPF aplikaci pro jednoduché nastavení uživatelského profilu.

V hlavním okně zobrazte:

- jméno uživatele,
- vybraný motiv aplikace,
- tlačítko **Upravit profil**.

Po kliknutí na tlačítko se otevře dialogové okno `ProfileWindow`.

Do dialogového okna se předají aktuální hodnoty z hlavního okna.

Dialogové okno bude obsahovat:

- textové pole pro úpravu jména,
- rozbalovací seznam pro výběr motivu,
- tlačítko **Uložit**,
- tlačítko **Zrušit**.

Motivy mohou být například:

- Modrý,
- Červený,
- Zelený,
- Tmavý.

### Požadavky

- Aktuální jméno a motiv předejte do dialogového okna při jeho vytvoření.
- Dialogové okno otevřete modálně.
- Po kliknutí na **Uložit** se změny přenesou zpět do hlavního okna.
- Po kliknutí na **Zrušit** se změny neuloží.
- Dialogové okno nastavte jako vlastněné hlavním oknem.
- Při zavírání dialogového okna křížkem zobrazte potvrzení, zda chce uživatel opravdu zavřít okno bez uložení.

### Doporučené prvky

- `Button`
- `Label` nebo `TextBlock`
- `TextBox`
- `ComboBox`

### Drobná nápověda

Data lze do nového okna předat například přes konstruktor.

Výsledek z dialogového okna lze vrátit pomocí veřejné vlastnosti a `DialogResult`.

Při rušení zavření okna lze v události `Closing` použít:

```csharp
e.Cancel = true;
```
