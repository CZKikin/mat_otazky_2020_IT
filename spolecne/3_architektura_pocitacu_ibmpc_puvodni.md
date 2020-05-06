# 3. Architekrura IBM-PC

## Historický přehled

1981 – první IBM PC – 8088 @ 4.55Mhz, až 64MB RAM, záznam na 5“ disketu

1987 – IBM PS/2 – VGA, 80386, záznam na 3,5“ disketu, PS/2 rozhraní a SIMM

90‘s – cdrom, pentium, 1024x768, zvukovka a modem, inkoustovky

2000‘s – USB, Ethernet, WiFi, bluetooth, PCI-E, DVD, SATA

2010‘s – SSD

## FormFaktory

Definice rozměrů a potřeb napájení počítače

AT – napájení přímo do desky – buď teče nebo ne

Atx – vždy pod malým proudem, zapne se uzemněním vodiče PS_ON

### AT

Nahradil XT. Od 286 do PenII. Napájecí zdroj měl 2x šesti pin konektory p_8 a p_9. Zapojovalil se do
jednoho 12pin konektoru ČERNOU k sobě! Jediné I/O je na klácesnicu (DIN).

### Atx

Od PenII až do včil, zdroj má 24pin (starý enem 20). Narozdíl od AT už má větší I/O.

## Hlavní komponenty PC

### CPU

Central processing unit, procesor – vykonává instrukce

Frekvence, počet jader a vláken, počet pci-e linek, potřeba

### GPU

Graphics processing unit – specializovaný mikroprocesor pro grafické výpočty


frekvence, počet grafických jader, grafická paměť, spotřeba

### Ram

Random access memory – rychlá polovodičová paměť

Frekvence, typ, kapacita

### Zdroj

PSU – power supply unit – mění střídavé napětí na napětí použité počítačem

Výkon, formfaktor

### Základní deska

Motherboard – deska jenž propojuje všechny periferie mezi sebou

poečet Pci-e, I/O, formfaktor

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

### PCI

Není lokální, je připojena přes mezisběrnicový můstek. Je 64 bitová (support pro 32bit mode).
Frekvence je 33Mhz. Support pro Plug&Play.

### PCI-e

1.0 - až 8GB/s

2.0 – až 16GB/s


3.0 – až 32GB/s

4.0 – 64GB/s

5.0 – by měla nabízet 64GB/s na jedné lince takže až 128GB/s – možné problémy s kompatibilitou
starých karet

## Čipové sady

Starají se o komunikaci mezi procesorem, BUS, řadiči, a MB. Nyní InputOutputHub → SuperI/O.

Předtím rozdělení na Severní a Jižní most.

## BIOS

Basic Input Output System

Základní osahávání HW, POST – power on self test dále řídí OS. CMOS pamět – baterka v PC – drží
info v biosu a drží hodiny

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
