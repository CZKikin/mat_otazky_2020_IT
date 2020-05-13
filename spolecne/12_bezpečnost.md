# Bespečnost v síťové infrastruktuře

### Co je potřeba?
Pro nastavení ssh je potřeba:
- Název zařízení
- secret pro privilegovaný režim
- Název domény
- Klíč pro šifrování - RSA
- IP adresa
- Username a secret
- Povolenou komunikaci

Pro zabezpečení konzole je potřeba:
- Username a secret

### Nastavení ssh na ROUTERU
SSH nastavím následovně (vyzkoušeno v packet traceru v. 7.3.0)
```
Router>enable
Router#configure terminal
Router(config)#hostname nazev_routeru
Rotuer(config)#enable secret cisco
nazev_routeru(config)#ip domain-name mojesit
nazev_routeru(config)#crypto key generate rsa 
```
Zde budeme tázáni na velikost klíče (větší = lepší)

```
The name for the keys will be: router.mojesit
Choose the size of the key modulus in the range of 360 to 2048 for your
  General Purpose Keys. Choosing a key modulus greater than 512 may take
  a few minutes.

How many bits in the modulus [512]: 512
% Generating 512 bit RSA keys, keys will be non-exportable...[OK]
```
```
nazev_routeru(config)#username cisco secret cisco
```
Pozn.: Může se stát, že u maturity po vás budou chtít SSHv2!! -  Pokud jde o packet tracer
zde to nejde. Tento router totiž má maximální velikost klíče 512, ale SSHv2 potřebuje alespoň 768.
Pokud by chtěli příkaz, šlo by to příkazem **ip ssh version 2**
```
*bře 1 0:3:24.979: RSA key size needs to be at least 768 bits for ssh version 2
*bře 1 0:3:24.980: %SSH-5-ENABLED: SSH 1.5 has been enabled
```
Zde již máme ssh aktivní, není nutno ho aktivovat příkazem. Vybereme interface
a dáme mu ip adresu. **Pozor!! Interface je ve výchozím nastavení routeru vyplý.**
**Zapneme ho pomocí příkazu** ***no shutdown***
Pokud nastavujeme ssh na switch, který pracuje jen na druhé vrstvě modelu ISO/OSI, musíme 
ip adresu nastavit na rozhraní vlan (virtual lan). Porty takového switche nemůžou mít ip adresu.

```
nazev_routeru(config)#interface gigabitEthernet 0/0
nazev_routeru(config-if)#ip address 192.168.1.1 255.255.255.0
nazev_routeru(config-if)#no shutdown
nazev_routeru(config-if)#exit
```
Vrátíme se zpět a povolíme SSH na virtuálních příkazových řádcích. Současně zapínáme ověřování
proti **lokální** databázi routeru.

```
nazev_routeru(config)#line vty 0 15
nazev_routeru(config-line)#transport input ssh
nazev_routeru(config-line)#transport output ssh
nazev_routeru(config-line)#login local
```
### Nastavení přihlašování na konzolovém rozhraní
Jelikož username a secret již máme, stačí jen zapnout přihlašování na konzolovém
rozhraní.
```
nazev_routeru(config)#line console 0
nazev_routeru(config-line)# login local
```

### Nastavení MOTD a login message
Nastavení zprávy systému
```
nazev_routeru(config)#banner motd %Toto je majetek moje_firma_sro. Pokud nejste opravneni ke sprave tohoto zarizeni, kontaktujte vaseho nadrizeneho%
nazev_routeru(config-line)# banner login %Jakakoli aktivita je logovana%
```

## Pilíře informační bezpečnosti

### Confidentiality - Důvěrnost
Důvěrnost brání prozrazení informací neoprávněným osobám, zdrojům a procesům. 
Dalším termínem důvěrnosti je soukromí. Organizace omezují přístup, aby zajistily, 
že data nebo jiné síťové zdroje mohou používat pouze oprávnění operátoři. 
Například programátor by neměl mít přístup k osobním informacím všech zaměstnanců.

Organizace musí školit zaměstnance o osvědčených postupech při ochraně citlivých informací, 
aby se chránily samy a organizace před útoky. 
Metody používané k zajištění důvěrnosti zahrnují šifrování dat, ověřování a řízení přístupu.

### Integrity - Integrita
Integrita je přesnost, konzistence a důvěryhodnost dat během celého jejich životního cyklu. Dalším pojmem integrity je kvalita. 
Data procházejí řadou operací, jako je zachycení, uložení, načtení, aktualizace a přenos. 
Data musí během všech těchto operací neoprávněných subjektů zůstat nezměněna.

Metody používané k zajištění integrity dat zahrnují hašování, kontroly validace dat, 
kontroly konzistence dat a kontroly přístupu. Systémy integrity dat mohou zahrnovat jednu nebo více výše uvedených metod.

