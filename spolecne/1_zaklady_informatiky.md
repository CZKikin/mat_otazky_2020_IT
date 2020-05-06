# 1. Základy Informatiky

## Číselné soustavy

Dvojková, osmičková, desítková a šestnáctková.

### Dvojková

Nabývá hodnot 0 a 1. Používaná v informatice z důvodu lehce rozdělitelným stavům.

Převod:
|    | |
|----|-|
|0000|0|
|0001|1|
|0010|2|
atd...

### Šestnáctková

Nabývá hodnot 0-9 a A-F. Používá se v informatice, kvůli zpříjemnění pro programátory.
|   |     |
|---|-----|
|0-9|0-9  |
|A-F|10-15|
`0x10 = 16(dec)`

## Jednotky používané v informatice

```
1 bit – základní jednotka informace - 1 nebo 0
1 B (byte) = 8 bitů
1 kB = 1000 b
1 kiB = 2^10 B = 1024 B
1 MiB = 2^20 B = 1 048 576
```
atd.

## Data a informace

### Informace

Informaci lze definovat jako zmenšení neurčitosti jevu. Lze ji vysílat, přijímat, uchovávat a zpracovávat. Informace, které zpracovává počítač jsou (prozatím) několika druhů:

- textové informace (texty, programy...)
- obrazové informace (fotografie, grafiky, video, animace...)
- zvukové informace (zvuky, hudba...)

U informací posuzujeme jejich:

- aktuálnost
- relevanci - adekvátnost potřebě. Informace je relevantní, je-li v ní obsaženo to, co potřebujeme vědět.
- pravdivost - soulad se skutečností

### Data

Data jsou nekódované informace.

### Signál

Signál je nositel informace (dat).

## Přímý kód

První možný způsob jak vyjádřit záporné číslo - vyčlenění prvního bitu jako znaménkového bitu. Pokud například binární číslo
00000001 vyjadřuje jedničku, pak 10000001 označuje −1.

Tento způsob ale komplikuje algoritmy pro praktické počítání – pro sčítání a odčítání jsou potřeba
odlišné algoritmy a nejprve je vždy třeba testovat znaménkový bit a podle výsledku provést sčítání
nebo odčítání. Další nevýhodou je, že existují dvě reprezentace čísla nula – kladná nula a záporná nula.
Proto byl později pro záznam záporných čísel zaveden doplňkový kód.

## Zakódování informace

**Kódování informace v informatice**

Veškeré informace uloženy v souborech, kódovány pomocí číslic 0 a 1. Soubory s informací kódovanou známým způsobem jsou opatřeny známou příponou a zpracovávány programy, které 
toto kódování znají.

## Propustnost

Je veličina, která říká, jaké množství dat je možné přenést za jednotku času. V toto číslo se může reálně
měnit. Udává se v bitech či bytech za sekundu.

## Typy přenosů dat

### Analogový a digitální přenos

Analogový přenos je přenos spojitého proměnného signálu, digitální komunikace je přenos diskrétních
zpráv. Tyto zprávy jsou buďto reprezentovány sledem impulsů prostřednictvím linkového kódu
(základní pásmo) nebo omezeným počtem lineárních průběhů (přeložené pásmo), a to za použití
digitální modulace. Modulace přeloženého pásma a odpovídající demodulace (nebo také detekce) se
provádí prostřednictvím modemu. Podle nejběžnější definice digitálního signálu jsou oba signály –
základního i přeloženého pásma, které jsou reprezentovány bitovými toky, považovány za digitální
vysílání. Naproti tomu jiná alternativní definice považuje pouze signál v základním pásmu jako
digitální a přenos přeloženého pásma digitálních dat jako formu digitálně-analogového převodu.
Přenášená data mohou být digitální zprávy pocházející z datového zdroje, jako například počítač nebo
klávesnice, ale také analogový signál, jako telefonní hovor nebo video signál, digitalizovaný do
bitového proudu (např. pomocí pulzně kódové modulace).

Digitální přenos nebo přenos dat tradičně patří do oblasti telekomunikací a elektrotechniky. Základní
principy přenosu dat mohou být pokryty v rámci počítačové vědy/techniky v oboru datové komunikace.
To zahrnuje také počítačové sítě, počítačové komunikační aplikace a síťové protokoly, například
směrování a meziprocesovou komunikaci. Ačkoli TCP ( _Transmission Control Protocol_ , tj. _protokol
řízeného přenosu_ ) zahrnuje pojem „přenos“, není TCP a jiné protokoly transportní vrstvy obvykle
popsán v učebnicích nebo v kurzech o přenosu dat, ale v počítačových sítích.


### Sériový a paralelní přenos

V telekomunikacích je sériový přenos sekvenční přenos signálu, zastupující znaky nebo jiný druh dat.
Digitální sériové přenosy jsou realizovány jako bity posílané přes jeden vodič nebo sekvenčně optickou
cestou. Vzhledem k tomu, že tento způsob nevyžaduje tolik práce se signálem (a existuje menší riziko
chyby než u paralelního přenosu), může být přenosová rychlost po každé jednotlivé cestě větší. To se
dá s výhodou použít na delší vzdálenosti pro kontrolní součet nebo paritní bit.

Paralelní přenos v oblasti telekomunikací znamená současný přenos signálního prvku znaků nebo
jiného druhu údajů. V digitální komunikaci je paralelní přenos současným přenosem souvisejících
signálních prvků přes dvě nebo více samostatných cest. Používá více vodičů, které mohou přenášet více
bitů současně, což umožňuje vyšší rychlost přenosu dat, než jaké lze dosáhnout pomocí sériového
přenosu. Tato metoda se používá interně v počítači, například pro vnitřní sběrnice, někdy i externě,
například u tiskáren. Hlavním problémem je „zkreslení“ (a přeslechy), protože vodiče při paralelním
přenosu mají (záměrně) mírně odlišné vlastnosti. Kvůli tomu mohou být některé bity přijaty dříve než
ostatní, což může poškodit zprávu. K řešení tohoto problému se nabízí paritní bit, nicméně paralelní
přenos na dlouhé vzdálenosti je stále méně spolehlivý, protože narušení přenosu je mnohem
pravděpodobnější.

## Takt a frekvence

Frekvence, neboli takt procesoru, je udáván v gigahertzech. Tedy udává, kolik se uděje cyklických dějů (výpočtů) za jednu sekundu.

```
Autor: Sloučeny práce Adama Kadlčíka a Kryštofa Sádlíka
Merger: Vít Staniček
Datum: 6.5.2020
```