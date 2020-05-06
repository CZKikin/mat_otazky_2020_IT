# 17. Wi-Fi a VF Technika
## Využití Wi-Fo a druhy připojení
Wi-Fi (nebo také Wi-fi, WiFi, Wifi, wi-fi, wifi) je v informatice označení pro několik standardů IEEE 802.11 popisujících bezdrátovou komunikaci v počítačových sítích (též Wireless LAN, WLAN). Samotný název WiFi vytvořilo Wireless Ethernet Compatibility Aliance. Tato technologie využívá tak zvaného „bezlicenčního frekvenčního pásma“,proto je ideální pro budování levné, ale výkonné sítě bez nutnosti pokládky kabelů. Název původně neměl znamenat nic,[4] ale časem se z něj stala slovní hříčka wireless fidelity (bezdrátová věrnost) analogicky k Hi-Fi (high fidelity – vysoká věrnost).

*Nemám páru co je kurva druh připojení Wi-Fi*

## Standardy 802.11(a,b,g,n)

| Standard     | Označení   | Rok[GHz] | Pásmo[Mbit/s] | Max rychlost | Fyzická vrstva |
| ------------ | ---------- | -------- | ------------- | ------------ | -------------- |
| IEEE 802.11 | - | 1997 | 2.4 | 2 | DSSS a FHSS |
| IEEE 802.11a | Wi-Fi 1 | 1999 | 5 | 54 | OFDM |
| IEEE 802.11b | Wi-Fi 2 | 1999 | 2.4 | 11 | DSSS |
| IEEE 802.11g | Wi-Fi 3 | 2003 | 2.4 | 54 | OFDM |
| IEEE 802.11n | Wi-Fi 4 | 2009 | 2.4/5 | 600 | MIMO OFDM |
| IEEE 802.11y | - | 2008 | 3.7 | 54 | - | - |
| IEEE 802.11ac | Wi-Fi 5 | 2013 | 5 | 3466.8 | MU-MIMO OFDM |
| IEEE 802.11ad | - | 2012 | 60 | 6757 | - | - |
| IEEE 802.11ax | Wi-Fi 6 | 2019 | 2.4/5/6 | 10530 | MIMO-OFDM |

## Frekvence
Frekvence (též kmitočet) je fyzikální veličina, která udává počet opakování periodického děje za daný časový úsek. Například v obvodu střídavého proudu takto označujeme počet kmitů napětí či proudu za jednotku času.

## Útlum
Útlum volného prostoru (anglicky free-space path loss; FSPL) je v telekomunikaci útlum elektromagnetické vlny, který je důsledkem rozptylu vlny do prostoru. Nezahrnuje zisk antény.Vztah pro útlum volného prostoru často vede k mylnému názoru, že útlum volného prostoru závisí na frekvenci elektromagnetické vlny. Výše uvedený výraz totiž ve skutečnosti kombinuje dva efekty. Rozptyl elektromagnetické energie ve volném prostoru, který je nepřímo úměrný druhé mocnině vzdálenost a účinnou (efektivní) plochu antény (aperturu), která popisuje, jak dobře anténa "chytá" výkon přicházející elektromagnetické vlny.

## Zisk
Udává, kolikrát větší výkon přijímací anténa poskytuje buď vůči půlvlnnému dipólu nebo vůči teoretické dokonale všesměrové anténě, tzv. izotropnímu zářiči

## Kanály
![Kanály](images/wifi_kan.png)
Standard 802.11 dělí každé z výše popsaných pásem do kanálů podobným způsobem, jako jsou rozděleny pásma rozhlasového a televizního vysílání. Například pásmo 2,4000-2,4835 GHz je rozděleno do 13 kanálů vzájemně posunutých o 5 MHz, přičemž kanál 1 pracuje na frekvenci 2,412 GHz a kanál 13 na frekvenci 2,472 GHz (Japonsko přidalo 14. kanál, který je povolen pouze pro 802.11b, a je posunut o 12 MHz od kanálu 13). 802.11b byl založen na DSSS modulaci s celkovou šířkou kanálu 22 MHz bez strmých prahů. Kvůli tomu jsou pouze tři nepřekrývající se kanály v celém pásmu. Dokonce i nyní je mnoho zařízení dodáváno s přednastavenými kanály 1, 6 a 11, i když novější standard 802.11g umožňuje čtyři vzájemně se nepřekrývající kanály - 1, 5, 9 a 13. Nyní jsou k dispozici čtyři, protože ODFM modulované 802.11g kanály jsou 20 MHz široké.

## Dosah
Výkon vysílané vlny.
```
P = E*H [w] 
```
Plošná hustota výkonu v danném místě je
```
P/S "S - Povrch koule"
```
Při šíření vlny na zemském povrchu se vlna může ohýbat, odrážet a pronikat překážkami.

*Víc nemůžu sehnat*

## Rychlost přenosu
Rychlost světla, přes překážky nižší, ztráty a odrážení.

## Výpočet vzdálenosti
**nic**

## Antény
Anténa je zařízení k příjmu nebo k vysílání rádiových signálů, je to část vysokofrekvenčního vedení upravená tak, aby účinně vyzařovala energii do prostoru. Antény se dělí na antény přijímací a antény vysílací (v principu ale může každá anténa vysílat i přijímat):

- vysílací anténa je určena k přeměně elektrické energie na energii elektromagnetických vln
- přijímací anténa naopak slouží k přeměně energie elektromagnetických vln na elektrickou energii
- přijímací a vysílací zároveň

Elektromagnetické vlny vyzařuje každý vodič, kterým prochází střídavý elektrický proud. Anténa je vodič upravený takovým způsobem, aby vyzařoval maximální množství elektrické energie. Ne každé uspořádání vodičů zaručuje maximum vyzařované energie. Například kroucené dvojlinky, používané v telekomunikacích, mají množství vyzařované i přijímané (rušení) energie optimalizované na minimum. Jako nejjednodušší anténu lze využít symetrický zářič, takzvaný dipól. Ten vychází z úseku vedení o délce poloviny vlnové délky vysílaného/přijímaného signálu.

## Fresnelova zóna
Fresnelova zóna je jednou z řady konfokálních protáhlý elipsoidní oblasti prostoru mezi a kolem vysílací antény a přijímací antény. Regiony se používají k pochopení a vypočítat sílu vln (například zvukové nebo rádiových vln) šířící se mezi vysílačem a přijímačem, jakož i předpovědět, zda překážky v blízkosti linie spojující vysílač a přijímač způsobí výrazný zásah.

## Šíření VF signálu
viz. **Dosah**

## Modulace
Proces, při kterém je některý z parametrů nosné vlny ovlivňován modulačním signálem.
Pro přenos zpráv  na různé vzdálenosti se používají VF vlny různých frekvencí, nazývané nosné vlny. Přenášené zprávy musí vhodným způsobem ovlivňovat některou charakteristickou veličinu nosné vlny: amplitudu ,frekvenci ,fázi,sled impulsů apod.. Toto ovlivňování nosné vlny se nazývá modulace.

Než dojde k modulaci, je nutné změny různých fyzikálních veličin (zvuk, světlo, teplota, tlak aj.), které představují přenášené zprávy, přeměnit na jim odpovídající elektrické signály. Těmito signály, které se nazývají modulační signály se potom provádí modulace.
### Analogové modulace

#### Amplitudová modulace
**nic**

#### Frekveční modulace

### Digitální modulace
#### Frequency shift keying (FSK)
#### Fázová modulace (PSK - Phase shift keying)

### Vícestavové Digitální modulace
#### 4-PSK
#### QPSK
#### Modulace QAM


## MIMO
**nic**

