# 8. Multimedia

## Zvuk
- Mechanické vlnění
- Člověk vnímá 16 Hz až 20 000 Hz, <16 Hz = infrazvuk, >20 000 Hz = ultrazvuk
- Rychlost zvuku: 340 m/s
- Vákuum je zvukovou izolací
- K reprodukci zvuku slouží reproduktory nebo sluchátka

## PRINCIP DIGITALIZACE ZVUKU

Analogový zvukový signál (signálové napětí) je přiveden do takzvaného A/D (analog/digital)
převodníku, jenž je součástí zvukové karty a ten ho převede do digitální podoby (na odpovídající číslo).
Tento proces se nazývá vzorkování. Je samozřejmé, že existuje mnoho způsobů takovéhoto převodu, a
že výsledná kvalita bude záviset právě na použitém způsobu, neboli na rozlišení převodníku. Pro
charakteristiku rozlišení převodníku jsou důležité dva faktory. Prvním z nich je vzorkovací kmitočet,
jemuž se taky někdy říká horizontální rozlišení. Toto číslo nám udává rychlost vzorkování (sampling
rate), neboli říká, kolikrát za sekundu počítač změří a zaznamená okamžitou hodnotu analogového
signálu. Vznikne tzv. aproximovaná funkce. Je tedy jasné, že digitální zvuk nikdy nemůže dokonale
napodobit zvuk analogový, protože průběh „mezi vzorky“ je prostě neznámý. Pro správnou funkci D/A
(Digital/Analog) převodníku, jež zpětně rekonstruuje digitální záznam do analogové formy (abychom
si hudbu mohli poslechnout), je podle tzv. vzorkovacího teorému třeba, aby frekvence vzorkování byla
alespoň dvakrát větší než nejvyšší frekvence vzorkovaného signálu. Jinak řečeno, při nejvyšším
přenášeném kmitočtu budou z každé periody odebrány právě dva vzorky. Protože lidské ucho je
schopno slyšet zvuk o maximální frekvenci asi 20 kHz, běžně používaný vzorkovací kmitočet je 44,1
kHz. Toto je také důvod, proč někteří lidé tvrdí, že digitální zvuk „deformuje výšky“. Při tomto
kmitočtu budou pro výšky nad 12 kHz odebrány 4 až 2 vzorky za periodu, což může být málo pro
jejich věrnou rekonstrukci. Zjednodušeně to lze vidět na obrázku 2, kdy pro dva různé zvuky jsou
zaznamenány identické vzorky. Dříve se používalo i poloviční, 22,05 kHz vzorkování. Pro nižší,
rozhlasovou, kvalitu s rozsahem do 15 kHz se používá vzorkování 32 kHz, naopak pro vyšší věrnost
reprodukovaného zvuku existují i vzorkování 48 kHz nebo dokonce 192 kHz. V tomto případě ale
zlepšení kvality už moc rozpoznatelné není, naopak se zvyšují nároky na místo na záznamovém médiu.
Druhý extrém jsou telefony, kde se používá vzorkování 8 kHz. Kmitočet Zvuková kvalita
digitalizovaného zvuku Šířka slova 8 bitů 11 kHz Velice nízká zvuková kvalita 22 kHz Lepší, ale ne o
moc 44 kHz Kvalita je v pořádku, ale pro tento kmitočet se většinou používá šířka slova 16 a více.
Šířka slova 16 bitů 11 kHz Odpovídá to průměru 22 kHz Dobrá kvalita 44 kHz Pokud je stereo, rovná
se CD kvalitě. Tabulka 1 Druhou důležitou charakteristikou A/D převodníku je šířka slova, neboli
vertikální rozlišení. Je to číselné vyjádření okamžité zvukové hladiny. Přesnost tohoto čísla závisí na
počtu bitů, jež použijeme k jejímu zapsání. Čím více bitů, tím více můžeme zaznamenat zvukových
intenzit a zvuk se pak jeví dynamičtější. Pro kvalitní záznam používaná šestnáctibitová šířka slova tak
pro zápis použije 16 bitů, což dovoluje rozlišit 216 neboli 65 536 napěťových úrovní. Tato hodnota
dovoluje zaznamenat zvuk o dynamickém rozsahu 96 dB. Pokud by byla max. amplituda vyšší, tak se
prostě digitálně odřízne. V telefonech se využívá 8-bitové rozlišení, naopak pro velmi kvalitní záznamy
i 24 až 32-bitové rozlišení. Obr. 3 Na obrázku 3 je názorně vidět jak vypadá digitalizovaný zvuk, jehož
výslednou kvalitu v závislosti na použitém vzorkovacím kmitočtu a šířce slova shrnuje tabulka 1. Takto
získaný zvuk z A/D převodníku se označují jako RAW data (nezpracovaná, 3 čistá data). Pro jejich
další použití je však nutno je uložit v určitém formátu

## ZVUKOVÉ FORMÁTY

