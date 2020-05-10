# 7. Algoritmizace

Algoritmus je přesný návod či postup, kterým lze vyřešit daný typ úlohy. Pojem algoritmu se nejčastěji
objevuje při programování, kdy se jím myslí teoretický princip řešení problému (oproti přesnému zápisu v
konkrétním programovacím jazyce). Obecně se ale algoritmus může objevit v jakémkoli jiném vědeckém
odvětví. Jako jistý druh algoritmu se může chápat i např. kuchařský recept. Zpravidla však na algoritmy
klademe určitá omezení.

V užším smyslu se slovem algoritmus označují takové postupy, které splňují některé silnější požadavky:

**_Elementárnost_**
Algoritmus se skládá z konečného počtu jednoduchých (elementárních) kroků.
**_Konečnost_** **(finitnost)**
Každý algoritmus musí skončit v _konečném_ počtu kroků. Tento počet kroků může být libovolně velký (podle
rozsahu a hodnot vstupních údajů), ale pro každý jednotlivý vstup musí být konečný. Postupy, které tuto
podmínku nesplňují, se mohou nazývat _výpočetní metody_. Speciálním příkladem nekonečné výpočetní
metody je _reaktivní proces_ , který průběžně reaguje s okolním prostředím. Někteří autoři však mezi
algoritmy zahrnují i takovéto postupy.
**_Obecnost (hromadnost, masovost, univerzálnost)_**
Algoritmus neřeší jeden konkrétní problém (např. „jak spočítat 3×7“), ale obecnou třídu obdobných
problémů (např. „jak spočítat součin dvou celých čísel“), má širokou množinu možných vstupů.
**_Determinovanost_**
Algoritmus je determinovaný, pokud za stejných podmínek (pro stejné vstupy) poskytuje stejný výstup. Tato
vlastnost je požadována u velké části úloh; existují však úlohy, kdy je naopak vyžadována náhodnost
(například simulace vrhu kostkou, míchání karet, generování hesel a šifrovacích klíčů); na standardních
počítačích je dosažení náhodnosti obtížné. Pravděpodobnostní algoritmy v sobě mají zahrnutu náhodu a
nemusí být determinované.
**_Determinismus_**
Každý krok algoritmu musí být _jednoznačně_ a _přesně_ definován; v každé situaci musí být naprosto zřejmé,
co a jak se má provést, jak má provádění algoritmu pokračovat. Protože přirozené jazyky neposkytují
naprostou přesnost a jednoznačnost vyjadřování, byly pro zápis algoritmů navrženy programovací jazyky,
ve kterých má každý příkaz jasně definovaný význam. Vyjádření výpočetní metody v programovacím
jazyce se nazývá program. Některé algoritmy jsou sice determinované, ale nejsou deterministické
(například řadící algoritmus rychlé řazení s náhodnou volbou pivota).
**_Výstup_**


Algoritmus má alespoň jeden _výstup_ , veličinu, která je v požadovaném vztahu k zadaným vstupům, a tím
tvoří odpověď na problém, který algoritmus řeší (algoritmus vede od zpracování hodnot k výstupu)

## Diagram
Nejčastěji používaný grafický záznam algoritmu.
Pro zápis se používají ustálené grafické symboly.
![HDD](images/Diagram.png)

## Principy strukturovaného programování
Strukturované programování je programovací paradigma, 
které umožňuje rozložit program do funkcí. 
Strukturované programování neumožňuje vytvářet třídy, objekty atd. 
Proto když chceme upravit již vytvořenou funkci, musíme udělat funkci novou 
(dochází k opakování kódu).
Celý program se potom skládá z nezapouzdřených bloků kódu a špatně se udržuje. 
Každá úprava programu zvyšuje složitost, program potom nutně dojde do stavu, 
kdy náklady na přidávání nových funkcí vzrostou na tolik, že se program již 
nevyplatí rozšiřovat.

