# Co je pole

-   **Pole** je **referenční typ** pevné délky, který drží prvky stejného typu za sebou v paměti.

-   Indexuje se od **0**.

-   Má vlastnost **`Length`** (počet prvků).

-   Přístup mimo rozsah vyhodí **`IndexOutOfRangeException`** - program spadne.


```csharp
int[] a;                 // deklarace (zatím null)
a = new int[3];          // alokace: {0, 0, 0} – výchozí hodnoty
int[] b = new int[] { 10, 20, 30 }; // inicializátor
int[] c = { 1, 2, 3, 4 };           // zkrácený zápis
```

# Výchozí hodnoty

-   Hodnotové typy (např. `int`, `bool`) mají `0`/`false`.

-   Referenční typy (`string`, vlastní třídy) mají `null`.


```csharp
int[] nums = new string[2]; // { 0, 0 }
bool[] flags = new bool[2]; // { false, false }
string[] names = new string[2]; // { null, null }
```

# Přístup k prvkům a základní operace

```csharp
int[] arr = { 5, 7, 9 };
int x = arr[0];     // 5
arr[1] = 42;        // změna prvku
int n = arr.Length; // 3

// pozor na rozsah:
int y = arr[3];     // Program spadne (existují indexy 0..2) (IndexOutOfRangeException) 
```

# Procházení pole

```csharp
int[] nums = { 1, 2, 3, 4 };

// 1) for – vhodné, když potřebuješ index a/nebo měnit prvky
for (int i = 0; i < nums.Length; i++)
{
    nums[i] *= 2;   // změna prvku je OK
}

// 2) foreach – jednodušší čtení, ale proměnnou 'item' při hodnotových typech nepřepíšeš
foreach (var item in nums)
{
    Console.WriteLine(item);
    // item = 123; // neprojde (read-only proměnná foreach)
}
```
# Příklad
```csharp
// Co je platný zápis

var a = new int[7];
int[] b = [7, 6, 5, 4, 3, 2, 1];
int[] c = {1, 2, 3, 4, 5, 6, 7};
int[] wtf = {1, 2, 1 + 2, new Random().Next(5,6), 6, (Int32.MaxValue >> 29) | 0b100};

// Co vypíše program
bool[] flags = new bool[3];
if(flags[0] == true){
    Console.Write("|");
} 

if(flags[1] == false){
    Console.Write("---");
}

flags[3] = true;

if(flags[3] == true){
    Console.Write(">");
} 
```

# Vyhledávání, třídění, další užitečné metody (`System.Array`)

```csharp
int[] a1 = { 3, 1, 4, 1, 5 };

Array.Sort(a1);          // {1,1,3,4,5}
Array.Reverse(a1);       // {5,4,3,1,1}
int idx = Array.IndexOf(a1, 4); // index prvního výskytu (nebo -1)
Array.Clear(a1, 0, 2);   // nastaví rozsah na výchozí hodnoty ({0,0,...})
Array.Clear(a1)         // vyprázdní celé pole
```

# Změna „velikosti“ pole

Pole má **pevnou délku**. Ke „změně velikosti“ se vytvoří **nové pole** a původní odkaz se přesměruje:

```csharp
int[] data = { 1, 2, 3 };
Array.Resize(ref data, 5); // data -> nové pole {1,2,3,0,0}
```

# Kopírování vs. sdílení reference

-   `=` **ne**kopíruje prvky, jen **předá referenci**.

-   Skutečná kopie prvků:


```csharp
int[] src = { 1, 2, 3 };
int[] alias = src;                 // sdílí stejnou paměť
int[] copy1 = (int[])src.Clone();  // mělká kopie (u hodnotových typů stačí)
int[] copy2 = new int[src.Length];
Array.Copy(src, copy2, src.Length);
```

# Předávání pole do funkce (co se děje)

-   **Pole je referenční typ**, ale **parametr se předává hodnotou** – tj. do funkce jde **kopie reference**.

-   Důsledky:

    1.  **Změny prvků uvnitř funkce** jsou viditelné venku (obě reference ukazují na stejné pole).

    2.  **Přesměrování parametru na nové pole** se venku **neprojeví**, pokud nepoužiješ `ref`.


```csharp
void MultiplyByTwo(int[] a)
{
    // změní prvky původního pole (venku to uvidíš)
    for (int i = 0; i < a.Length; i++)
        a[i] *= 2;

    // tohle venku vidět nebude (pouze lokální přesměrování parametru)
    a = new int[] { 99, 99 };
}

void ReplaceArray(ref int[] a)
{
    // díky ref se změní i reference volajícího
    a = new int[] { 7, 7, 7 };
}

int[] nums = { 1, 2, 3 };
MultiplyByTwo(nums); // nums => {2,4,6}
ReplaceArray(ref nums); // nums => {7,7,7}
```

> Shrnutí: prvky měnit můžeš i bez `ref`; chceš-li přesměrovat *samotné pole* (tj. referenci), použij `ref`.

---

# Řezy a indexování od konce (C# 8+)

```csharp
int[] a = { 10, 20, 30, 40, 50 };
int last = a[^1];     // 50 (index od konce)
int[] mid = a[1..4];  // {20,30,40} – vznikne NOVÉ pole
```

# Pole referenčních typů vs. hodnotových typů

```csharp
class Point { public int X; }
Point[] pts = { new Point{X=1}, new Point{X=2} };
pts[0].X = 999; // mění objekt, takže změnu uvidíš
// Pozor: při Clone/Copy je kopie „mělká“ – kopírují se reference na objekty.
```

# Praktický minipříklad (vše dohromady)

```csharp
using System;

class Demo
{
    static void Main()
    {
        int[] scores = { 3, 1, 4, 1, 5 };
        Array.Sort(scores);                  // {1,1,3,4,5}
        Console.WriteLine(scores[^1]);       // největší = 5

        Multiply(scores, 10);                // změní prvky
        Console.WriteLine(string.Join(", ", scores)); // 10, 10, 30, 40, 50

        Array.Resize(ref scores, scores.Length + 1);
        scores[^1] = 60;

        int[] top3 = scores[^3..];           // poslední tři
        Console.WriteLine(string.Join(", ", top3));   // 40, 50, 60
    }

    static void Multiply(int[] arr, int k)
    {
        for (int i = 0; i < arr.Length; i++)
            arr[i] *= k;
    }
}
```