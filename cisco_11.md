# Bezpečnost aktivních síťových prvků
V této otázce se zabývám zabezpečením přístupu do konzole cisco zařízení a nastavením SSH.

## Co je potřeba?
Pro nastavení ssh je potřeba:
- Název zařízení
- Název domény
- Klíč pro šifrování - RSA
- IP adresa
- Username a secret
- Povolenou komunikaci

Pro zabezpečení konzole je potřeba:
- Username a secret

## Nastavení ssh na ROUTERU
SSH nastavím následovně (vyzoušeno v packet traceru v. 7.3.0)
```
Router>enable
Router#configure terminal
Router(config)#hostname nazev_routeru
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
Může se stát, že u maturity po vás budou chtít SSHv2!! -  Pokud jde o packet tracer
zde to nejde. Tento router totiž má maximální velikost klíče 512, ale SSHv2 potřebuje alespoň 768.
Pokud by chtěli příkaz, šlo by to příkazem **ip ssh version 2**
```
*bře 1 0:3:24.979: RSA key size needs to be at least 768 bits for ssh version 2
*bře 1 0:3:24.980: %SSH-5-ENABLED: SSH 1.5 has been enabled
```