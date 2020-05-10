# 2. Procesory pro PC

## Charakteristika a parametry procesorů IBM-PC kompatibilní

### i8086
- první v r. 1969 od Intelu - Intel 4004 - 4bit s fr. 108 KHz
- v r. 1977
- první 16bit proc.
- zpětně kompatibilní s i8080
- první s architekturou x86
- 16b vnitřní architektura
- 16b datová sběrnice
- 20b adresní sběrnice
- umí adresovat až 2^20 (1MiB) operační paměti

#### Adresovaní v reálném modu
- skladá se ze dvou 16b složek - segment, offset
```
segment	A 8 F 3 0 	- 16 - proto se posune
offset    2 4 5 E
  	    A B 3 8 E => zápis - segment:offset => A8F3:245E

	- vznikne výsledná fyzická 20b adresa -> segment x 16 + offset
```

### i286
- Frekvence 6 – 25Mhz 
- První setup BIOS
- v r. 1981
- 130 000 tranzistorů
- 16b procesor 16b datovou a 24b adresní sběrnicí
- umožňuje práci ve dvou režimech
- realný režim
  - plně kompatibilní s procesorem 8086
  - 20b adresa (může adresovat 1MiB operační paměti)
  - tvoří se stejně jako u 8086

- chraněný režim
  - nový režim, nekompatibilní s 8086
  - adresa se tvoří ze dvou 16b složek (selektor a offset) za pomoci tabulek 
  - vysledná adresa je 24b (16MiB ram)

### i386

- 1983
- Frekvence 16-40 Mhz
- první Multitasking
- první Použítí cahce na zákl. Desce
- prvni 32b procesor
- 32b datová a 32 adresní sběrnice
- 275 000 tranzistorů
- umí 3 režimy
- reálný - stejný jako 8086
- chraněný režim
  - výsledná adresa je 32b (4GiB op. pam.)
  - adresa se tvoří ze selektoru a offsetu
  - je rozšířeny o strankovaní - převádí to lineární adresu ve vzdálené paměti na fyzickou adresu
- virtuální režim
  - funguje podobně jako 8086
  - možnost virtualní paměti 1MB, může uložit kdekoli do 4GiB adresního prostoru


### i486

**Prakticky i80386, ale s FPU**
- optimalizovaná 386 s interní cache a numerický koprocesor 80387
- 32bitovy procesor, 32bit adresní sběrnice, 32bit datová sběrnice
- 1,25 milionů tranzistorů
- spálená historie -> 80487 - že vyráběly z plnohodnotných CPU mat. koprocesory tím, že v nich něco spálili
- byli i procesory 80486 dx2 a dx4


### Intel Pentium

1991, D-Bus – 64b, A-Bus – 32b, Frekvence 60 – 200Mhz

Má dvě větve ALU – výkon má tedy 2x větší, ale na stejné frekvenci
- Pentium
- 3,1 milionů tranzistorů
- rok 1993
- napájecí napětí -> 3,3V
- 32bit procesor, 64bit datová sběrnice, 32bit adresní sběrnice
- 1 superskalární procesor -> 10x - během 1 taktu udělá 2 instrukce naraz
- obsahuje 16KiB cache paměti
- rozdělená na:
  - 8 KiB na data
  - 8 KiB na insturkce

### Pentium Pro
- pro servery, výkonné pracovní stanice
- rok 1995

##### Pentium MMX
- rozšířeni instrukcní sady
- pro multimediální výpočty
- rok 1997
- technologie SIMD

### AMD K5

1997 Během 1. taktu dvě instrukce, dynamické přepínání skoku, Pipelining – Postupně se instrukce
zpracovává více jednotkami

### Pentium 2

1997, PAE – Page address extension, f = 233 – 500 Mhz, A – Bus = 32 b +4 PAE, D-Bus = 64b
Cache již v pouzdru CPU L1 i L2, L1 u jádra (stejná frekvence), L2 mimo (½ frekvence)

- odlehčená verze - Celeron - bez L2 cache, pase 128Kib L2 cache

### Pentium 3

1999, f = až 1.4 Ghz, D – bus = 64b, A -bus = 32 + 4
- rozšíření instrukční sady SSE
```
- ID na internetoch - každý procesor měl jedinečné ID a byl dohledatelný, 
byla kolem toho nějaká aféra podle Pilčíka **Merge comment: FACT CHECK NEEDED**
```

