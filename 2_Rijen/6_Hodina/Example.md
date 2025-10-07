# Úkoly

- Včechny úkoly řešte pomocí funkcí/metod
- každý úkol se bude skládat z minimálně jedné funkce
- návratový typ a argumenty funkce jsou plně ve vaší režii

## Bankomat

- Nechte uživatele zadat libovolné kladné číslo.
- Pokud uživatel zadá částku `0–350 000`,
    - vypíšete hlášku `Úspěšně vloženo "částka" Kč.` (místo _částka_ program doplní zadané číslo)
- Pokud uživatel zadá zápornou částku,
    - vypíšete hlášku `Detekována krádež – prosíme, neutíkejte, přijde policie.`
- Pokud uživatel zadá částku `350 001 a více`,
    - základ: `Nelze vložit více než 350 000 Kč`
- **Bonus**
    - _Hodí se_ kostkou a pokud padne 6, akceptuje se vklad `350 000` a přebytek jde bance do kapsy.
    - Jinak se vklad zamítne a vypíše se `Nelze vložit více než 350 000 Kč`.

### Chod programu

```
Scénář 1:
Vložte do bankomatu 0–350 000:
120000
Úspěšně vloženo 120 000 Kč.

Scénář 2:
Vložte do bankomatu 0–350 000:
-500
Detekována krádež – prosíme, neutíkejte, přijde policie.

Scénář 3:
Vložte do bankomatu 0–350 000:
351001
Nelze vložit více než 350 000 Kč.

Scénář 4 (bonus):
Vložte do bankomatu 0–350 000:
351001
Úspěšně vloženo 350 000 Kč a děkujeme za příspěvek ve výši 1 001 Kč.
```

## Kámen nůžky papír vs AI

- napište program, který bude do nekonečna hrát kámen nůžky papír proti hráči a nikdy neprohraje.
- Uživatel nebude psát slova, ani ukazovat gesta na kameru.
- Program zobrazí nabídku, která bude vypadat například takto: 
```
Vyberte možnost:
1. Kámen
2. Nůžky
3. Papír
4. Ukončit hru
```

- Bonus: 
- Vytvořte režimy
  - _Jirka procházka_ - PC Hraje jen kámen
  - _Arthrogryposis_ - PC Hraje jen papír
  - Nůžky - PC Hraje jen nůžky