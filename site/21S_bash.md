# 21. Interpret BASH

**Bash (Bourne Again SHell)** je interpret příkazů (shell) projektu. Shell představuje základní rozhraní pro komunikaci uživatele s operačním systémem počítače. Jeho základní funkcí je spouštění zadaných příkazů a programů, 
navíc poskytuje řadu vlastních příkazů umožňujících efektivní práci se systémem.

Bash je tedy možné používat:
- interaktivně (realizuje příkazovou řádku operačního systému), nebo
- jako interpret skriptů

V interaktivním režimu čte bash příkazy ze standardního vstupu (od uživatele) místo ze souboru, 
jinak je jeho chování v obou režimech stejné

## Pravidla pro Bash skripty
Skript v jazyce bash je textový soubor obsahující příkazy jazyka bash, oddělené novou řádkou, nebo středníkem. Na první řádku (opravdu to musí být první řádka, tzn. před hlavičkou NESMÍ být ani prázdná řádka) skriptu je vhodné napsat hlavičku, která umožní rozpoznat, že se jedná o skript a jakým jazykem má být skript interpretován. Na operačním systému Linux bude mít tato hlavička tvar:  `#!/bin/bash`
Znaky **#!** na začátku první řádky říkají, že se jedná o skript, za nimi následuje plná cesta k interpretu příkazů (v našem případě `/bin/bash`). Zde je vhodné si uvědomit, že po přenesení skriptu na jiný systém, kde se interpret bashe nachází v jiném adresáři (např. ve FreeBSD to může být `/usr/local/bin/bash`) nemusí skript fungovat podle předpokladu. Hlavička je důležitá v případě, že skript spouštíme pouze zadáním jeho cesty (skript musí být v tomto případě nastaven jako spustitelný). Pokud spouštíme skript jako argument příkazu bash, např.: `/bin/bash ./muj_skript.sh`
Hlavička není pro spuštění nezbytná. Přesto je vhodné ji do souboru uvést pro pozdější jednoduchou identifikaci, o jaký soubor se jedná.

## Proměnné
Bash **nemá** datové typy proměnných - resp. s obsahem proměnné se vždy pracuje jako s řetězcem. Proměnná je identifikována názvem, který se může skládat z malých a velkých písmen anglické abecedy, podtržítek a číslic, přičemž nesmí číslicí začínat. Názvy proměnných jsou case-sensitive, což znamená, že promenna a PROMENNA jsou dvě různé proměnné.
Přiřazení hodnoty proměnné se provádí operátorem =, např.  A=24
Řazení do proměnné A řetězec "24". Při přiřazování je důležité myslet na to, že před operátorem = ani za ním nesmí být mezera, jinak je příkaz interpretován chybně.
Pokud potřebujeme pracovat s hodnotou proměnné (předat ji jako parametr, nebo přiřadit jako hodnotu do jiné proměnné), musíme proměnnou zapsat jako znak $ + název proměnné, tedy např.: echo $A # výpis obsahu proměnné na standardní výstup
Alternativní způsob zápisu využívá složené závorky kolem názvu proměnné: 
``` bash
echo ${A}
```
To je výhodné, pokud např. bezprostředně za hodnotou proměnné následují znaky, které by jinak byly považovány za součást názvu proměnné: 
``` bash 
echo x$Ax # vytiskne znak "x" + hodnotu proměnné "Ax"
echo x${A}x # vytiskne znak "x" + hodnotu proměnné "A" + znak "x"
```