```py
def secti(a,b):
	return a+b

cislo1 = int(input("Zadej první číslo: "))
cislo2 = int(input("Zadej druhé číslo: "))
print(secti(cislo1, cislo2))
```
## OOP (Objektově orientované programování)
Jedná se o filozofii a způsob myšlení, designu a implementace, kde klademe důraz na znovupoužitelnost.
OOP programování se skládá z objektů a tříd. Objekty mají atributy (proměnné) a metody (funkce). Hlavními pilíři OOP jsou:
- zapouzdření (umožňuje skrýt některé metody a atributy tak, aby zůstaly použitelné jen pro třídu zevnitř – klíčová slova private, public)
- dědičnost (umožňuje využít již napsaný kód nějaké třídy a druhou třídu jen doplnit o další funkcionalitu)
- polymorfismus (umožňuje přepsat si metodu delejNeco() u každé podtřídy (v dědičnosti) tak, aby dělala, co chceme) 

![Polymorfizmus](images/oop_speak.png)
![Dědičnost](images/oop_model.png)

```py
class Kalkulacka:
	
	def secti(self, a, b):
		return a+b
		
kalkulacka = Kalkulacka()

cislo1 = int(input("Zadej první číslo: "))
cislo2 = int(input("Zadej druhé číslo: "))

print(kalkulacka.secti(cislo1, cislo2))

```

Konstruktor = metoda, která se volá po vytvoření instance třídy (objektu).

## Konstrukce jazyka Python
Pythonské odřazení musí být 4 mezery (tabulátor) - Pozor nestřídat -> Indentation error
### Podmínka
``` py
if podmínka:
	pass
	
elif další podmínka:
	pass
	
else:
	pass
```
	
### Cyklus
``` py
while podmínka:
	# dokud platí podmínka, cyklus běží
for i in range(číslo):
	# kolikrát cyklus proběhne udává číslo
for proměnná in pole:
	# obdoba foreach, zde prochází prvky pole
```
### Proměnná
Python má dynamické datové typy (před proměnnou se neudává datový typ, např. int)
Proměnná se vytvoří napsáním názvu proměnné, přiřazení hodnoty se vykoná použitím =
Např. cislo = 14, text = “ahoj“

### Vstupy
Vstup můžeme získat funkcí input(), pokud potřebujeme určit datový typ (např. int) napíšeme 
int(input())

### Výstupy  
V konzoli můžeme výstup realizovat pomocí funkce print(), např. print(cislo, text)
Funkci print() můžeme nastavit parametry end (co se udělá po vypsání, defaultně se odřádkuje) 
a sep (oddělovač jednotlivých vypisovaných proměnných)
``` py
print("Hello", "how are you?", sep="---")
```
> **OUTPUT**
> Hello---how are you?

### Procedury
Funkcím, které nic nevrací (jen něco udělají) se občas říká procedury. Např. print(). Pojem procedura se v Pythonu příliš nepoužívá.

### Funkce
Funkce se definují klíčovým slovem def. Funkce umožňují řešení problému rozdělit na podproblémy, nabízejí znovu použitelnost a zpřehledňují kód.
Pokud funkce něco vrací, využíváme k tomu slovo return. Do funkce můžeme dosadit parametry, ty se zadávají do závorky za název funkce.
```py
def mocnina(cislo):
    cislo = cislo ** 2
    return cislo
```

### Operátory Pythonu 
> == \
> \> \
> \< \
> \<= \
> \>= \
> != \
Slouží k porovnávání hodnot.

`is`
Porovná jestli obě proměnné odkazují na stejný objekt a ačkoliv mohou mít proměnné stejnou hodnotu, tak nemusí odkazovat na stejný objekt. \
`in`
Operátor in zjišťuje, zda-li je řetězec obsažený v jiném řetězci (lze použít i s jinými datovými typy). \
`not`
Vytváří negaci podmínky, lze použít s operátory is a in.

```
Autor: Jakub Šimurda
Merger: Sádlík Kryštof
Datum: 8.5.2020
```