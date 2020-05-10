# 3. Architekrura IBM-PC

## Historický přehled

### přehled počítačů obecně
Nultá generace (1930 – 1940)
Počítač s reléovými obvody. Hybnou silou vývoje nulté generace se stala 2SV – paralelně k velkému pokroku v různých částech světa.
Howard Aiken – Působil na Harvardu, PC Mark I – koncepce Harvardská

První generace (1945 – 1951)
Využívala elektronek, relé už jen zřídka. Počítače byly neefektivní, velmi drahé, vysoký příkon, velká poruchovost a velmi nízkou výpočetní rychlost.
1946 – PC ENIAC
John Von Neumann – přetvořil Eniac na Edvac – použil základy bin soustavy podle Leibnitze a Shannona.

Druhá generace (1951 – 1965)
Tranzistory, které dovolily zlepšit všechny parametry počítače (zmenšení rozměrů, zvýšení rychlosti a spolehlivosti, snížení energetických nároků). Bardeen, Brattan, Schockley – Bellovy laboratoře

Třetí generace (1965 – 1980)
Integrované obvody. S postupem času roste počet tranzistorů v integrovaném obvodu (zlepšuje se integrace). Multitasking proces (vykonávané programy se střídají). Integrovaný obvod – SSI, MSI, LSI…. 
SI=stupeň integrace
S = Small – méně než 10 tranzistorů M = Medium – 10 – 1000 tranz. L = Large - 1000 – 100 000 tranz.

Čtvrtá generace (od 1981)
Charakteristická mikroprocesory a osobními počítači. Mikroprocesory v jednom pouzdře obsahují celý CPU (dřívější procesory se skládaly z více obvodů) a jsou integrované s vysokou integrací, 
které umožnily snížit počet obvodů na základní desce, zvýšila se spolehlivost, zmenšily rozměry, zvýšila se rychlost a kapacita pamětí. S rozvojem počítačů sítí vzniká internet. VLSI = miliony tranz.

### přehled PC 
1981 – první IBM PC – 8088 @ 4.55Mhz, až 64MB RAM, záznam na 5“ disketu

1987 – IBM PS/2 – VGA, 80386, záznam na 3,5“ disketu, PS/2 rozhraní a SIMM

90‘s – cdrom, pentium, 1024x768, zvukovka a modem, inkoustovky

2000‘s – USB, Ethernet, WiFi, bluetooth, PCI-E, DVD, SATA

2010‘s – SSD

## FormFaktory

Definice rozměrů a potřeb napájení počítače

AT – napájení přímo do desky – buď teče nebo ne

Atx – vždy pod malým proudem, zapne se uzemněním vodiče PS_ON

Zdroje typu AT – zapínání na boku zdroje, není možné řídit spotřebu. Měly zapínací tlačítko napojené přímo do silové části napájecího zdroje.
Zdroje typu ATX – jiný způsob zapínání/vypínání. Zdroj není spojen přímo se zapínacím tlačítkem. 
To umožňuje zapínání počítače i jinými způsoby (Wake on LAN, Wake on RING, 
klávesnicí nebo myší). Přesto má mnoho napájecích zdrojů ATX na své 
zadní straně klasický vypínač. Tím se počítač skutečně vypne a softwarové zapnutí 
pak není možné. Pokud je tento vypínač zapnutý, PC stále spotřebovává energii, i když vypadá jako vypnutý.


### AT

Nahradil XT. Od 286 do PenII. Napájecí zdroj měl 2x šesti pin konektory p_8 a p_9. Zapojovalil se do
jednoho 12pin konektoru ČERNOU k sobě! Jediné I/O je na klácesnicu (DIN).

### Atx

Od PenII až do včil, zdroj má 24pin (starý enem 20). Narozdíl od AT už má větší I/O.

### Koncepce PC
- John von Neumannovo schéma – používá 1 elektronickou paměť pro program i pro data
- Harvardská architektura – používá oddělenou paměť pro data a pro program
Současné PC nejsou konstruovány ani podle jedny architektury. Univerzální PC obsahují jen 1 paměť, 
do které se umísťují programy i zpracovávaná data, avšak procesor umožňuje paměť obsahující program označit jen pro čtení, 
a naopak část paměti, která obsahuje data označit tak, že nelze vykonávat strojové instrukce, které jsou v ní 
uloženy.

## Hlavní komponenty PC

### CPU