### Pentium 4

2001, HyperThreading – rychlé přepínání mezi dvěmi sadami registrů, frekvence až 3.6GHz,
d-bus - 64b, a-bus – 32 +4 b
- SSE2

### Intel CORE

2006+, D-bus i A - bus 64b, frekvence až 4-5 GHz

- Core 2
  - duo - 2 jádra
  - quad - 4 jádra
  - menší taktovací frekvence

Core i
  - 64bit, více jádrové
  - i3 - 2 jádra, hyperthreading
  - i5 - 4 jádra
  - i7 - 4 jádra, hyperthreading
  - variabilní taktovaní jader
 
### AMD
- 386 - napájení 3,6V, pro notebooky
- 486
- K5 - proti Pentiu, vydaný se zpožděním, pomalý v FPU operacích, neuspěšný
- K6 - AMD koupilo firmu Next Gen která ho vyvinula, vykonný procesor
- K6-2 - rozšíření 3D Now!
- K7 - nová architektura, 3 FPU, prodávaný jako Athlon
- K8 - AMD Hammer / Athlon 64 / Opheron - pro servery

## Paměťový prostor, cache, módy činnosti

### Paměťový prostor

Dělí se na paměť uživatelskou, paměť systémovou, a paměť dat. Do uživatelské paměti se ukládá
uživatelský program. Tato paměť bývá typu EPROM nebo EEPROM a mívá kapacitu řádově od
desítek kB až po jednotky MB u modulárních programovatelných automatů, u kompaktních
programovatelných automatů spíše v desítkách kB. V systémové paměti je umístěn systémový
program. Tato paměť bývá rovněž typu EPROM. V paměti dat, která musí být typu RAM (RWM), jsou
umístěny uživateli dostupné uživatelské registry, zápisníkové registry (merkery, flagy), čítače, časovače
a většinou i vyrovnávací registry pro obrazy vstupů a výstupů. Počet těchto registrů výrazně ovlivňuje
možnosti programovatelného automatu. Adresovatelný prostor vymezený pro vstupy/výstupy omezuje
počet připojitelných periferních jednotek. Důležitým parametrem jsou i rozsahy čítačů a časovačů.

### Cache

Cache (též mezipaměť) je v informatice označení pro hardwarovou nebo softwarovou součást počítače,
která uchovává data a tím následující přístup k těmto datům může být rychlejší. Od vyrovnávací paměti
(bufferu) se cache liší tím, že může poskytovat data v ní uložená opakovaně (zatímco vyrovnávací
pamětí data pouze procházejí). Použití termínu cache a vyrovnávací paměť může být zaměňováno,
protože obě funkce mohou splývat.

Cache je tvořena (relativně) rychlou pamětí, která je však dražší. Proto má cache menší velikost, než
úložný prostor, ke kterému zrychluje přístup. Optimalizací úspěšného využití cache lze dosáhnout
vyššího výkonu zařízení (počítače). Hardwarovou cache najdeme v mikroprocesorech nebo pevných
discích. Cache může být softwarově vytvořena v operační paměti.


### Módy činnosti

#### Chráněný

##### Ochrana paměti

Chráněný režim přináší podporu ochrany paměti, která umožňuje přidělit běžícímu procesu určitý úsek
operační paměti a znemožnit, aby mohl zasahovat mimo tento vymezený prostor. Umožňuje tím zavést
multitasking (v paměti může být najednou více procesů).

##### Privilegovaný režim

Privilegovaný režim umožňuje zajistit, aby neprivilegované procesy nemohly měnit nastavení, která
byla provedena v privilegovaném režimu. Jádro operačního systému běží v privilegovaném režimu a
všechny ostatní procesy v neprivilegovaném. Tak jádro neztratí nad počítačem kontrolu a jen jádro
může procesům přidělovat a odebírat systémové prostředky, ukončovat je, vynucovat změnu kontextu,
rozhodovat o dostatečném oprávnění k provedení určité činnosti atd.

##### Virtualizace paměti

Dále chráněný režim přináší pokročilou správu operační paměti, která spočívá v podpoře virtuální
paměti pomocí stránkování, což usnadňuje provozování multitaskingu.

