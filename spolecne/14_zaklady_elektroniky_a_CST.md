# 14. Základy elektroniky a Číslicová technika

## Základní eliktrické veličiny

### Elektrický náboj
	
Elektrický náboj je fyzikální veličina (skalární) popisující jednu ze 
základních vlastností hmoty a vyjadřuje velikost schopnosti působit 
elektrickou silou. Nositeli elementárního elektrického náboje jsou 
stavební částice hmoty - protony (kladný náboj) 
a elektrony (záporný náboj). Elementární náboj má velikost 
**e = 1,602·10-19 C (coulomb).** 
Celkový elektrický náboj je vždy celočíselným násobkem elementárního 
náboje, je tedy kvantován a roven algebraickému součtu elektrických 
nábojů jednotlivých částí. Elektrický náboj nelze vyrobit ani zničit, 
pouze přemístit (zákon zachování elektrického náboje). 
Těleso s elektrickým nábojem je zdrojem elektrického pole, 
ve kterém se projevuje působení elektrické síly. 

Jednotkou elektrického náboje v soustavě SI je coulomb (C). 
Je to takové množství elektrického náboje, který projde za 1 sekundu 
průřezem vodiče, jímž protéká ustálený proud 1 ampér (1 C = 1 A·s). 
Snadno lze vypočítat, že náboj 1 C odpovídá 6,242·1018 elementárních nábojů.

### Elektrický proud

Elektrický proud je uspořádaný pohyb volných částic s elektrickým nábojem, 
který nastává ve vhodném fyzikálním prostředí, vlivem elektrického pole. 
Jako fyzikální veličina je elektrický proud definován množstvím 
elektrického náboje Q prošlého soustavou za určitý čas t.
```
I= Q/t
```
Směr toku elektrického proudu je dán konvencí jako směr pohybu částic s kladným 
nábojem. V elektrických obvodech tedy proud teče od kladného pólu 
elektrického zdroje přes spotřebič k zápornému pólu zdroje. Tento směr je opačný 
ke směru pohybu volných elektronů v pevných vodičích. Elektrický proud 
stejnosměrný (direct current, DC, =) protéká obvodem jedním směrem, 
který se s časem nemění. Střídavý proud (alternating current, AC, ~) periodicky mění svůj 
směr i velikost.

Jednotka elektrického proudu – ampér (A) – je základní jednotkou SI. 
Je definován jako elektrický proud, který při stálém průtoku dvěma rovnoběžnými přímými 
nekonečně dlouhými vodiči zanedbatelného kruhového průřezu, umístěnými ve vakuu ve 
vzájemné vzdálenosti 1 metr, vyvolá mezi nimi stálou sílu o velikosti 2·10–7 newtonu 
na 1 metr délky vodiče.

### Elektrický odpor 
Elektrický odpor (rezistance) je fyzikální veličina charakterizující schopnost daného systému vést elektrický proud. Závisí na materiálu, teplotě, délce a průřezu vodiče. Každý materiál má charakteristický měrný odpor ρ (rezistivitu). 
S rostoucí délkou vodiče L roste jeho odpor R, s rostoucím průřezem vodiče A jeho odpor klesá.
```
R=(ró)*L/A
```

### Elektrické napětí

Elektrické napětí je definováno jako rozdíl elektrických potenciálů mezi dvěma body v elektrickém poli nebo jako 
práci vykonanou při přemístění kladného jednotkového elektrického náboje 
mezi dvěma body elektrického pole.

Jednotkou elektrického potenciálu a elektrického napětí je volt (V). 
Je to napětí mezi konci vodiče, do něhož stálý proud 1 ampéru 
dodává výkon 1 wattu.

## Elektrická práce a výkon elektrického proudu
Nejčastějším případem konání elektrické práce je působení elektrického pole 
zdroje o napětí U na částice s elektrickým nábojem ve vodiči, 
které způsobí pohyb částic – elektrický proud I po dobu t.

```
W = U*I*t
```

Elektrický výkon je fyzikální veličina, která vyjadřuje vykonanou elektrickou práci za jednotku času. 
Značí se písmenem P a jeho jednotkou je watt, značený písmenem W. 
Elektrický výkon je druhem výkonu, u kterého práci koná elektrická síla

