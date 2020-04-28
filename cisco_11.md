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
SSH nastavím následovně (vyzoušeno v packet traceru v. xx)
```
Router>enable
Router#configure terminal
Router(config)# hostname nazev_routeru
nazev_routeru(config)# ip domain-name mojesit
nazev_routeru(config)# crypto key generate rsa 
```
Zde budeme tázáni na velikost klíče (větší = lepší)

```

```