##### Virtualizace systému

Chráněný režim přináší také možnost virtualizace, takže uvnitř jednoho systému (hypervizor) lze
provozovat jiný systém (virtualizovaný), který bude mít dojem, že má počítač jen pro sebe (je však pod
kontrolou hypervizoru).

##### Zpětná kompatibilita

Procesory podporující chráněný režim zachovávají kvůli zpětné kompatibilitě i podporu staršího
reálného režimu. To umožnilo používat již existujícího software (jak aplikační software, tak i operační
systém DOS nebo starší Microsoft Windows).

Procesory rodiny x86 se dodnes z důvodu zpětné kompatibility spouštějí nejprve v reálném režimu a do
chráněného režimu musí být teprve přepnuty, což moderní operační systémy (Microsoft Windows,
Linux, macOS, ...) dělají při bootování hned po aktivaci jádra.

#### Reálný

Reálný mód neboli režim reálných adres (anglicky real mode, real address mode) je v informatice
základní režim mikroprocesorů z rodiny x86. Rozlišuje se až od řady Intel 80286, kdy byl uveden
chráněný režim, ale fakticky odpovídá jedinému pracovnímu režimu starších mikroprocesorů Intel
8086 a Intel 80186. To je také důvod, proč procesory z rodiny x86 (včetně nejmodernějších 64bitových
procesorů x86-64) dodnes z důvodu zpětné kompatibility začínají svůj běh právě v reálném módu a do
jiného režimu je musí explicitně přepnout jádro operačního systému.


Typickými vlastnostmi režimu reálných adres je segmentace paměti s 20bitovou adresací (tedy
nanejvýš 1 MiB přímo adresovatelné paměti) a neomezený přímý přístup do celé paměti i ke všem
perifériím. Nelze tedy zajistit spolehlivé fungování multitaskingu.

##### Adresace

Adresa je v režimu reálných adres určena dvěma registry: segmentovým a offsetovým. Fyzická adresa
je vypočítána jako součet hodnoty v segmentovém registru vynásobené 16 (tedy posunuté o 4 bity
doleva) a hodnoty v offsetovém registru.

Díky přenosu tak může být výsledkem až 21bitové číslo: šestnáctkově 0xFFFF0 + 0xFFFF =
0x10FFEF. Pro 21. bit bylo do standardu IBM PC zavedeno rozšíření, které umožňovalo 21. adresní bit
aktivovat řadičem klávesnice. Na procesorech Intel 80286 a novějších, které měly širší adresní sběrnici,
bylo toto chování emulováno softwarově. Adresy nad hranicí 1 MiB (přesněji do adresy 1 MiB + 64
KiB – 16 bajtů, tj. do adresy 1114095) byly označovány jako HMA (high memory area) a bylo do nich
možné umístit například část systému DOS a uvolnit tak místo v konvenční paměti.

##### Přepínání do reálného režimu

Záměrem firmy Intel při zavádění režimu chráněné virtuální paměti bylo, aby v tomto režimu v
budoucnu běžely všechny operační systémy i jejich programy. Tomu odpovídala i podpora přepínání
režimů: zatímco pro přepnutí z reálného režimu do chráněného dal Intel k disposici snadný postup,
druhým směrem žádný snadný způsob nepřipravil a na procesorech řady 80286 bylo jediným
způsobem resetovat procesor.

Protože režimy se podstatně liší a programy napsané pro jeden z nich je potřeba upravit, aby běžely v
druhém, bylo vzhledem k množství programů pro reálný režim zpočátku nereálné, aby se od jeho
používání zcela upustilo. Řešením bylo používat ono resetování procesoru, byť se jedná o poměrně
nezvyklou a časově náročnou operaci. Při resetování samotného procesoru totiž nedochází ke smazání
paměti a při správném ošetření tedy může operační systém přepnout tam i zpět bez následků.

## Přerušení, přímý přístup do paměti

### Přerušení

Přerušení (anglicky interrupt) je v informatice metoda pro asynchronní obsluhu událostí, kdy procesor
přeruší vykonávání sledu instrukcí, vykoná obsluhu přerušení, a pak pokračuje v předchozí činnosti.
Původně přerušení sloužilo k obsluze hardwarových zařízení, které tak signalizovaly potřebu obsloužit
(tj. odebrat z vyrovnávací paměti vstupně-výstupního zařízení data nebo do ní další data nakopírovat,
odtud označení vnější přerušení). Později byla přidána vnitřní přerušení, která vyvolává sám procesor,
který tak oznamuje chyby vzniklé při provádění strojových instrukcí a synchronní softwarová přerušení

