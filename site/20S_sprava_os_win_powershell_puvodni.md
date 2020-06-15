# 20. Správa OS Windows v PowerShellu

PowerShell je automatizace úloh pro rùzné platformy a rozhraní pro správu konfigurace, která se
skládá z prostøedí pøíkazového øádku a skriptovacího jazyka. Na rozdíl od vìtšiny prostøedí, která
pøijímají a vracejí text, je PowerShell postaven nad modulem CLR (Common Language
Runtime) .NET a pøijímá a vrací objekty .NET. Tato zásadní zmìna pøináší zcela nové nástroje a
metody pro automatizaci.

```
Zapíná se napsáním PowerShell do pøíkazové øádky ve windows.
```
##  Základní pøíkazy

```
- cls - vyèistí pøíkazovou øádku PS, cls je alias pro Clear-Host
- Get-Alias - Vypíše seznam pouitelnıch aliasù v PS
- Get-History - vypíše historii zadanıch pøíkazù
- .\názevSouboru.pøípona - otevøe soubor (Vdycky zapínejte PowerShell jako správce,
jinak to nic nebude umìt)
- PowerShell ISE - je hlavnì pro psaní scriptù
- Start-Transcript - vše co èlovìk napíše a PS vypíše se uloí do texáku - není nutné, ale
lepší pro správu
- Get-PSDrive - vypíše dostupné disky
- Get-Help *jakıkoliv pøíkaz* - vypíše informace o daném pøíkazu
- Get-Help Get-Command -Examples - vypíše moné pouití pøíkazu
- Get-Command -noun S* - Vypíše všechny pøíkaz u kterıch zaèíná P.Jméno “S”
- Get-Command -noun service - Vypíše pouze pøíkazy které mají P.Jméno service
- Get-Service - vypíše všechny dostupné sluby. S jednotlivımi slubami mùeme
manipulovat
- Get-Process - vypiše seznam aktivních procesù
- Start-Process notepad.exe - zapne process
- Stop-Process -Name "NázevProcesu" -Force - ukonèí proces
- Get-Process -Name Calculator | Get-Member - vypiš mi proces kalkulaèka | (a zároveò)
mi vypiš jeho pouitelné vlastnosti a metody
- Get-Process -Name Calculator | Select-Object \* - vypiš mi proces kalkulaèka | (a zároveò)
mi vypiš detailnì jeho vlastnosti
```
## Promìnné

```powershell
- PS C:\Windows\System32> $promenna = 123
- PS C:\Windows\System32> $promenna
> 123
```
```powershell
- $promenna2 = Get-Process Calculator
- $promenna
- $promenna2.\*TAB\* - vypíše po jednom vlastnosti promìnné
- $promenna2.kill() - vypne kalkulaèku, ale promìnná bude dál existovat
```
## Cmdlety

*Cmdlet* patøí mezi specializované pøíkazy v prostøedí PowerShellu, které implementují specifické
funkce. Cmdlety jsou pojmenované tak, e zaèínají *slovesem* , pak následuje znak *pomlèka* a pak je
*podstatné jméno* ( *Get-ChildItem* ), tento styl pojmenování dovoluje vıstinìjší pojmenování
jednotlivıch pøíkazù. Cmdlety jako vısledek mohou vrátit *objekt a kolekce* (pøípadnì pole objektù).

