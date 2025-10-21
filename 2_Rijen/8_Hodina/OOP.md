## Co je OOP v C#?

Objektově orientované programování (OOP) organizuje kód do **tříd** a **objektů**.

- Každý objekt kombinuje:

    - **stav** (pole/atributy, typicky přes **vlastnosti – properties**)

    - **chování** (metody)

- Objekty spolu komunikují voláním metod a předáváním zpráv/parametrů.

---

```csharp
public class Person{

    // Attributes
    public int age;
    public String name;
    private double energy; // Private attributes typically start with _
    private const int BaseEnergy = 100;
    
    // Methods
    public void Sleep(){
        Console.WriteLine("sleeping for a healthy 4 hours");
        energy += 0.1;
    }
    public void Work(){
        if (energy > 0){
            Console.WriteLine("Working...");
            energy -= 5; // some random value
        }
            
        else {
            Console.WriteLine("Guess I'll die");
            energy = 0;
         }
    }
    public void GainEnergy(double value){
        Console.WriteLine("Eating");
        energy += value;    
    }
    
    // Constructor
    public Person(String name, int age){
        this.name = name;
        this.age = age;
        energy = _BASE_ENERGY;
    }
    
    // getters
    public int GetAge(){ return age; }
    public Strign GetName(){ return name; }
}
```
---
- Využití
```csharp
public static void Main(string[] args){
    Person a = new Person("Cyril", 17);
    a.sleep();
    a.work();
    a.gainEnergy(15.3);
}
```
---
- C# style
```csharp
using System;

public class Person
{
    // Fields
    private double _energy;
    private const int BaseEnergy = 100;

    // Properties
    public int Age { get; }
    public string Name { get; }
    public double Energy => _energy;

    // Constructor
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
        _energy = BaseEnergy;
    }

    // Methods
    public void Sleep()
    {
        Console.WriteLine("Sleeping for a healthy 4 hours");
        _energy += 0.1;
    }

    public void Work()
    {
        if (_energy > 0)
        {
            Console.WriteLine("Working...");
            _energy -= 5;
        }
        else
        {
            Console.WriteLine("Guess I'll die");
            _energy = 0;
        }
    }

    public void GainEnergy(double value)
    {
        Console.WriteLine("Eating");
        _energy += value;
    }
}

```

## Základní principy

- **Zapouzdření (Encapsulation):**  
  Skrytí vnitřního stavu za veřejným rozhraním. V C# se používají **modifikátory přístupu
  ** (`public`, `private`, `protected`, `internal`) a **vlastnosti** (properties) místo přímého přístupu k polím.

