# Opakování na test

- 7.10.2025
- vše od začátku roku (prostudujte si materiály z 2. hodiny)
- 3 příklady s rostoucí náročností
- váha 6

## Rekapitulace z minula

- opakování metod
- syntaxe
- návratový typ
- předání argumentů

## Dnes

- Pokročilejší příklady na metody/funkce
- opakování práce s řetězcem
- předání reference místo hodnoty

### Metody

#### Práce s řetězci


Je prázdný / jen mezery?
- Úkol: Vrať true, když je null, prázdný nebo jen whitespace.
- Signatura: bool IsBlank(string? s)
- Příklad: " " → true

---
Rodné číslo
- Úkol: Ověř formát YYMMDD/XXXX nebo YYMMDDXXXX a že je datum validní (včetně února).
- Signatura: bool IsCzechRCFormat(string input)
- Příklad: "995229/1234" → false (neplatné datum)

---

Končí na suffix?
- Úkol: Ověř, zda text končí zadaným suffixem.
- Signatura: bool EndsWithSuffix(string s, string suffix)
- Příklad: ("soubor.txt",".txt") → true

---
Normalizace řetězce
- Úkol: Odstraň z kraje i konce bílé znaky a zredukuj vícenásobné mezery uvnitř na jednu.
- Signatura: string NormalizeSpaces(string input)
- Příklad: " Ahoj světe " → "Ahoj světe"

---

- První písmeno velké (Title Case)
- Úkol: Každé slovo začni velkým písmenem (respektuj češtinu).
- Signatura: string ToTitleCase(string input, CultureInfo culture)
- Příklad: "mistr a markétka" → "Mistr A Markétka"