## Pole
Kromě obyčejných proměnných umožňuje bash pracovat s poli. Pole vytvoříme buď deklarací příkazem declare -a POLE, který vytvoří prázdné pole, nebo přímo přiřazením prvků pole do proměnné. Prvky pole se zapisují do kulatých závorek: 
`PRAZDNE_POLE=() # vytvoření prázdného pole v proměnné PRAZDNE_POLE`
`BARVY=(cervena zelena modra) # vytvoření pole se třemi prvky "cervena", "zelena" a "modra" v proměnné BARVY`
Při přístupu k prvkům pole se používá zápis: 
```bash
${BARVY[0]} # vrátí první položku pole
```
Přičemž v hranatých závorkách je číselný index položky, číslování je od 0. Pokud bychom na index a hranaté závorky zapomněli, dostaneme první prvek pole (tzn. $BARVY vrátí stejnou hodnotu jako ${BARVY[0]}). Následující zápisy nám umožní zjistit délku pole (počet položek), nebo získat všechny položky pole najednou:
```bash
${#BARVY[*]} # vrátí počet položek pole BARVY
${BARVY[*]} # vrátí všechny položky pole BARVY jako jeden řetězec, ve kterém jsou položky pole vzájemně odděleny mezerou
${BARVY[@]} # vrátí všechny položky pole BARVY samostatně (pro správnou funkci je potřeba správně použít uvozovky)
```
Přidávat prvky k existujícímu poli můžeme např. operátorem += : BARVY+=(cerna bila)

## Export
Viditelnost proměnné v bashi je omezena na instanci interpretu vykonávajícího aktuální skript. Pokud chceme hodnotu proměnné přenést do synovského procesu (pokud spouštíme z jednoho skriptu jiný skript), můžeme použít příkaz
```bash
export PROMENNA
```
kterým říkáme, že se má proměnná zkopírovat do proměnných spuštěných procesů. V běžných programech spuštěných z aktuálního skriptu jsou takovéto proměnné viditelné jako "proměnné prostředí".

## Uvozovky
Řetězce v bashi je důrazně doporučeno uzavírat do uvozovek, ačkoliv to syntaxe jazyka striktně nevyžaduje. Uvozovky pomohou především v případech, kdy obsah proměnné OBSAHUJE MEZERY nebo některé znaky se zvláštní interpretací. Podívejme se na příklad:
```bash
A="text s mezerami"
program $A
program "$A"
```
Pokud bychom vynechali uvozovky u přiřazení do proměnné A, obdržíme zřejmě chybové hlášení o neznámém příkazu "s" - interpret nemá jak odlišit zda se jedná o pokračování řetězce, nebo příkaz který chcete spustit s přednastavenou proměnnou A na hodnotu "text". Druhá řádka se interpretuje jako
program text s mezerami
což znamená, že spuštěný program obdrží tři samostatné argumenty "text", "s" a "mezerami", což zřejmě není náš záměr. Třetí řádek pracuje tak, jak požadujeme, tj. předá programu jediný argument bez ohledu na jeho obsah.
Pokud budu chtít předat celé pole jako parametry spuštěného programu (každý prvek jako samostatný argument), musím výraz ${POLE[@]} uzavřít do uvozovek: program "${POLE[@]}"
jinak mezery v řetězcích způsobí rozdělení řetězce na více samostatných argumentů.

## Apostrofy
Bash umožňuje uzavírat řetězce kromě "dvojitých uvozovek" také do 'apostrofů', přičemž základní rozdíl mezi nimi je ten, že uvnitř apostrofů se neprovádí překlad proměnných na jejich hodnoty, tedy např.: echo "Obsah promenne je $A" vytiskne hodnotu proměnné, ale echo 'promenna $A' vytiskne řetězec "promenna $A". Uvozovky a apostrofy můžeme jinak s výhodou zaměňovat, pokud potřebujeme vytvořit řetězec obsahující právě apostrof nebo uvozovky.

## Výstup a formátovaný výstup
Běžící skript má, stejně jako každý jiný proces, k dispozici svůj standardní vstup, výstup a chybový výstup, jejichž prostřednictvím si vyměňuje data s jinými procesy nebo uživatelem. Nejjednodušší způsob výpisu řetězce na standardní výstup umožňuje příkaz echo. Častěji však využíváme výstupu jiných programů spuštěných z našeho skriptu - pokud jejich výstup explicitně nepřesměrujeme, je automaticky přesměrován na výstup procesu běžícího skriptu. 