```
P = U*I -> W=P*t (Ws, kWh)
```

Účinnost je fyzikální veličina, která udává poměr mezi výkonem a příkonem stroje při vykonávání práce.

Energie dodaná stroji musí být vždy větší než práce strojem vykonaná z důvodu ztrát - přeměně energie na 
neužitečné druhy (např. v důsledku tření se mění mechanická energie v teplo). 
Proto účinnost je vždy menší než 100 %.

```
η = P/P˘p
```

## Sériové a Paralelní zapojení resistorů 
### Sériové zapojení
![Seriové zapojení](images/zapojeni_serie.png)

### Paralelní zapojení
![Paralelní zapojení](images/zapojeni_paralel.png)

## Zdroje napětí
**Nebudu se zdržovat pak dodělám**
Elektrický zdroj funguje na principu rozdílu záporně nabitých částic
(elektronů) na pólech. + a - se přitahují -> vznik elektrického proudu.

Může být myšleno jako Zdroj elektrického napětí je zařízení, 
ve kterém se přeměňuje jiný druh energie na energii elektrickou.

## Základní logické funkce

### AND
Logický součin – má na výstupu log. 1 pouze tehdy, je-li na všech jeho vstupech log. 1.
Matematický zápis: Y = A * B

### NAND
Negovaný logický součin – má na výstupu log. 1 pouze tehdy, 
pokud není na všech vstupech log. 1. Je to negovaný (opačný) 
výsledek logického součinu (AND). Je to nejpoužívanější log. člen.
Matematický zápis: Y = /(A * B)

### OR
Logický součet – má na výstupu log. 1 pouze tehdy, 
pokud je alespoň na jednom vstupu log. 1.
Matematický zápis: Y = A + B

### NOR
Negovaný logický součet – má na výstupu log. 1 pouze tehdy, 
pokud je na všech vstupech log. 0. Je to negovaný (opačný) 
výsledek logického součtu (OR).
Matematický zápis: Y = /(A + B)

### XOR
Exklusivní logický součet – má na výstupu log. 1 pouze tehdy, 
pokud je na vstupech rozdílná log. hodnota.
Matematický zápis: Y = /(A B)

### NOT 
Logická negace (invertor) – na výstupu je vždy opačná logická 
hodnota než na vstupu.
Matematický zápis: Y = /A

### YES (repeater)
Opakovač – na výstupu je vždy stejná logická hodnota jako na vstupu.
Matematický zápis: Y = A

## Logické úrovně

Boolean -> True a False
Mezi těmito stavy, je zakázané pásmo (Zamezuje špatné registraci hodnoty)
![Logické úrovně](images/logicke.jpg)

### Vysvětlivky:
```
VOH     (Voltage Output High; minimální výstupní napětí pro logickou 1)
VCC     (kladné napájecí napětí integrovaného obvodu)
VOL     (Voltage Output Low; maximální výstupní napětí pro logickou 0)
VIH     (Voltage Input High; minimální vstupní napětí pro logickou 1)
VIH-max (maximální vstupní hodnota napětí pro logickou 1) 
VIL-min (minimální vstupní hodnota napětí pro logickou 0)
VIL     (Voltage Input Low; maximální vstupní hodnota napětí pro logickou 0)
VCC     (připojený kolektor tranzistoru – Collector)
VEE     (připojený emitor tranzistoru – Emitter) 
VDD     (kladné napájecí napětí; Drain)
VSS     (GND nebo záporné napájecí napětí; Source)

```

## Logické hodnoty
Logický, číslicový či digitální obvod je elektronický obvod, 
který pracuje s diskrétními stavy. Jsou tvořeny tzv. logickými členy 
(nazývanými též hradla). Naopak z logických obvodů se skládají 
číslicové systémy.

Na rozdíl od analogových elektronických obvodů, 
které jsou založené na spojité formě informace 
(mechanické ručičkové hodiny), v logických obvodech je 
informace reprezentována a zpracovávána v podobě diskrétní 
(digitální hodiny).

## Typické kombinační obvody 
- dekodéry
- multiplexery a demultiplexery
- komparátory
- obvody pro aritmetické operace (sčítačky, generátory přenosu apod.