vyvolávaná speciální strojovou instrukcí, která se obvykle používají pro vyvolání služeb operačního
systému.

- proces s vyšši prioritou si vyžádá přerušení, procesor nechá toho, co zrovna dělá a věnuje se prioritnímu procesu, jak ho dodělá, věnuje se tomu, který dělal předtím
- žádá se o čas procesoru
- generuje se IRQ (Interupt ReQuest) hardwarem počítače - generuje ho zařízení na sběrnici


### DMA – Přímý přítup do paměti

DMA (anglicky Direct Memory Access, tj. přímý přístup do paměti) je v informatice způsob přímého
přenosu dat mezi operační pamětí a vstupně/výstupními zařízeními. Data neprocházejí skrze procesor a
lze tak dosáhnout vyššího výkonu (během přenosu dat může procesor zpracovávat jiné strojové
instrukce). DMA se používá pro přenos větších objemů dat například řadič pevných disků, grafická
karta, síťová karta, zvuková karta a podobně. DMA je odchylkou od Von Neumannovy architektury
počítače.

#### Princip

Klasická komunikace se vstupně-výstupními zařízeními je realizována pomocí strojových instrukcí IN
(přenáší data ze zařízení do registru procesoru) a OUT (přenáší data z registru procesoru do zařízení),
které tato data (typicky slovo procesoru) přenášejí po datové sběrnici, a adresní sběrnice přitom slouží
k adresaci vstupně-výstupního zařízení (tzv.PIO přenosy). Z hlediska procesoru jsou vstupně-výstupní
zařízení velmi pomalá a procesor musí na reakci zařízení čekat, což velmi zpomaluje výpočetní
rychlost počítače.

DMA je řízené speciálním řadičem, který je součástí základní desky počítače. Přenášení velkých
objemů dat mezi vstupně-výstupními zařízeními a operační pamětí je pak řízeno DMA řadičem a
procesor je brzděn těmito přenosy jen částečně (při blokování sběrnice konfliktem přístupů do paměti)
a může vykonávat jinou činnost. Počítač tak má z hlediska uživatele větší výkon díky paralelizaci
(současnému vykonávání) přenosů dat a činnosti procesoru. Program nejprve řadič DMA naprogramuje
(pomocí několika instrukcí IN a OUT) a o další přenosy se již nemusí programátor starat. Dokončení
přenosu může být signalizováno přerušením, které aktivuje obsluhu přerušení, která může
naprogramovat řadič DMA na další přenosy.

## Zpracování instrukcí

### Jednoduché

Jedná se o následující stupně:

1.Instruction fetch – vyzvednutí instrukce
2.Decode – dekódování instrukce, zároveň se načítají registry
3.Execute – provedení instrukce
4.Access – čtení z paměti
5.Writeback – zápis výsledku do paměti

> 0) programový vstup pro zpracovaní
> 1) radic žádá vstupní zařízení o hodnoty
> 2) vstupni zarizeni prenese hodnoty do operacni pameti
> 3) řadič je informován o načtení dat
> 4) řadič žádá o přenos dat (instrukce) do ALU nebo do výstupního zařízení
> 5) odeslání dat z paměti do ALU nebo do výstupního zařízení
> 6) žádost o provedení instrukce v ALU nebo ve výstupním zařízení
> 7) uložení výsledku operace do operační paměti
> 8) ALU informuje řadič o doručení instrukce
> 9) předání výsledku výpočtu

### Zřetězené

Pipelining, zřetězené zpracování či překrývání strojových instrukcí je způsob zvýšení výkonu
procesoru současným prováděním různých částí několika strojových instrukcí. Základní myšlenkou je


rozdělení zpracování jedné instrukce mezi různé části procesoru a tím i umožnění zpracovávat více
instrukcí najednou. Fáze zpracování je rozdělena minimálně na 2 úseky:

1.Načtení a dekódování instrukce
2.Provedení instrukce a případné uložení výsledku
To vedlo k vytvoření procesoru složeného ze dvou spolupracujících subprocesorů, kdy každá část
realizuje danou fázi zpracování. Procesor má části – EU (Execution Unit) a BIU (Bus Interface Unit).
Zřetězení se stále vylepšuje a u novějších procesorů se již můžeme setkat stále s více řetězci
rozpracovaných informací. Z toho vyplývá, že je možno dokončit více než 1 instrukci za 1 hodinový
cyklus (takt procesoru).

Zřetězené zpracování je technika používaná při návrhu počítačů pro zvýšení jejich instrukčního
průchodu. Základní instrukční cyklus je rozdělen na série zvané vedení. Místo zpracovávání každé
instrukce postupně, každá instrukce je rozdělena na sled kroků, takže různé kroky mohou být vykonány
současně a paralelně (jiným okruhem).

Zřetězení zvyšuje instrukční průtok prováděním více operací současně, ale nesnižuje instrukční latenci
(čas pro provedení instrukce od začátku do konce), jelikož stále musí provést všechny kroky. Vskutku,
může to zvyšovat latenci kvůli přídavné režii z rozdělení výpočtů na oddělené kroky a hůře, zřetězení
se může zdržet, což dále zvyšuje latenci. Zřetězení tedy zvyšuje průtok za cenu latence a je často
používáno v CPU, ale nikoliv v realtime systémech, které jsou na latenci těžce závislé.

Každá instrukce je rozdělena do posloupnosti závislých kroků. Prvním krokem je vždy načtení
instrukce z paměti, posledním krokem je většinou zápis výsledku do registru nebo paměti. Zřetězení se
snaží umožnit procesoru pracovat na tolika instrukcích zároveň, kolik je závislých kroků, stejně jako
montážní linka sestavuje několik vozidel současně, místo aby čekala, až jedno projde celou linkou, než
začne s dalším. Stejně jako cílem montážní linky je udržet každou součást produktivní v každém
okamžiku, zřetězení chce udržet každou část procesoru zaneprázdněnou s nějakou instrukcí. Zřetězení
v počítači umožňuje, že čas cyklu je čas nejpomalejšího kroku a ideálně je v každém cyklu dokončena
jedna strojová instrukce.

Pojem pipeline je analogií faktu, že v potrubí je v každém úseku kapalina, stejně jako je každá část
procesoru zatížena prací.


## Jednotky Procesoru

ALU, FPU, Řadič – zajišťuje součinnost jednotlivých součástí procesoru , Vektorová jednotka –
matematický koprocesor, registry

## HyperThreading

Hyper-threading (oficiálně Hyper-Threading Technology, též HT Technology, HTT, HT) je v
informatice technologie používaná výrobcem procesorů Intel pro zjednodušené zajištění
vícevláknového paralelního zpracování strojových instrukcí. Technologie vytváří z jednoho
fyzického procesoru dva virtuální procesory tím, že jsou v něm aktivovány dvě řídicí jednotky.
Vůči softwaru systém představuje místo jednoho fyzického dva (logické) procesory. Hyper-
threading umožňuje lépe využít hardware procesoru, snížit odezvu systému (latenci), zrychlit
výpočty (systém s aktivovaným hyper-threadingem je podle typu výpočtů zhruba stejně rychlý
nebo až o třetinu rychlejší).

Rychle přepíná mezi dvěma sadami registrů.

## Možnosti zvětšování výkonu procesoru

- HyperThreading
- Superskalarita – některé jednotky jsou v procesoru víckrát
- Přetaktování,
- Rozšíření šířky slova – 32bit, 64bit
- zefektivnění mikrokódu
- Predigce skoků – jakési předvídání skoků. Základem je myšlenka, že skoky jsou většinou 	ve smyčkách a reagují na nějakou podmínku, která 10x vyjde a 1x nevyjde.
- pipelining - zpracování 2 instrukcí najednou
- přidání víc jader
  - na určité operace jsou vyhrazené a duplikované specializované části procesoru - FPU, ALU
  - instrukce nejdou zpracovávat paralelně - musí se počkat na dokončení rozpracované instrukce
- velikost procesorové cache - propojuje procesor s RAMkama

```
Autor: Jiří Jungwirth
Merger: Sádlík Kryštof
Datum: 7.5.2020
```