- **Dědičnost (Inheritance):**  
  Třída může **dědit** z jedné základní třídy (`:`) a převzít její členy. Upravuje se přes **virtuální**/**přepsané**
  metody (`virtual`/`override`). Cílem je **znovupoužitelnost** a **rozšiřitelnost**.

- **Polymorfismus (Polymorphism):**  
  Stejné volání může vést k odlišnému chování podle konkrétního typu objektu. V praxi: volání přes referenci základní
  třídy nebo **rozhraní** (`interface`) vyvolá přepsanou implementaci potomka.

- **Abstrakce (Abstraction):**  
  Zvýraznění podstatných vlastností a skrytí detailů. V C#: **abstraktní třídy** (`abstract`) a **rozhraní** definují *
  *co** je třeba umět, nikoliv **jak**.

---

## Základy C# OOP – stavební kameny

- **Třída (`class`)**: šablona pro objekty.

- **Objekt**: konkrétní instance třídy vytvořená pomocí `new`.

- **Pole vs. vlastnosti**:

    - **Pole**: surový stav (typicky `private`).

    - **Vlastnost (property)**: řízený přístup ke stavu s `get`/`set` (často **auto-property**).

- **Metody**: chování třídy, mohou být **statické** (`static`) – patří třídě, nikoli instanci.

- **Konstruktory**: inicializace nových objektů; mohou být přetížené.

- **Modifikátory přístupu**: `public`, `private`, `protected`, `internal`,
  kombinace `protected internal`, `private protected`.

- **Dědičnost a přepisování**: `virtual`, `override`, zákaz dědění přes `sealed`.

- **Rozhraní (`interface`)**: kontrakt schopností; třída/struct jej **implementuje** (`:`) a musí dodat
  metody/vlastnosti.

- **Abstraktní třídy (`abstract`)**: nelze přímo instancovat; obsahuje abstraktní členy k doplnění v potomcích.

- **`this`**: odkaz na aktuální instanci (užitečné při pojmenování parametrů shodných s vlastnostmi).

- **Inicializátory objektů**: pohodlné nastavení vlastností při vytváření instance.

- **Přetížení metod**: více metod se stejným názvem, ale jinými parametry.

- **Základní datové typy**: `int`, `string`, `bool`, atd.; `string` je referenční typ s chováním hodnotového.

- **`record`** (stručně): typ pro **datově orientované** objekty s rovností podle obsahu; vhodné pro DTO, ale pro
  základy stačí vědět, že existuje.

- **`struct`** (stručně): **hodnotový typ**, obvykle malý a neměnný; třídy jsou **referenční typy**.

---

## Procedurální vs. objektový přístup

### Procedurální přístup

- **Organizace:** funkce a globální/ sdílená data.

- **Struktura:** posloupnost kroků volajících funkce.

- **Výhody:** přímočarost, jednoduchost pro malé skripty.

- **Nevýhody:** horší modularita, obtížná údržba a rozšiřitelnost, tendence k rozptýlenému stavu.

### Objektově orientovaný přístup

- **Organizace:** logika zabalená v třídách/objektech.

- **Struktura:** využití zapouzdření, dědičnosti, polymorfismu → modulární, testovatelný návrh.

- **Výhody:** lepší opakovatelnost, čitelnost, možnost modelovat doménu.

- **Nevýhody:** vyšší návrhová náročnost, počáteční režie.

---

## Mini-slovníček C# OOP (prakticky)

- **Property – auto-property**:

  ```csharp
  public class Player {
      public string Name { get; set; } = "Anonym"; // auto-property se základní hodnotou
      public int Score { get; private set; }       // set je soukromý – kontrola zvenčí
      public void AddPoints(int pts) => Score += pts;
  }
  ```

- **Konstruktory a přetěžování**:

  ```csharp
  public class Card {
      public int Value { get; }
      public Card(int value) { Value = value; }
  }
  ```

- **Dědičnost + polymorfismus**:

  ```csharp
  public abstract class Participant {
      public string Name { get; }
      protected Participant(string name) => Name = name;
      public abstract int Decide(int currentScore); // kontrakt
  }
  
  public class Dealer : Participant {
      public Dealer() : base("Dealer") {}
      public override int Decide(int currentScore) => currentScore < 17 ? 1 : 0;
  }
  ```

- **Rozhraní**:

  ```csharp
  public interface IShufflable { void Shuffle(); }
  
  public class Deck : IShufflable {
      public void Shuffle() { /* ... */ }
  }
  ``` 
---
# Mini úkoly
## Cvičení 1 — Kniha (`Book`)

**Zadání:**  
Navrhni třídu `Book` se stavem: `Title`, `Author`, `Pages`. Přidej metodu `Info()` vracející krátký popis jako string (např. `"Author — Title (Pages: 320)"`).  
**Tip:** Použij auto-properties.

**Mini test:**

```csharp
var b = new Book("Duna", "Frank Herbert", 544);
Console.WriteLine(b.Info());
```

---

## Cvičení 2 — Baterie (`Battery`)

**Zadání:**  
Třída `Battery` má energii v procentech (0–100). Metody: `Charge(int amount)` a `Use(int amount)`. Hodnota se nesmí dostat mimo 0–100.  
**Tip:** Uvnitř hlídej rozsah (Math.Min/Math.Max).

**Mini test:**

```csharp
var bat = new Battery(50);
bat.Use(30);   // 20
bat.Charge(90);// 100
Console.WriteLine(bat.Level);
```

---

## Cvičení 3 — Student (`Student`)

**Zadání:**  
Třída `Student` má `Name` (jen get) a `Credits` (jen get). Metody: `PassCourse(int credits)` zvyšuje kredity; `Reset()` vrátí na 0.  
**Tip:** `Name` zkus udělat jako `get; init;` nebo jen `get;` a nastavovat v konstruktoru.

**Mini test:**

```csharp
var s = new Student("Cyril");
s.PassCourse(6);
Console.WriteLine($"{s.Name}: {s.Credits}"); // Cyril: 6
s.Reset();
```

---

## Cvičení 4 — Teploměr (`Thermometer`)

**Zadání:**  
Třída `Thermometer` drží `TemperatureC` (double). Metody: `ToFahrenheit()` → `double`, `Warm(double delta)`, `Cool(double delta)`.  
**Tip:** Vzorec: `F = C * 9/5 + 32`.

**Mini test:**

```csharp
var t = new Thermometer(20);
t.Warm(2.5);
Console.WriteLine(t.ToFahrenheit());
```

---

## Cvičení 5 — Počítadlo kroků (`StepCounter`)

**Zadání:**  
`StepCounter` má vnitřní `steps` (private) a veřejné `Steps` (jen get). Metody: `Add(int n)` (ignoruj záporné), `Reset()`.  
**Tip:** Zvaž ochranu proti přetečení (nepovinné).

**Mini test:**

```csharp
var sc = new StepCounter();
sc.Add(1200);
sc.Add(-5); // ignoruj
Console.WriteLine(sc.Steps);
```

---

## Cvičení 6 — Zůstatek (`Wallet`)

**Zadání:**  
Třída `Wallet` s `Balance` (decimal, jen get). Metody: `Deposit(decimal amount)`, `Withdraw(decimal amount)` (povol jen, když je dost peněz).  
**Tip:** Vracej `bool` z `Withdraw`, ať volající ví, zda se povedlo.

**Mini test:**

```csharp
var w = new Wallet();
w.Deposit(100m);
Console.WriteLine(w.Withdraw(130m)); // false
Console.WriteLine(w.Balance);        // 100
```

---

## Cvičení 7 — Časovač pomodoro (`PomodoroTimer`)

**Zadání:**  
Drž `WorkMinutes` a `BreakMinutes` (jen get). Metody: `StartWork()`, `StartBreak()` vypíší, co se děje (Console.WriteLine) a vrátí délku segmentu v minutách.  
**Tip:** Stačí jednoduché chování, žádné reálné měření času.

**Mini test:**

```csharp
var p = new PomodoroTimer(25, 5);
p.StartWork();
p.StartBreak();
```

---

## Cvičení 8 — Hudební skladba (`Song`)

**Zadání:**  
`Song` má `Title`, `Artist`, `LengthSeconds`. Metody: `Play()` (vypíše „▶️ Titul — Artist (mm:ss)“), `ShortInfo()` (string).  
**Tip:** Napiš pomocnou privátní metodu pro formátování `mm:ss`.

**Mini test:**

```csharp
var s = new Song("Remember Me", "Umi", 213);
s.Play();
Console.WriteLine(s.ShortInfo());
```

---

## Cvičení 9 — Úkol (`TodoItem`)

**Zadání:**  
`TodoItem` má `Text` (get), `IsDone` (get). Metody: `MarkDone()`, `MarkUndone()`.  
**Tip:** Přidej `CreatedAt` (DateTime, get) pro čas vzniku (bonus).

**Mini test:**

```csharp
var todo = new TodoItem("Napsat první třídu");
todo.MarkDone();
Console.WriteLine($"{todo.Text}: {todo.IsDone}");
```

---

## Cvičení 10 — Jednoduchý bankovní účet (`BankAccount`)

**Zadání:**  
Atributy: `Owner` (get), `Number` (get), `Balance` (get). Metody: `Deposit`, `Withdraw`, `PrintStatement()` (vypíše poslední operaci a stav).  
**Tip:** `Withdraw` vracej `bool`; validuj záporné částky.

**Mini test:**

```csharp
var acc = new BankAccount("A-001", "Eva");
acc.Deposit(500);
acc.Withdraw(120);
acc.PrintStatement();
```

---

## Cvičení 11 — Přehrávač videa (`VideoPlayer`)

**Zadání:**  
Stav: `Title`, `DurationSec`, `PositionSec` (jen get). Metody: `Play()`, `Pause()`, `Seek(int seconds)` (omez pozici na 0–Duration).  
**Tip:** `Seek` může brát kladné i záporné posuny.

**Mini test:**

```csharp
var v = new VideoPlayer("Intro", 90);
v.Seek(30);
v.Play();
v.Seek(-10);
v.Pause();
```

---

## Cvičení 12 — Dveře (`Door`)

**Zadání:**  
Stav: `IsOpen` (get). Metody: `Open()`, `Close()`, `Toggle()`.  
**Tip:** `Open`/`Close` můžou nic nedělat, když je stav stejný (idempotentní).

**Mini test:**

```csharp
var d = new Door();
d.Open();
d.Toggle(); // zavře
Console.WriteLine(d.IsOpen);
```

---

## Cvičení 13 — Základní validace (`User`)

**Zadání:**  
`User` má `Username` (get), `Email` (get). Konstruktor by měl vyhodit `ArgumentException`, když je prázdný `Username` nebo neplatný `Email` (stačí jednoduchá kontrola `"@"`).  
**Tip:** Validuj v konstruktoru.

**Mini test:**

```csharp
var u = new User("cyril", "cyril@example.com");
Console.WriteLine($"{u.Username} / {u.Email}");
```

---

## Cvičení 14 — Nádrž na vodu (`WaterTank`)

**Zadání:**  
Max kapacita (get) a aktuální objem (get). Metody: `Fill(int liters)`, `Drain(int liters)`. Nikdy nepřelej přes kapacitu ani nepůjdi pod 0.  
**Tip:** Zvaž návratový `int` — kolik se skutečně nalilo/odteklo.

**Mini test:**

```csharp
var wt = new WaterTank(100);
wt.Fill(80);
Console.WriteLine(wt.Fill(50)); // nalije se jen 20
```

---

## Cvičení 15 — Jednoduchý RNG wrapper (`Dice`)

**Zadání:**  
`Dice` má počet stěn (get). Metoda `Roll()` vrátí číslo v intervalu 1..N.  
**Tip:** Drž `Random` jako `static readonly` pole v třídě.

**Mini test:**

```csharp
var d6 = new Dice(6);
Console.WriteLine(d6.Roll());
```

---
