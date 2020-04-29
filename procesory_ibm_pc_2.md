# 2. Procesory pro PC...................................................................................................................................

## Charakteristika a parametry procesorů IBM-PC kompatibilní..............................................................

### i

1982, A-Bus -24b, D-Bus – 16b, Frekvence – 6 – 25Mhz, První setup BIOS

### i

1983, A-Bus 32b, D-Bus 32b, Frekvence 16-40 Mhz, 1. Multitasking, 1. Použítí cahce na zákl. Desce

### i

Prakticky i80386, ale s FPU

### Intel Pentium.....................................................................................................................................

1991, D-Bus – 64b, A-Bus – 32b, Frekvence 60 – 200Mhz + 16 KiB

Má dvě větve ALU – výkon má tedy 2x větší, ale na stejné frekvenci

### AMD K

1997 Během 1. taktu dvě instrukce, dynamické přepínání skoku, Pipelining – Postupně se instrukce
zpracovává více jednotkami

### Pentium 2..........................................................................................................................................

1997, PAE – Page address extension, f = 233 – 500 Mhz, A – Bus = 32 b +4 PAE, D-Bus = 64b

Cache již v pouzdru CPU L1 i L2, L1 u jádra (stejná frekvence), L2 mimo (½ frekvence)

### Pentium 3..........................................................................................................................................

1999, f = až 1.4 Ghz, D – bus = 64b, A -bus = 32 + 4

### Pentium 4..........................................................................................................................................

2001, HyperThreading – rychlé přepínání mezi dvěmi sadami registrů, frekvence až 3.6GHz,

d-bus - 64b, a-bus – 32 +4 b

### Intel CORE.......................................................................................................................................

2006+, D-bus i A - bus 64b, frekvence až 4-5 GHz


## Paměťový prostor, cache, módy činnosti..............................................................................................

### Paměťový prostor.............................................................................................................................

Dělí se na paměť uživatelskou, paměť systémovou, a paměť dat. Do uživatelské paměti se ukládá
uživatelský program. Tato paměť bývá typu EPROM nebo EEPROM a mívá kapacitu řádově od
desítek kB až po jednotky MB u modulárních programovatelných automatů, u kompaktních
programovatelných automatů spíše v desítkách kB. V systémové paměti je umístěn systémový
program. Tato paměť bývá rovněž typu EPROM. V paměti dat, která musí být typu RAM (RWM), jsou
umístěny uživateli dostupné uživatelské registry, zápisníkové registry (merkery, flagy), čítače, časovače
a většinou i vyrovnávací registry pro obrazy vstupů a výstupů. Počet těchto registrů výrazně ovlivňuje
možnosti programovatelného automatu. Adresovatelný prostor vymezený pro vstupy/výstupy omezuje
počet připojitelných periferních jednotek. Důležitým parametrem jsou i rozsahy čítačů a časovačů.

### Cache................................................................................................................................................

Cache (též mezipaměť) je v informatice označení pro hardwarovou nebo softwarovou součást počítače,
která uchovává data a tím následující přístup k těmto datům může být rychlejší. Od vyrovnávací paměti
(bufferu) se cache liší tím, že může poskytovat data v ní uložená opakovaně (zatímco vyrovnávací
pamětí data pouze procházejí). Použití termínu cache a vyrovnávací paměť může být zaměňováno,
protože obě funkce mohou splývat.

Cache je tvořena (relativně) rychlou pamětí, která je však dražší. Proto má cache menší velikost, než
úložný prostor, ke kterému zrychluje přístup. Optimalizací úspěšného využití cache lze dosáhnout
vyššího výkonu zařízení (počítače). Hardwarovou cache najdeme v mikroprocesorech nebo pevných
discích. Cache může být softwarově vytvořena v operační paměti.


### Módy činnosti...................................................................................................................................

#### Chráněný......................................................................................................................................

##### Ochrana paměti.......................................................................................................................

Chráněný režim přináší podporu ochrany paměti, která umožňuje přidělit běžícímu procesu určitý úsek
operační paměti a znemožnit, aby mohl zasahovat mimo tento vymezený prostor. Umožňuje tím zavést
multitasking (v paměti může být najednou více procesů).

##### Privilegovaný režim................................................................................................................

Privilegovaný režim umožňuje zajistit, aby neprivilegované procesy nemohly měnit nastavení, která
byla provedena v privilegovaném režimu. Jádro operačního systému běží v privilegovaném režimu a
všechny ostatní procesy v neprivilegovaném. Tak jádro neztratí nad počítačem kontrolu a jen jádro
může procesům přidělovat a odebírat systémové prostředky, ukončovat je, vynucovat změnu kontextu,
rozhodovat o dostatečném oprávnění k provedení určité činnosti atd.

##### Virtualizace paměti..................................................................................................................

Dále chráněný režim přináší pokročilou správu operační paměti, která spočívá v podpoře virtuální
paměti pomocí stránkování, což usnadňuje provozování multitaskingu.

##### Virtualizace systému...............................................................................................................

Chráněný režim přináší také možnost virtualizace, takže uvnitř jednoho systému (hypervizor) lze
provozovat jiný systém (virtualizovaný), který bude mít dojem, že má počítač jen pro sebe (je však pod
kontrolou hypervizoru).

##### Zpětná kompatibilita...............................................................................................................

Procesory podporující chráněný režim zachovávají kvůli zpětné kompatibilitě i podporu staršího
reálného režimu. To umožnilo používat již existujícího software (jak aplikační software, tak i operační
systém DOS nebo starší Microsoft Windows).

