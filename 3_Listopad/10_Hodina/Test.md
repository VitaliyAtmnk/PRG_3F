# Varianta A

## Úloha 1

- vytvořte třídu `Light`
- třída má atributy `state` a `room`
- vytvořte konstruktor, který přijme název místnosti, ve kterém se světlo nachází a nastaví `state` na vypnutý (false, 0, slovo, je to na vás)
- vytvořte funkci toggle(), která vypne/zapne světlo a vypíše
  - v {room} (ne)svítí světlo

```csharp
Light l1 = new Light("Koupelna");
l1.toggle(); // vypíše se:  v Koupelna svítí světlo. 
l1.toggle(); //             v Koupelna nesvítí světlo. 
```
---
## Úloha 2

- mějte pole čísel, reprezentující hru piškvorek
  - 0 - prázdné pole
  - 1 - `X`
  - 2 - `O`
- vykreslete hru piškvorek na konzoli

```
pro zkopírování:
{ 0, 1, 0, 2, 0, 1, 0, 2, 0 }

pro představu:
{ 0, 1, 0,
  2, 0, 1
  0, 2, 0 }
  
výsledek na konzoli:

| _ | X | _ |
| O | _ | X |
| _ | O | _ |
```
---
## Úloha 3

- Vytvořte třídu `Converter`
- třída umí převáďet mezi číselnými soustavami
- třídá má metody
  - `int BinToDec(string Number)`
  - `string DecToHex(int num)`
  - `string HexToBin(string Number)`

```csharp
var conv = new Converter();
string binary = conv.HexToBin("3F"); // 00111111, nebo 111111 (bez nul na začátku)
int dec = conv.BinToDec("1110"); // 14
string hex = conv.DecToHex(255); // FF
```
---
# Varianta B

## Úkol 1

**Zadání:**  
`TodoItem` má `Text` (get), `IsDone` (get). Metody: `MarkDone()`. 

**Mini test:**

```csharp
var todo = new TodoItem("Napsat první třídu");
var hw = new TodoItem("Udělat úkol z matematiky");
todo.MarkDone();
Console.WriteLine($"{todo.Text}: {todo.IsDone}"); // Napsat první třídu: Hotovo
Console.WriteLine($"{hw.Text}: {hw.IsDone}"); // Udělat úkol z matematiky: Rozpracované
```
---
## Úkol 2

- mějte pole čísel, reprezentující hru piškvorek
  - 0 - prázdné pole
  - 1 - `X`
  - 2 - `O`
- vykreslete hru piškvorek na konzoli

```
pro zkopírování:
{ 0, 1, 0, 2, 0, 1, 0, 2, 0 }

pro představu:
{ 0, 1, 0,
  2, 0, 1
  0, 2, 0 }
  
výsledek na konzoli:

| _ | X | _ |
| O | _ | X |
| _ | O | _ |
```
---
## Úloha 3

-   vytvořte třídu `TextTools`

-   třída bude obsahovat metody pro práci s textem:

  -   `int CountVowels(string text)` – vrátí počet samohlásek (`a, e, i, o, u, y` včetně českých variant malých i velkých)

  -   `string Reverse(string text)` – vrátí text pozpátku

  -   `bool IsPalindrome(string text)` – vrátí `true`, pokud je text palindrom (ignorujte mezery a velikost písmen)


Ukázka použití:

```csharp
var tools = new TextTools();

int v = tools.CountVowels("Ahoj světe");     // např. 4 (A, o, ě, e)
string r = tools.Reverse("Test");           // "tseT"
bool p1 = tools.IsPalindrome("oko");        // true
bool p2 = tools.IsPalindrome("Kuna nese sen a nuk"); // true (pokud správně ignorujete mezery a velikost písmen)
```