## Aritmerické a logické operace
Proměnné v bashi jsou řetězce. Pokud do proměnné uložíme celé číslo, uloží se jako řetězec jednotlivých dekadických číslic. Příkaz expr umí převést zadané řetězcové argumenty na čísla a provádět s nimi základní aritmeticé operace. Výsledek výpočtu vypisuje expr na standardní výstup. 


Operace|Znak
---|---
Sčítání|\+
Odčítání|\-
Násobení|\*
Dělení|/
Dělení modulo|%

Při zadávání parametrů příkazu expr je nutné důsledně oddělovat mezerami operátory a operandy, jinak je příkaz nerozpozná správně. Volání externího příkazu expr není v rámci skriptu příliš pohodlné a přehledné, proto bash nabízí zkrácený zápis 
```bash
$(( výraz )) … A=$(( A+1 ))
```
Další možnosti aritmetických výpočtů nabízí vnitřní příkaz bashe let. Poskytuje navíc mj. logické a bitové operátory a operátory inkrementace a dekrementace. Inkrementaci proměnné je možné zapsat velmi úsporně let A++

## Testování hodnot
Test vrací (stejně jako jiné příkazy) hodnotu 0, pokud vše proběhlo v pořádku, tj. vyhodnocovaná podmínka je platná. Hodnotu 1 vrací tehdy, když podmínka neplatí. Vzniká tak trochu paradoxní situace, kdy pro Bash je 0 pravda a 1 nepravda. S tím si ale nemusíme příliš lámat hlavu. Dobré může být vědět, že když dojde k chybě (např. špatná syntaxe), vrací test návratový kód 2.
Ukažme si funkci příkazu test na příkladu. Budeme zjišťovat existenci souboru `/etc/passwd`. K tomu u příkazu test slouží přepínač -e. Výsledek ověříme vypsáním hodnoty proměnné PIPESTATUS. Potom zkusíme totéž se souborem `/var/passwd`, který většinou neexistuje:

```bash
test -e /etc/passwd
echo $PIPESTATUS
0
test -e /var/passwd
echo $PIPESTATUS
1
```

- -b soubor - existuje a je to blokový speciální soubor;
- -c soubor - existuje a je to znakový speciální soubor;
- -d soubor - existuje a je to adresář;
- -e soubor - existuje;
- -f soubor - existuje a je to normální soubor;
- -g soubor - existuje a má právo set-group-id;
- -k soubor - existuje a má nastavený sticky bit;
- -L soubor - existuje a je to symbolický odkaz;
- -p soubor - existuje a je to pojmenovaná roura (FIFO);
- -r soubor - existuje a je čitelný;
- -s soubor - existuje a má délku větší než nula;
- -S soubor - existuje a je to soket;
- -u soubor - existuje a má nastaven set-user-id bit;
- -w soubor - existuje a je zapisovatelný;
- -x soubor - existuje a je proveditelný;
- -O soubor - existuje a je vlastněný efektivním user id;
- -G soubor - existuje a je vlastněný efektivním group id.

## Podmínky
Podmínky jsou v bashi realizovány příkazem if, jehož syntaxe je 
```bash
if <příkaz>
  then  <příkaz1>  <příkaz2>  ...
else  <příkaz3>  ...
fi
```
Za klíčovým slovem if následuje příkaz, který je spuštěn, a na základě jeho návratové hodnoty probíhá interpretace kódu prováděním příkazů za klíčovým slovem then (návratová hodnota 0), nebo else (nenulová návratová hodnota). Blok "else" je nepovinný. 