Procesory rodiny x86 se dodnes z důvodu zpětné kompatibility spouštějí nejprve v reálném režimu a do
chráněného režimu musí být teprve přepnuty, což moderní operační systémy (Microsoft Windows,
Linux, macOS, ...) dělají při bootování hned po aktivaci jádra.

#### Reálný..........................................................................................................................................

Reálný mód neboli režim reálných adres (anglicky real mode, real address mode) je v informatice
základní režim mikroprocesorů z rodiny x86. Rozlišuje se až od řady Intel 80286, kdy byl uveden
chráněný režim, ale fakticky odpovídá jedinému pracovnímu režimu starších mikroprocesorů Intel
8086 a Intel 80186. To je také důvod, proč procesory z rodiny x86 (včetně nejmodernějších 64bitových
procesorů x86-64) dodnes z důvodu zpětné kompatibility začínají svůj běh právě v reálném módu a do
jiného režimu je musí explicitně přepnout jádro operačního systému.


Typickými vlastnostmi režimu reálných adres je segmentace paměti s 20bitovou adresací (tedy
nanejvýš 1 MiB přímo adresovatelné paměti) a neomezený přímý přístup do celé paměti i ke všem
perifériím. Nelze tedy zajistit spolehlivé fungování multitaskingu.

##### Adresace..................................................................................................................................

Adresa je v režimu reálných adres určena dvěma registry: segmentovým a offsetovým. Fyzická adresa
je vypočítána jako součet hodnoty v segmentovém registru vynásobené 16 (tedy posunuté o 4 bity
doleva) a hodnoty v offsetovém registru.

_Související informace naleznete také v článku High memory area._

Díky přenosu tak může být výsledkem až 21bitové číslo: šestnáctkově 0xFFFF0 + 0xFFFF =
0x10FFEF. Pro 21. bit bylo do standardu IBM PC zavedeno rozšíření, které umožňovalo 21. adresní bit
aktivovat řadičem klávesnice. Na procesorech Intel 80286 a novějších, které měly širší adresní sběrnici,
bylo toto chování emulováno softwarově. Adresy nad hranicí 1 MiB (přesněji do adresy 1 MiB + 64
KiB – 16 bajtů, tj. do adresy 1114095) byly označovány jako HMA (high memory area) a bylo do nich
možné umístit například část systému DOS a uvolnit tak místo v konvenční paměti.

##### Přepínání do reálného režimu..................................................................................................

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

## Přerušení, přímý přístup do paměti.......................................................................................................

### Přerušení...........................................................................................................................................

Přerušení (anglicky interrupt) je v informatice metoda pro asynchronní obsluhu událostí, kdy procesor
přeruší vykonávání sledu instrukcí, vykoná obsluhu přerušení, a pak pokračuje v předchozí činnosti.
Původně přerušení sloužilo k obsluze hardwarových zařízení, které tak signalizovaly potřebu obsloužit
(tj. odebrat z vyrovnávací paměti vstupně-výstupního zařízení data nebo do ní další data nakopírovat,
odtud označení vnější přerušení). Později byla přidána vnitřní přerušení, která vyvolává sám procesor,
který tak oznamuje chyby vzniklé při provádění strojových instrukcí a synchronní softwarová přerušení


vyvolávaná speciální strojovou instrukcí, která se obvykle používají pro vyvolání služeb operačního
systému.


### DMA – Přímý přítup do paměti.....................................................................................................

DMA (anglicky Direct Memory Access, tj. přímý přístup do paměti) je v informatice způsob přímého
přenosu dat mezi operační pamětí a vstupně/výstupními zařízeními. Data neprocházejí skrze procesor a
lze tak dosáhnout vyššího výkonu (během přenosu dat může procesor zpracovávat jiné strojové
instrukce). DMA se používá pro přenos větších objemů dat například řadič pevných disků, grafická
karta, síťová karta, zvuková karta a podobně. DMA je odchylkou od Von Neumannovy architektury
počítače.

#### Princip........................................................................................................................................

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

## Zpracování instrukcí...........................................................................................................................

### Jednoduché.....................................................................................................................................

Jedná se o následující stupně:

1.Instruction fetch – vyzvednutí instrukce
2.Decode – dekódování instrukce, zároveň se načítají registry
3.Execute – provedení instrukce
4.Access – čtení z paměti
5.Writeback – zápis výsledku do paměti

### Zřetězené.........................................................................................................................................

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


## Jednotky Procesoru..............................................................................................................................

ALU, FPU, Řadič – zajišťuje součinnost jednotlivých součástí procesoru , Vektorová jednotka –
matematický koprocesor

## HyperThreading...................................................................................................................................

**Hyper-threading (oficiálně Hyper-Threading Technology, též HT Technology, HTT, HT) je v
informatice technologie používaná výrobcem procesorů Intel pro zjednodušené zajištění
vícevláknového paralelního zpracování strojových instrukcí. Technologie vytváří z jednoho
fyzického procesoru dva virtuální procesory tím, že jsou v něm aktivovány dvě řídicí jednotky.
Vůči softwaru systém představuje místo jednoho fyzického dva (logické) procesory. Hyper-
threading umožňuje lépe využít hardware procesoru, snížit odezvu systému (latenci), zrychlit
výpočty (systém s aktivovaným hyper-threadingem je podle typu výpočtů zhruba stejně rychlý
nebo až o třetinu rychlejší).**

Rychle přepíná mezi dvěma sadami registrů.

## Možnosti zvětšování výkonu procesoru..............................................................................................

Pipelining, HyperThreading, Superskalarita – některé jednotky jsou v procesoru víckrát, Přetaktování,
Rozšíření šířky slova – 32bit, 64bit, více jader, zefektivnění mikrokódu
