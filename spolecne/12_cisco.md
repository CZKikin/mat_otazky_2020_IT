# Bezpečnost aktivních síťových prvků
V této otázce se zabývám zabezpečením přístupu do konzole cisco zařízení a nastavením SSH.

## Co je potřeba?
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

## Nastavení ssh na ROUTERU
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
## Nastavení přihlašování na konzolovém rozhraní
Jelikož username a secret již máme, stačí jen zapnout přihlašování na konzolovém
rozhraní.
```
nazev_routeru(config)#line console 0
nazev_routeru(config-line)# login local
```

## Nastavení MOTD a login message
Nastavení zprávy systému
```
nazev_routeru(config)#banner motd %Toto je majetek moje_firma_sro. Pokud nejste opravneni ke sprave tohoto zarizeni, kontaktujte vaseho nadrizeneho%
nazev_routeru(config-line)# banner login %Jakakoli aktivita je logovana%
```