Pro to, aby se se zvukovými soubory dalo manipulovat (aby se daly přenášet, rozpoznat a přehrát),
musí být tyto soubory opatřeny hlavičkou. Ta musí obsahovat údaje o délce záznamu, o rychlosti
přehrávání (resp. sample rate), o počtu bitů na jeden vzorek a informace o typu záznamu, což může být
buď mono nebo stereo. Zvukové formáty se dělí na ztrátové (např. MP3) a bezztrátové (WAV).

### BEZZTRÁTOVÝ FORMÁT WAVE (.WAV)

WAV je formát pro ukládání audiodat pro Windows, a proto je velmi rozšířený a podporuje ho většina
programů pro práci se zvukem. Umožňuje jednoduchou manipulaci a editaci zvuku. Vzorky ukládá bez
zvláštních úprav, takže zachovává vysokou kvalitu zvuku. Na druhou stranu jsou z tohoto důvodu WAV
soubory poměrně objemné a tím pádem ne moc praktické pro jejich masivnější ukládání (i když při
dnešních kapacitách HDD to přestává být problém) a pro sdílení přes Internet


### ZTRÁTOVÉ KOMPRESNÍ FORMÁTY

Jak už bylo řečeno, běžně používaná kvalita záznamu zvuku je 16-bitová šířka slova při vzorkovacím
kmitočtu 44,1 kHz, samozřejmě ve stereo kvalitě. Jedna sekunda zvuku tak zabere 44 100 2 2 = ⋅⋅
176 400 bajtů, jedna minuta pak 10 584 000 bajtů... Proto byly vytvořeny ztrátové kompresní formáty,
které využívají toho, že spoustu uložených dat lidské ucho vůbec neslyší a další změny při vhodném
zamaskování přeslechne. Na druhou stranu je samozřejmé, že pokud pracují např. s pouhou desetinnou
(i menší částí) zaznamenaných dat, nemohou dosáhnout původní kvality. Tabulka 2 Existuje několik
typů těchto formátů, jimž se také říká codec (od compress/decompress – každý data komprimuje a
dekomprimuje poněkud odlišným způsobem). Nejznámější je formát MP3 (viz dále), další pak např.
RA/RM (Real Audio) používaný k přenosu dat přes Internet, WMA (Windows Media Audio), VQF,
OGG Vobis a další...

## Pojmy grafiky

Pixel: je zkratka anglického PICture Element, tedy obrazový bod.

Velikost obrázku: na monitoru – v obrazových bodech - počet obrazových bodů, ze kterých je ✗
obrázek sestaven (např. 800 x 600 px)

✗ na disku – datová velikost - v Bajtech a jeho násobcích (např 356 kB)

✗ na papíře - v délkových jednotkách (počet obrazových bodů / rozlišení x 2,54 = velikost obrázku v
cm)
Rozlišení obrázku: je veličina, která má význam pouze při tisku obrázku. Udává, z kolika pixelů bude
vyskládána délka 1 palce (2,54 cm) při tisku. Je to vlastně hustota obrazových bodů. Udává se v DPI
(dots per inch, tedy bodů na palec).

✗ pro monitor stačí rozlišení 72 – 90 dpi

✗ pro kvalitní tisk minimálně 300 dpi

Rozlišení monitoru: počet obrazových bodů na šířku krát počet obrazových bodů na výšku monitoru.
(Např. 1 280 x 1 024 bodů.)

Rozlišení fotoaparátu: celkový počet obrazových bodů, ze kterých je schopen fotoaparát sestavit
fotografii při nejvyšší kvalitě. Např 10 Mpx (2592 x 3888 px).

RGB: zkratka Red, Green, Blue

Histogram jasu obrázku: Je graf zobrazující četnost pixelů pro celou škálu jasů od 0 (černé) po 225
(bílou) v obrázku.

(histogramy lze vytvořit i pro jednotlivé barvy RGB)

jas (brightness) – celková světlost obrázku

kontrast – rozdíl mezi nejtmavším a nejsvětlejším bodem obrázku


sytost barvy (saturace): čistota barvy;

Rastová a Vektorová grafika

### Formáty grafiky

Jpeg, gif, bmp – rastrová

SVG, CDR, AI – vektor

MP4, avi, - video

## Pravidla pro trvorbu prezentace
- Prezentace je pouze doplňkový materiál, na každý snímek max. 5 odrážek(max 5 slov)
- Má především podtrhnout fakta
- Myšlenky zformulovat do klíčových hesel, při prezentaci je dále rozvést

### Šablony, multimediální objekty a jejich využití

#### Šablona 
- Vzor nebo plán snímku, případně skupiny snímků (barvy, písma, efekty…)
- Může obsahovat konkrétní tematický obsah, formátování pozadí

#### Multimediální objekty 

- Využití k reklamním účelům, předvedení výrobků, služeb, doprovodný předmět k přednáškám, 
oživují jakékoliv vystoupení
```
Autor: Adam Vrána
Merger: Sádlík Kryštof
Datum: 6.5.2020
```
