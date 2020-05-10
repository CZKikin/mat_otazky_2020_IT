# Hardware a programování minipočítače Raspberry Pi (15)

## Architektura ARM

- 32 /64 bitová mikroprocesorová architektura typu RISC
- Přístup do paměti se provádí pouze instrukcemi LOAD / STORE
- Povoluje částečné překrývání vnitřních registrů
- Obsahuje také jednoduchý instrukční soubor a jednoduše využitelné kompilátory
  vyšších programovacích jazyku
- RPi 4 má procesor Broadcom BCM
- ARM procesory využívají RISC

Procesory ARM pracují ve čtyřech základních pracovních režimech, které jsou:

- Uživatelský režim USR
- Privilegovaný režim supervizora SUP (sudo)
- Privilegovaný režim přerušení IRQ
- Privilegovaný režim rychlého přerušení FIQ ( v podstatě IRQ s vyšší prioritou)

V privilegovaných režimech je možné provádět strojové instrukce, které mohou ohrozit chod počítače

Procesory ARM podporují dva adresové módy:

- pomocí čítače instrukcí
- pomocí bázové adresy uložené v jednom z registrů

## Popis parametrů a porovnání s PC

Nejnovější RPi 4
- 64bit čtyřjádrový procesor o taktu 1,5 GHz
- RAM 4 GiB (nejvyšší model)
- Napájení USB-C (dříve micro-USB)
- Dva micro-HDMI porty (s podporou rozlišení 4K, dříve jen HDMI port)
- 4x USB (2x USB 3.0, 2x USB 2.0)
- 15 - pin rozhraní MIPI kamerový (CSI) konektor, který se používá s kamerou RPi

RPi je srovnatelný se slabším stolním počítačem, použitý procesor ARM je srovnatelný s běžným CPU smartphonu. Na RPI je možné používat různé distribuce Linuxu (např.
Raspbian) i Windows 10 IOT.

## GPIO

RPi nabízí čtyřiceti pinový GPIO (General-purpose input/output) header (J8), což jsou vstupní nebo výstupní piny,
28 z nich se může libovolně programovat. Jsou využívány k připojení vstupně-výstupních periferií, 
jako jsou například LED diody, podporované displeje, tlačítka, reproduktory a mnoho dalších.

Na těchto GPIO pinech je možné nastavit dvě logické hodnoty 1 a 0. Díky logické 1 bude na pin přivedeno
napětí 3,3 V, anebo pomocí logické 0 se dosáhne napětí 0 V. GPIO také nabízí vstupy/výstupy +5 V (pro
napájení samotného RPi), +3,3 V a GND.

Na pinech se nachází SPI sběrnice, PWM, I2C sběrnice.


### SPI (Serial Peripheral Interface)
Je sériově periferní rozhraní, používá se mezi řídícími mikroprocesory a integrovanými obvody, komunikace
je řešena pomocí společné sběrnice.
U rozhraní SPI je vždy jeden řídicí obvod (Master) a jeden či více periferních obvodů (Slave). Master řídí
celou komunikaci a pomocí signálů SlaveSelect určuje, se kterým periferním zařízením se právě pracuje.

Master aktivuje signál SlaveSelect (SS) pro obvod s kterým chce komunikovat a uvede jej do log. 0. Poté co
je obvod vybrán, Master na výstupu SCLK(serial clock) začne posílat hodinové pulsy, a zároveň posílá data
na výstupu MOSI(Master Out, Slave In), jakmile přenos skončí, uvede vstup SS do neaktivního stavu.

SPI je plně duplexní sběrnice, takže pokud probíhá i komunikace ze strany Slave->Master slouží k tomu
vodič MISO (Master In, Slave Out)

### I2C
(někdy taky TWI)

Komunikace probíhá na dvou vodičích, datový SDA a hodinový SLC
Je zde taky Master a Slave, ale na rozdíl od SPI má Slave vlastní sedmibitovou adresu (0-127)
Master na vodiči SDA pošle log. 0 a poté nastaví 0 i na lince SCL, tím vznikne „startovací signál“
následně master začne vysílat hodiny a zároveň posílá na vodič SDA data.

## Instalace operačního systému

Nejjednodušší cestou, jak nainstalovat operační systém je stáhnout Raspbian verzi „NOOBS“, přesunout
instalátor na naformátovanou microSD kartu (min. 8 GB), vložit kartu do RPi a zapnout ho. Následně nás
instalátor provede prvotním nastavením.

## Programování a zapojení 7 segmentového displeje

Dva typy 7 segmentového displeje:
- společná katoda (-)
- společná anoda (+)

U společného plusu musíme dát rezistor (330 ohm), RPi zvládá dodávat okolo 60 mA, pokud dovolíme
odebírat víc, může dojít ke spálení RPi

