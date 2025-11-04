# Opakování na test

- **11\. 11. 2025** – A1 i A2

- **45 minut**

- **OOP a pole**

- **3 úlohy:**

1. Jednoduchá třída s vlastnostmi (*properties*) a metodou (včetně getteru, setteru a konstruktoru)

2. Složitější třída (práce s řetězcem, matematická úloha nebo vykreslení do konzole)

3. Práce s polem (vytvoření, přístup k prvkům, přepis hodnot)

> Jako vždy jsou povolené materiály z GitHubu a příklady z minulých hodin.  
> Na procvičení máte na **Moodle** 2 úlohy na **pole** a 2 na **OOP**.

---

## Typy příkladů

### 1\. Jednoduchá třída

- Vytvořte třídu `Guitar`.

- Obsahuje vlastnosti (*properties*):

  - `NumberOfStrings` (počet strun)

  - `Name` (název kytary)

  - `Material` (typ materiálu – dřevo, plast apod.)

- Obsahuje konstruktor, který nastaví všechny hodnoty při vytvoření instance.

- Ke **všem** vlastnostem napište getter.

- Napište metodu `PrintInfo()`, která vypíše informace o kytaře.

```csharp
public class Program {
    public static void Main(string[] args){    
        var Kytara = new Guitar(8, "SCHECTER PT-8 MS Black Ops", "Eben");
        Console.WriteLine(Kytara.Name);
        Kytara.PrintInfo();
    }
}
--- Konzole --- 
/*

SCHECTER PT-8 MS Black Ops
Název: SCHECTER PT-8 MS Black Ops, Počet strun: 8, Materiál: Eben    

*/
```

---

### 2\. Komplikovanější třída

- Vytvořte třídu `Coder`.

- Obsahuje vlastnost `secret` (s getterem).

- Obsahuje metody:

  - `void Encode(string input)`

  - vezme `input` a zakóduje ho podle následujících pravidel:

  - všechna písmena v `input` se posunou o `secret` pozic v abecedě,

  - pokud posun přesáhne konec abecedy (např. chceme posunout `z` o 5), začne se znovu od písmene `a`  
    → `z` posunuté o `5` = `e`,

  - příklad: pokud `secret = 3`, pak `Encode("ahoj") = dkrm`.

- `void Decode(string input)`

  - opak funkce `Encode`, tedy:

  - `Encode("ahoj") = dkrm` ⇒ `Decode("dkrm") = ahoj`.

```csharp
public class Program {
    public static void Main(string[] args){    
        var blackbox = new Coder(3);
        blackbox.Encode("ahoj");
        blackbox.Decode("dkrm");
    }
}
--- Konzole --- 
/*

dkrm
ahoj

*/
```

---

### 3\. Pole (Lodě)

- Vytvořte pole čísel o délce 20.

- Pole bude reprezentovat hrací plochu.

- Na libovolná místa v poli vložte **jednou** čísla `1`, `2` a `3`.

- Vytvořte funkci `static void DrawBoard(int[] arr)`, která:

  - vykreslí herní plochu,

  - používá následující symboly:

    - `w` → 0

    - `⏅` → 1

    - `𓊝` → 2

    - `⛴` → 3

```csharp
public class Program {
    public static void Main(string[] args){    
        var board = new int[20];
        // zde přepište jedno číslo v poli na 1, jiné na 2 a 3
        // pole může vypadat například takto:
        // {0, 0, 3, 0, 0, 1, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
        DrawBoard(board);
    }
}
--- Konzole --- 
/*
|w|w|⛴|w|w|⏅|w|𓊝|w|w|w|w|w|w|w|w|w|w|w|w|
*/
```

---

#### Bonus

- Generujte pozice lodí náhodně.

- Přidejte interakci (herní smyčku) s uživatelem:

  - Uživatel uvidí hrací pole bez lodí.

  - Zadá pozici, kam chce střelit.

  - Vypíše se zpráva **HIT** / **MISS**

    - **HIT** – uživatel trefil loď

    - **MISS** – netrefil

  - **POZOR!** V dalším kole se hrací pole vykreslí znovu, ale model lodi se zobrazí pouze tehdy, pokud uživatel trefil
    políčko alespoň tolikrát, kolik má loď životů.

- Přidejte vlastní pravidlo ke hře, nebo upravte některé existující.