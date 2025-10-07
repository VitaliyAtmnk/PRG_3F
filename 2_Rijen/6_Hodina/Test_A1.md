# Zadání (C#)

## Úkol 1 — Půjčovna aut

-   Načtěte od uživatele věk.

-   Zeptejte se, zda má řidičský průkaz (`ano/ne`).

-   Zeptejte se, kolik let má skutečné řidičské praxe (celé číslo, může být i 0).

-   Pokud je uživateli **aspoň 21 let**, **má řidičák** a **praxe je aspoň 1 rok**, vypište, že si může půjčit auto.

-   Jinak vypište, **co přesně nesplňuje** (může být více věcí najednou).


### Příklad chodu programu

```bash
Zadej věk: 22
Máš řidičský průkaz? (ano/ne): ano
Kolik let praxe máš za volantem? (0+): 2
→ Můžeš si půjčit auto.
```

Další možný průběh:

```bash
Zadej věk: 20
Máš řidičský průkaz? (ano/ne): ne
Kolik let praxe máš za volantem? (0+): 0
→ Nemůžeš si půjčit auto: nejsi starší 21 let, nemáš řidičský průkaz a nemáš alespoň 1 rok praxe.
```

---

## Úkol 2 — Čísla do `n` dělitelná 3 nebo 5

**Zadání:**  
Napište program, který:

-   vyžádá si celé číslo `n` z intervalu **1–50**,

-   postupně vypíše **všechna čísla od 1 do `n` včetně**, která jsou dělitelná **3 nebo 5**,

-   na konci vypíše **kolik** jich bylo a **jejich součet**.


### Příklad chodu programu

```bash
Zadej číslo (1–50): 12
3
5
6
9
10
12
Počet: 6
Součet: 45
```

---

## Úkol 3

**Zadání:**  
Napište funkci `obvod_obdelniku(a, b)`, která spočítá obvod obdélníku se stranami `a` a `b`.  
Program:

-   zeptá se uživatele na délky obou stran,

-   použije funkci k výpočtu obvodu,

-   a výsledek vypíše.


### Příklad chodu programu

```yaml
Zadej délku strany a: 5
Zadej délku strany b: 3
Obvod obdélníku je: 16
```

---