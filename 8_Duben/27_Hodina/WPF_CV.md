# 1\. Objednávka pizzy

## Zadání

Vytvoř WPF formulář pro objednávku pizzy.

Aplikace bude obsahovat:

-   `TextBox` pro jméno zákazníka
    
-   skupinu `RadioButton` pro výběr velikosti pizzy:
    
    -   malá
        
    -   střední
        
    -   velká
        
-   několik `CheckBoxu` pro přísady navíc:
    
    -   sýr navíc
        
    -   šunka
        
    -   žampiony
        
    -   olivy
        
-   `Button` s textem **Vytvořit objednávku**
    
-   `TextBlock` pro zobrazení výsledku
    

## Po kliknutí na tlačítko

Vypiš shrnutí objednávky, například:

**Jan Novák si objednal velkou pizzu. Přídavky: sýr navíc, olivy.**

Pokud není zaškrtnutý žádný doplněk, vypiš:

**Bez přídavků.**

## Rozšíření

Dopočítej i cenu:

-   malá: 120 Kč
    
-   střední: 150 Kč
    
-   velká: 190 Kč
    
-   každý doplněk: +20 Kč
    

---

# 2\. Registrace na školní kroužek

## Zadání

Vytvoř formulář pro přihlášení do školního kroužku.

Aplikace bude obsahovat:

-   `TextBox` pro jméno a příjmení
    
-   `DatePicker` pro datum narození
    
-   skupinu `RadioButton` pro výběr kroužku:
    
    -   programování
        
    -   robotika
        
    -   grafika
        
-   `CheckBox`:
    
    -   mám vlastní notebook
        
    -   souhlasím s pravidly kroužku
        
-   `Button` **Odeslat přihlášku**
    
-   `TextBlock` pro výstup
    

## Po kliknutí na tlačítko

Zobraz shrnutí přihlášky.

Například:

**Eva Malá se přihlásila do kroužku robotika. Vlastní notebook: ano. Souhlas s pravidly: ano.**

## Podmínka

Pokud není zaškrtnutý `CheckBox` **souhlasím s pravidly kroužku**, aplikace místo shrnutí vypíše upozornění:

**Přihlášku nelze odeslat bez souhlasu s pravidly.**

---

# 3\. Nastavení vzhledu aplikace

## Zadání

Vytvoř jednoduché okno s nastavením aplikace.

Aplikace bude obsahovat:

-   skupinu `RadioButton` pro výběr motivu:
    
    -   světlý
        
    -   tmavý
        
    -   modrý
        
-   `CheckBox`:
    
    -   zapnout zvuky
        
    -   zobrazovat tipy při spuštění
        
    -   automatické ukládání
        
-   `Button` **Uložit nastavení**
    
-   `TextBlock` pro vypsání zvoleného nastavení
    

## Po kliknutí na tlačítko

Vypiš text, například:

**Zvolený motiv: tmavý. Zapnuté volby: zvuky, automatické ukládání.**

Pokud není zaškrtnutý žádný `CheckBox`, vypiš:

**Žádné doplňkové volby nejsou zapnuté.**

## Rozšíření

Změň podle vybraného `RadioButton` barvu pozadí okna nebo některého prvku.