Central processing unit, procesor – vykonává instrukce

Procesor základní součást počítače, která vykonává strojový kód 
spuštěného počítačového programu. Ten je složen z jednotlivých strojových instrukcí, 
které jsou uloženy v operační paměti počítače. Procesor je v současnosti velmi složitý 
sekvenční integrovaný obvod umístěný na základní desce počítače.

Frekvence, počet jader a vláken, počet pci-e linek, potřeba

### GPU

Graphics processing unit – specializovaný mikroprocesor pro grafické výpočty

frekvence, počet grafických jader, grafická paměť, spotřeba

### Ram

Random access memory – rychlá polovodičová paměť

Frekvence, typ, kapacita

### Zdroj

PSU – power supply unit – mění střídavé napětí na napětí použité počítačem

Slouží ke zpracování střídavého napětí dodávaného ze sítě na nízké napětí potřebné napájení 
komponent počítače. Některé zdroje mají přepínač pro změnu vstupního napětí mezi 230 V a 115 V, 
ostatní se automaticky přizpůsobí jakémukoli napětí v tomto rozsahu. Nejčastěji dodávané počítačové 
zdroje spadají do standardu ATX.

Výkon, formfaktor

### Základní deska

Motherboard – deska jenž propojuje všechny periferie mezi sebou

Obsahuje většinu elektronických částí počítače. Hlavním účelem základní desky je propojit jednotlivé součástky počítače do fungujícího celku 
a poskytnout jim elektrické napájení. Typická základní deska umožňuje zapojení procesoru, operační paměti. 
Další komponenty (např. grafické a zvukové karty, pevné disky, mechaniky) se připojují pomocí rozšiřujících slotů nebo kabelů, 
které se zastrkávají do příslušných konektorů.
Na základní desce je dále umístěna energeticky nezávislá paměť ROM, ve které je uložen systém BIOS, který slouží k oživení 
počítače hned po spuštění. Nejdůležitější integrované obvody jsou zabudovány v čipové sadě (chipset). 
Fyzicky může jít buď jenom o jeden čip, nebo dva (v tom případě se označují jako northbridge a southbridge). Čipová sada rozhoduje, jaký procesor a 
operační paměť je možné k základní desce připojit.


počet Pci-e, I/O, formfaktor

### SSD/HDD

Solid State Drive / Hard Drive – Úložistě pro trvalá data

kapacita, rychlost, u HDD počet otáček

### Skříň

Místo pro uložení komponentů

airflow, I/O, antidust filtr

## Sběrnice

### ISA

Je 8-bit PC Bus, později 16bit. Má paralelní zapojení. Sync s cpu (8mhz) pokud CPU_F > BUS_F →
generátor čekacích taktů. Lokální sběrnice.

1982, paralelní, 16b, frekvence 7-12MHz, propustnost=20MB/s, dnes se na zákl. desce nevyskytuje.

### PCI

Není lokální, je připojena přes mezisběrnicový můstek. Je 64 bitová (support pro 32bit mode).
Frekvence je 33Mhz. Support pro Plug&Play.
1992, paralelní, verze 2.01996-3.02010, 128MB/s, Bus mastering – možnost zařízení řídit provoz na sběrnici.

### PCI-e
2003, firma INTEL, sériová, f= 2,5GHz(v1.1), 5GHZ(v2.0), prop.=f x 1b x 2 směry[b/s]  (PCIE x1)

1.0 - až 8GB/s

2.0 – až 16GB/s

3.0 – až 32GB/s

4.0 – 64GB/s

5.0 – by měla nabízet 64GB/s na jedné lince takže až 128GB/s – možné problémy s kompatibilitou
starých karet

## Čipové sady

Starají se o komunikaci mezi procesorem, BUS, řadiči, a MB. Nyní InputOutputHub → SuperI/O.

Předtím rozdělení na Severní a Jižní most.

Dříve byly na zákl. desce samostatné integrované obvody – řešící svůj vlastní přidělený problém: řadič sběrnice, řadič paměti, řadič DMA, řadič IRQ, časovač, čítač, RTC, BIOS
Čipová sada se stará o komunikaci periferií s procesorem – sběrnice, sloty, řadiče a dalším součástky na základní desce.
Mezi nejznámější producenty čipů patří: NVIDIA, AMD, VIA Technologies, SiS a Intel.
U počítačů tento termín obvykle označuje 2 čipy na základní desce – tzv. northbridge (česky severní můstek) a tzv. southbridge (česky jižní můstek). V dnešní době northbridge a southbridge výrobce někdy implementuje do 1 čipu – funkci obou zastupuje jeden čip. 

