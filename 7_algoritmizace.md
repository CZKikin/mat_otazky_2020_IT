# 7. Algoritmizace.......................................................................................................................................

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