Cmdlet mùe bıt napsán v jakémkoliv jazyce, kterı podporuje platformu .NET (napøíklad C#,
VB.NET, IronPython, PHP, J# a jiné).

- Objekty, roury, aliasy

## OBJEKTY

K vytvoøení objektu v PS je nejprve zapotøebí pouít cmdlet **_New-Object_** k vytvoøení poèáteèního
objektu. Tento pøíkaz vytvoøí *.NET* nebo *COM* objekt ze sortimentu tøíd. Klasickı objekt je *.NET*
zaloenı na Objektu nebo PSObjektu. Avšak PSObjekt je preferovanı kvùi problémùm, které mohou
nstat pøi pøidávání vlastností k objektu zaloeného na tøídì Objekt.

K vytvoøení objektu zaloeného na PSObjektu potøebujete pouít *New-Object* s *–TypeName*
parametrem, abyste specifikovali typ/tøídu objektu.

```powershell
$system = New-Object -TypeName PSObject
Kdy spustíte tento pøíkaz, vygeneruje to PSCustomObject a zapíše se do promìnné $system
```
## ROURY

Roura zapojí více pøíkazù a jeden pøíkaz, pøedává svùj vıstup dalšímu pøíkazu, ten dalšímu a to a
do vısledku na obrazovce.

```
Jednotlivé pøíkazy nám oddìluje 
```
## ALIASY

Rutina Get-Alias získá aliasy v aktuální relaci. To zahrnuje vestavìné aliasy, aliasy, které jste
nastavili nebo importovali, a aliasy, které jste pøidali do svého profilu PowerShell.

Ve vıchozím nastavení **_Get-Alias_** alias a vrací název pøíkazu. Pøi pouití parametru Definice získá
Get-Alias název pøíkazu a vrací jeho aliasy.

```powershell
? Get-Alias
[[-Name] <String[]>]
[-Exclude <String[]>]
```

```powershell
[-Scope <String>]
[<CommonParameters>]
? Get-Alias
[-Exclude <String[]>]
[-Scope <String>]
[-Definition <String[]>]
[<CommonParameters>]
```
- Pøístup k souborovému systému, registru a úètùm

## REGISTRY

**New-Item -Path "HKCU:\brambora" -** vytvoøí novı registr
**New-ItemProperty -Path "HKCU:\brambora" -Name Pokus -Value 12345 -PropertyType** string -
pøidáme vlastnosti registru

**Set-ItemProperty -Path "HKCU:\brambora" -Name Pokus -Value 54321 -** zmìna vlastností
registru
**Get-Item -Path HKCU:\Brambora -** vypíše hodnoty registru
**Remove-ItemProperty -Path HKCU:\Brambora -name pokus -** Vymae hodnotu registru
**Remove-Item -Path HKCU:\Brambora -** vymae registr

## UIVATELÉ

**Get-LocalUser -** vypíše seznam uivatelù
**New-LocalUser "Pepa" -Password 123456 -FullName "Pepa Z Depa" -Description "Pokusnı
králík" -** Vytvoøí nového uivatele Pepa
**Add-LocalGroupMember -Group "Users" -Member "Pepa" -** pøídá uivatele pepa do skupiny
Users
**Remove-LocalUser -Name "Pepa" -** odstraní uivatele

```
více info => Get-Help LocalUser / Get-Help LocalGroup
```
- Práce s ACL
**_Set-Acl_** mìní popis zabezpeèení urèité poloky, jako je sloka nebo klíè registru, aby odpovídal
hodnotám popisu zabezpeèení, které jsi doplnil.

Chcete-li pouít **_Set-Acl_** , pouijte parametr **_Path_** nebo **_InputObject_** k identifikaci poloky, její
popis zabezpeèení chcete zmìnit. Potom pomocí parametrù **_AclObject_** nebo **_SecurityDescriptor_**
zadejte popis zabezpeèení, které mají hodnoty, které chcete pouít. **_Set-Acl_** pouije pouití popis
zabezpeèení.

```powershell
Set-Acl
```
```powershell
[-Path] <String[]>
[-InputObject] <PSObject>
[-AclObject] <Object>
[-ClearCentralAccessPolicy]
[-Passthru]
[-Filter <String>]
```

```powershell
[-Include <String[]>]
[-Exclude <String[]>]
[-WhatIf]
[-Confirm]
[<CommonParameters>]
```
- Pøístup k WMI (cmdlet pro wmi, získání informací), Získávání informací o

## Objektech

```powershell
Get-CimInstance -ClassName Win32_Desktop #Tato funkce vrátí informace pro všechny pracovní plochy, a u jsou pouívány.
Get-CimInstance -ClassName Win32_BIOS #Tøída WMI Win32_BIOS vrátí pomìrnì kompaktní a úplné informace o systému BIOS v místním poèítaèi.
Get-CimInstance -ClassName Win32_Processor | Select-Object -ExcludeProperty "CIM*"
```
- Obecné informace o procesoru mùete naèíst pomocí Win32_Processor tøídy WMI, i
kdy budete pravdìpodobnì chtít tyto informace filtrovat
- **Get-CimInstance -ClassName Win32_ComputerSystem -** Vıpis vırobce a modelu poèítaèe
- **Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object -Property *user*
-** Vıpis místních uivatelù a vlastníkù
- **Get-CimInstance -ClassName Win32_LocalTime** - Získání místního èasu z poèítaèe
- **Get-CimInstance -ClassName Win32_Service | Select-Object -Property
Status,Name,DisplayName -** Pokud chcete zobrazit stav všech slueb v urèitém poèítaèi,
mùete pouít Get-Service rutinu místnì. Pro vzdálené systémy mùete pouít
Win32_Service tøídy WMI. Pokud pouijete Select-Object k filtrování vısledkù na stav,
názeva Zobrazovanınázev, bude vıstupní formát témìø totonı s tímto formátem Get-
Service
- Clipboard (schránkou – ctrl + c/v)

- **_Set-Clipboard -Value "Tohle je pokus"_** **-** vloí tento text do schránky a kdy pak nìkde
zmáènete ctrl+v tak se vloí “Tohle je pokus”
- **_Get-Date | Set-Clipboard_** **-** “05/22/2019 23:07:21”
- **_Get-Date |Out-String | Set-Clipboard_** - "støeda 22. kvìtna 2019 23:07:54”