## Cykly
Bash nabízí tři druhy cyklů: for, while a until.
Cyklus for slouží k procházení seznamu hodnot a jeho syntaxe je
```bash
for PROMENNA in seznam_hodnot
  do  <příkaz>  ...
 done
```
Příkaz for postupně přiděluje řetězce ze seznamu (pole nebo řetězec hodnot oddělených IFS) do proměnné PROMENNA a pro každé přiřazení vykoná seznam příkazů uvnitř bloku do ... done.
Cykly while a until mají shodnou syntaxi a rozdíl mezi nimi je pouze ve vyhodnocení podmínky:
```bash
while <příkaz> # nebo until <příkaz>
   do  <příkaz>  ...
  done
```
Na začátku každého průchodu cyklem se spustí příkaz následující klíčové slovo while resp. until. Rozdíl mezi nimi je ten, že cyklus while pokračuje, dokud je návratová hodnota spuštěného příkazu nulová, cyklus until pokračuje, dokud je návratová hodnota nenulová.
Uvnitř všech cyklů (tedy uvnitř bloku do ... done) je možné používat příkazy pro řízení průchodu cyklem break a continue. Příkaz break způsobí okamžité ukončení cyklu. Příkaz continue přeskočí zbytek příkazů uvnitř cyklu a skočí zpět na začátek cyklu.

## Konstrukce funkcí
Definice funkce v jazyce bash je možná dvěma způsoby:
```bash
function nazev_funkce {<příkaz>  ...}
nazev_funkce() {  <příkaz>    ...}
```
Funkce nemá pevný počet parametrů. K jednotlivým parametrům se uvnitř funkce dostanete přes proměnné $1, $2, atd., podobně jako mimo funkce pracujete s parametry skriptu. Analogicky se uvnitř funkce chovají proměnné $#, $\*, $@ a příkaz shift. Návratová hodnota funkce je dána návratovou hodnotou posledního příkazu. Provádění funkce je možné ukončit příkazem return, jehož nepovinným parametrem je návratová hodnota.
Funkce se volá prostým uvedením jejího jména, následovaného parametry, stejně jako se volá externí program nebo skript.

## Signály
Signály jsou prostředek k jednoduché komunikaci mezi procesy na unixových systémech. Každému procesu lze poslat signál, přičemž máme-li dostatečné oprávnění, proces na něj zareaguje. Pomocí signálů lze proces ukončit, pozastavit, přerušit, atd. Ovšem signál může vyvolat i jinou akci – programátoři mají možnost signály ve svých programech obsluhovat nebo ignorovat. Například když programu přijde signál 15 (tj. TERM – ukončit), tak lze naprogramovat to, aby se nejdříve uložila načatá práce a teprve potom se program ukončil.
Signály mají přiřazená čísla i názvy. Signály jsme si kdysi pojmenovali nejen proto, abychom si nemuseli pamatovat čísla, ale také proto, že čísla se na různých systémech mohou lišit. Vyjmenujeme a popíšeme si několik používanějších signálů.
Názvy signálů vždy začínají řetězcem „SIG“ (jako signál), takže chceme-li ukončit proces signálem, tak říkáme, že mu posíláme SIGTERM.


ČÍSLO|NÁZEV|ZJEDNODUŠENÝ POPIS
---|---|---
1|HUP (Hangup)|Tento signál proces obdrží tehdy, když je uzavřen jeho řídící terminál.
2|INT (Interrupt)|Toto je signál, který proces obdrží, když běží v terminálu a uživatel stiskne Ctrl+C. Obvykle ukončí proces.
3|QUIT|Ukončí proces a zapíše stav paměti, se kterou program pracoval (tzv. core dump).
4|ILL(Illegal instruction)|Tento signál posílá operační systém, když proces vyvolá neznámou instrukci.
8|FPE(Floating point exception)|Tímto signálem jádro trestá programy, které se snaží dělit nulou, atp.
9|KILL(Kill)|„Zabije“ proces (okamžitě). Nelze obejít.
10|USR1(User-defined)|Uživatelsky definovaný signál.
11|SEGV(Segmentation fault)|Obvykle posílá operační systém programům, které chybně pracují s pamětí.
15|TERM(Terminate)|Ukončí proces.
19|STOP|Zastaví proces. Nelze obejít.
20|TSTP(Terminal stop)|Zastaví proces, ale lze obejít. Tento signál proces obdrží, když běží interaktivně v shellu a uživatel stiskne Ctrl+Z.
18|CONT(Continue)|Obnoví běh procesu po obdržení některého ze dvou předchozích signálů.

```
Autor: Svatava Malatinská
Merger: Sádlík Kryštof
Datum: 29.5.2020
```