U ještě novějších zařízení jsou funkce severního mostu přímo integrovány do procesoru a k procesoru je připojen pouze “Jižní most” s jeho standardními periferiemi (HDD, BIOS, USB…) 

Chipset je většinou určen pro konkrétní rodinu mikroprocesorů.

## BIOS

Basic Input Output System

Základní osahávání HW, POST – power on self test dále řídí OS. CMOS pamět – baterka v PC – drží
info v biosu a drží hodiny
BIOS (Basic Input Output System) nejzákladnějšího programu počítače. Funkcí BIOSu je řízení celého systému – zajišťuje komunikaci jednotlivých komponent počítače (hardwaru) s čipsetem základní desky a operačním systémem (OS) – propojuje hardware se softwarem.

BIOS nabízí nejenom změny pro urychlení chodu počítače, tedy zvýšení výkonu PC. Pro nastavování, změnu a ukládaní údajů systému BIOS slouží program setup.

Během několika počátečních sekund při probíhající detekci počítače (spouštění) stačí ve většině případů 
zmáčknout klávesu delete. Jednotliví výrobci BIOSů si však vyhrazují právo na různé způsoby vstupu do programu 
Setup, tedy jinou klávesu.

POST – 1. první instrukce pípne

2. kontrola prvních 64Kib paměti
3. Kontrola řadičů, chipsetu
4. Vyhledávání dalších BIOSů
5. Předá kontrolu jiným BIOSům
6. Zjištění kapacity RAM
7. Vyhledávání úložišť
8. Předání kontroly OS

## Realizace RAM

RAM (Random access memory) je polovodičová rychlá paměť používána na dočasné uložení dat. Je
elektronicky závislá. FAP (Fyzický paměťový prostor) se jeví jako souvislý prostor buněk. Tyto buňky
jsou pak lineárně adresovány.

SRAM – Statická RAM

DRAM – Dynamická

DDR – Double data rate

Ecc – error corection code – kontrola bloku dat paritním bitem


## Pevné disky

Jsou energeticky nezávislá úložiště. Jsou částečně mechanické, jiné jsou polovodičové

#### HDD – Hard Drive

Je magnetický disk. Ukládá na plotny, který adresuje na cylindr, hlava a sektor. Je velmi náchylný na
vibrace → v případě nutnosti zaparkuje čtecí hlavu. S příchodem větších kapacit se přešlo na LBA –
logic block addressing – spojení do clusterů (několik sektorů dohromady)

#### SSD - Solid state disk
SSD postupem času nahradily pevné disky a umožnily řadu nových aplikací, jako digitální fotoaparáty a kamery, mobilní telefony, GPS a podobně., často ve tvaru paměťových karet. Používají stejné rozhraní SATA, pro vyšší přenosové rychlosti PCI-Express, popřípadě ATA v rozhraní PCMCIA, ExpressCard a podobně (tj. stejný konektor i typ komunikace).

Výhody:
- SSD nemají mechanické pohyblivé části
- mají rychlejší přístup k datům
- dosahují vyšších přenosových rychlostí
- nevydávají hluk atd.
- jsou mnohem menší a lehčí

##### Buňky SSD
Víceúrovňová buňka je v elektronice paměťový prvek schopný ukládat více než jeden bit informace, 
ve srovnání s jednoúrovňovou buňkou (SLC), která může uložit pouze jeden bit v paměťovém prvku. 
Trojúrovňové buňky (TLC) a čtyřúrovňové buňky (QLC) jsou verzí MLC paměti, která může ukládat v 
buňce 3 a 4 bity. Na základě konvence, označení „víceúrovňová buňka" , bývá často přirovnáváno k „dvojúrovňové buňce", 
což je mírně zavádějící.

Hierarchie pamětí je setříděna následovně:

SLC (1 bit v buňce) – nejrychlejší, nejvyšší cena, největší životnost
MLC (2 bity v buňce)
TLC (3 bity v buňce)
QLC (4 bity v buňce) – nejpomalejší, nejlevnější, největší životnost

```
Autor: Roman Skalík
Merger: Sádlík Kryštof
Datum: 7.5.2020
```
