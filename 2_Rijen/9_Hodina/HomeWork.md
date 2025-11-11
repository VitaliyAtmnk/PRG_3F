# Úlohy OOP

---

## Úloha 1 – **PasswordGenerator**

### Zadání:

Vytvořte třídu `PasswordGenerator`, která slouží k vytváření náhodných hesel.

-   Třída má vlastnosti:

    -   `int Length` – délka generovaného hesla

    -   `bool UseNumbers` – určuje, zda se mají používat čísla

    -   `bool UseSpecialChars` – určuje, zda se mají používat speciální znaky

-   Má konstruktor, který všechny tři hodnoty nastaví.

-   Obsahuje metodu:

    -   `string Generate()`

        -   vygeneruje náhodné heslo podle nastavených pravidel

        -   pokud `UseNumbers == true`, přidá do sady znaků čísla `0–9`

        -   pokud `UseSpecialChars == true`, přidá i speciální znaky `!@#$%`

        -   z takto vytvořené sady znaků vygeneruje heslo délky `Length`

-   Metoda `PrintPassword()` vypíše heslo na konzoli.


#### Ukázka použití:

```csharp
public class Program {
    public static void Main(string[] args){
        var generator = new PasswordGenerator(10, true, true);
        generator.PrintPassword();
    }
}
--- Konzole ---
/*
Vygenerované heslo: A7m!rK@9pQ
*/
```

```csharp
public class PasswordGenerator
{
    int Length { get; set; }
    bool UseNumbers { get; set; }
    bool UseSpecialChars { get; set; }

    // alt + insert -> constructor

    public PasswordGenerator(int length, bool useNumbers, bool useSpecialChars)
    {
        Length = length;
        UseNumbers = useNumbers;
        UseSpecialChars = useSpecialChars;
    }

    public string Generate()
    {
        string allowedCharacters = "abcdefghijklmnopqrstuvwxyABCDEFGHIJKLMNOPQRSTUVWXY";
        string password = "";

        if (UseNumbers)
        {
            allowedCharacters += "0123456789";
        }

        if (UseSpecialChars)
        {
            allowedCharacters += "!@#$%";
        }

        var rng = new Random();

        for (int i = 0; i < Length; i++)
        {
            int randomIndex = rng.Next(0, allowedCharacters.Length);
            char randomChar = allowedCharacters[randomIndex];
            password += randomChar;
        }

        return password;
    }
}
```

---

## 🧩 Úloha 2 – **Student**

### Zadání:

Vytvořte třídu `Student`, která uchovává informace o známkách a dokáže vypočítat průměr.

-   Třída má vlastnosti:

    -   `string Name`

    -   `int[] Grades` – pole známek (1–5)

-   Má konstruktor, který nastaví jméno a známky.

-   Obsahuje metody:

    -   `double GetAverage()` – vrátí průměr známek

    -   `void PrintResult()` – vypíše jméno, průměr a informaci o prospěchu:

        -   průměr < 1.5 → **výborný**

        -   1.5–2.5 → **chvalitebný**

        -   2.5–3.5 → **dobrý**

        -   jinak → **nedostatečný**


#### Ukázka použití:

```csharp
public class Program {
    public static void Main(string[] args){
        var student = new Student("Petr", new int[] {1, 2, 1, 1, 2});
        student.PrintResult();
    }
}
--- Konzole ---
/*
Student: Petr
Průměr: 1.40
Prospěch: výborný
*/
```

---

# Úlohy na pole

---

## Úloha 3 – **Teploměr**

### Zadání:

Vytvořte program, který uchovává teploty za jednotlivé dny v poli.

-   Vytvořte pole `temperatures` o délce 7 (týdenní teploty).

-   Naplňte ho **náhodnými čísly** od `-5` do `25`.

-   Vypište všechny hodnoty a:

    -   nejvyšší teplotu

    -   nejnižší teplotu

    -   průměrnou teplotu


#### Ukázka výstupu:

```yaml
Teploty: [4, 10, -2, 18, 25, 12, 6]
Nejnižší teplota: -2 °C
Nejvyšší teplota: 25 °C
Průměrná teplota: 10.43 °C
```

💡 *Bonus:* Přidejte zjištění, kolik dní bylo nad 10 °C.

---

## Úloha 4 – **Traffic Simulation**

### Zadání:

Simulujte jednoduchý dopravní pruh, ve kterém se auta posouvají doleva.

-   Vytvořte pole `road` délky 10, kde:

    -   `0` = prázdné místo

    -   `1` = auto

-   Na začátku náhodně rozmístěte několik aut (např. 3–5 kusů).

-   Vytvořte metodu `static void MoveCars(int[] arr)`, která:

    -   posune všechna auta o 1 pozici doleva (auto ze začátku pole se „ztratí“)

-   V každém kroku vykreslete stav silnice (`_` = prázdné, `🚗` = auto).


#### Ukázka výstupu:

```
|_|_|🚗|_|_|🚗|_|🚗|_|_|   // jak vykreslíte mezery je zcela na Vás, zde je použit znak "|"
|_|🚗|_|_|🚗|_|🚗|_|_|_|
|🚗|_|_|🚗|_|🚗|_|_|_|_|  
```

💡 *Bonus:* Přidejte cyklus, který bude animaci opakovat několikrát (např. 5 tahů).
- Využijte
  - Console.Clear(); // vyčistí konzoli
  - Thread.Sleep(50); // pozastaví program na 50 ms, čas si upravte dle potřeb