Číslování podle pinů (1-40) (.BCM číslování podle GPIO)
```python
GPIO.setmode(GPIO.BOARD)
```

Nastavení pinů pro výstup (musí se provést u všech pinů) např.:
```python
GPIO.setup(35, GPIO.OUT) #GPIO
```

Pokud máme společnou anodu, tak 1 nesvítí, 0 svítí (u katody je to naopak).

K displeji máme připojených 7 pinů (nezapojujeme tečku) např:
```python
gpin=[35,12,36,33,32,38,40]
```

Každý pin je připojen k jednomu segmentu.
A k pinu 35, B 12, C 36, D 33, E32, F 38, G 40.
Chceme-li rozsvítit 5 musíme zapnout segmenty A, C, D, G, F.

Segment rozsvítíme:
```
GPIO.output(cislo_pinu,0)
```

Zapneme piny 35, 36, 33, 40, 38
Na konci všech programů je vhodné používat:

```
GPIO.cleanup() #reset pinů
```

## Ovládání několika sedmisegmentových displejů – multiplexní řešení

Tato metoda spočívá v tom, že jsou jednotlivé stejné vývody všech sedmisegmentových displejů spolu
spojeny, např. všechny vývody “a”, poté všechny vývody “b” apod. Tím dostaneme vždy osm využitých pinů
mikrokontroleru pro řízení zobrazeného znaku, ať přidáme jakékoli množství sedmisegmentových displejů.
K těmto osmi pinům ale navíc potřebujeme ke každému sedmisegmentovému displeji jeden pin
mikrokontroléru pro řízení rozsvícení. Tím spínáme společný vývod displeje.

**Zobrazení znaků probíhá následujícím způsobem:**

- Nastavíme znak, který chceme zobrazit na prvním displeji.
- Sepneme na krátký časový interval pouze první displej, aby došlo k zobrazení znaku pouze na prvním
displeji.
- Vypneme první displej.
- Nastavíme znak, který chceme zobrazit na druhém displeji.
- Sepneme na krátký časový interval pouze druhý displej, aby došlo k zobrazení znaku pouze na druhém
displeji.
- Vypneme druhý displej.
- Pokračujeme až do posledního displeje a poté znovu začneme od prvního displeje.

Pokud budeme dostatečnou rychlostí přepínat mezi zobrazenými znaky (frekvence cca 50 Hz pro všechny
displeje), tak se nám bude zdát, že jsou všechny vývody rozsvíceny, protože lidské oko není schopné tak
rychlé změny vnímat. Výhoda tohoto řízení je poměrně malý počet vývodů. Nevýhoda je, že musíme
programově neustále obnovovat zobrazené znaky v nekonečné smyčce. Další nevýhodou je, že s
narůstajícím počtem sedmisegmentových displejů klesá jas, protože se snižuje střída rozsvícení pro
jednotlivé displeje. S tím je nutné počítat při návrhu protékajícího proudu sedmisegmentovými displeji.


## Vstupní periferie

Tlačítka mají čtyři vývody. Vždy dva a dva jsou spojeny dohromady

**Zákmit** - při zmáčknutí procesor zachytí třeba dva nebo tři po sobě jdoucí stisknutí.
Řešení zákmitů:
- Mechanicky – tedy použitím bezzákmitových tlačítek. Ale ta jsou velmi drahá.
- Elektricky – přidáním kondenzátoru – odfiltruje rychlé pulsy, Schmittův obvodu, monostabilní
klopný obvod
- Softwarově – nejjednodušší řešení je při každém stisknutí tlačítka počkat třeba 300 milisekund,
zkontrolovat zda je tlačítko stále stisknuté, a teprve poté dělat nějakou akci. Těmto postupům se
říká debouncing

### Pull Up a Pull Down

Pro nastavení PullUP/PullDOWN v pythonu:
```python
GPIO.setup(button_pin, pull_up_down=GPIO.PUD_UP/ GPIO.PUD_DOWN)
# pokud se použije toto nastavení, není nutné dávat Pull Up/Down rezistor fyzicky do obvodu
```

### Proč se tam dává pull up / pull down rezistor?

Když stiskneme tlačítko objeví se na GPIO pinu buď napětí 3.3 V nebo 0 V (zem) podle toho, jak to máme
zapojeno. Pokud však tlačítko pustíme, pin se nemá k čemu připojit, je připojený jen tak ke „vzduchu“ a
může dělat problémy.

Abychom se tomu vyhnuli použijeme Pull Up / Pull Down rezistor, který při nestisknutém tlačítku připojí
GPIO pin ke kladnému napětí, respektive zemi.

```
Autor: Matula Daniel
Datum: 10.5.2020
Merger: Vít Staniček
Sloučení prací neproběhlo, byly provedeny úpravy formátování.
```