### Availability - Dostupnost
Dostupnost údajů je princip, který se používá k popisu potřeby udržovat dostupnost informačních systémů a služeb za všech okolností. 
Kybernetické útoky a selhání systému mohou zabránit přístupu k informačním systémům a službám. 
Například přerušení dostupnosti webové stránky konkurenta jeho snížením může poskytnout výhodu jeho soupeři. 
Tyto útoky odmítnutí služby ohrožují dostupnost systému a v případě potřeby brání legitimním uživatelům v přístupu k informačním 
systémům a jejich používání.

Metody používané k zajištění dostupnosti zahrnují redundanci systému, zálohování systému, zvýšenou odolnost systému, 
údržbu zařízení, aktuální operační systémy a software a zavedené plány na rychlé zotavení z nepředvídaných katastrof.

## Principy šifrování a jejich protokoly

### Symetrické

` 3DES(Triple DES), IDEA, AES`

Symetrické algoritmy používají stejný předsdílený klíč k šifrování a dešifrování dat, což je metoda známá také jako 
šifrování soukromého klíče.
Nejběžnějšími typy kryptografie jsou blokové šifry a proudové šifry. 
Každá metoda se liší způsobem, jakým seskupuje kousky dat pro jejich šifrování.

#### Blokové šifry

Blokové šifry transformují blok prostého textu s pevnou délkou na společný blok ciphertext o 64 nebo 128 bitech. 
Velikost bloku je množství dat zašifrovaných najednou. 
Chcete-li dešifrovat tento šifrový text, použijte reverzní transformaci na blok šifrového textu pomocí stejného tajného klíče.
Blokové šifry obvykle vedou k výstupním datům, která jsou větší než vstupní data, protože ciphertext musí být násobkem velikosti bloku. 
Například Data Encryption Standard (DES) je symetrický algoritmus, který šifruje bloky v 64bitových blocích pomocí 56bitového klíče. 
Aby se toho dosáhlo, algoritmus bloku vezme data po jednom kusu najednou, například 8 bajtů na kus, dokud není celý blok plný. 
Pokud je méně vstupních dat než jeden celý blok, přidává algoritmus umělá data nebo mezery, dokud nepoužívá celých 64 bitů, 
jak je znázorněno na obrázku 1 pro 64 bitů vlevo.

#### Streamovací šifry

Na rozdíl od blokových šifrů šifrují proudové šifry najednou jeden bajt nebo jeden bit najednou, 
jak je znázorněno na obrázku 2. Představte si šifry proudu jako blokovou šifru s velikostí bloku jednoho bitu. 
U proudové šifry se transformace těchto menších jednotek prostého textu liší v závislosti na tom, 
kdy se s nimi během šifrovacího procesu setká. Streamovací šifry mohou být mnohem rychlejší než blokové šifry a obvykle 
nezvýší velikost zprávy, protože mohou zašifrovat libovolný počet bitů.

A5 je proudová šifra, která poskytuje hlasové soukromí a šifruje komunikaci mobilních telefonů. 
Je také možné použít DES v režimu proudové šifry.

Složité kryptografické systémy mohou kombinovat blok a proud ve stejném procesu.


### Asymetrické
Asymetrické šifrování, také nazývané šifrování pomocí veřejného klíče, používá pro šifrování jeden klíč, který se liší od klíče použitého pro dešifrování. 
Zločinec nemůže vypočítat dešifrovací klíč na základě znalosti šifrovacího klíče a naopak v žádném přiměřeném čase.

Asymetrické algoritmy používají vzorce, které může vyhledat kdokoli. Tyto nesouvisející klíče jsou tím, co tyto algoritmy zajišťuje. 
Asymetrické algoritmy zahrnují:

`RSA (Rivest-Shamir-Adleman)` - používá produkt dvou velmi velkých prvočísel se stejnou délkou mezi 100 a 200 číslicemi. 
Prohlížeče používají RSA k navázání zabezpečeného připojení (SSH).

`Diffie-Hellman` - poskytuje metodu elektronické výměny pro sdílení tajného klíče. Zabezpečené protokoly, 
například Secure Sockets Layer (SSL), Transport Layer Security (TLS), Secure Shell (SSH) a Internet Protocol Security (IPsec), 
používají Diffie-Hellman.

`ElGamal` - používá digitální vládní standard USA. Tento algoritmus je zdarma k použití, protože nikdo nemá patent.

`Eliptická křivka kryptografie (ECC)` - používá eliptické křivky jako součást algoritmu. 
V USA používá Národní bezpečnostní agentura ECC pro generování digitálního podpisu a výměnu klíčů.
