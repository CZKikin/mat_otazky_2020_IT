# Bootování operačního systému a souborové systémy

Master Boot Record, boot sektor, fáze bootování operačního systému, geometrie pevných
disků, metody přístupu na disk, souborový systém FAT32, souborový systém NTFS, linuxové
souborové systémy (ext2, ext3)

## Master boot record

- Master boot record = **hlavní spouštěcí záznam** ( obdoba boot sektoru).
- Je umístěn v **prvním sektoru pevného disku** (nebo obdobného média), tj. na jeho
    úplném začátku.
- Jeho velikost je **512 bajtů** a je v něm umístěn:
    o Zavaděč OS, kterému BIOS předává při startu počítače řízení
    o Tabulka rozdělení disku na logické části (oddíly) – partition table
    o Číselný identifikátor disku
- MBR dokáže adresovat **maximálně 2 TB disky**. Jeho nástupcem je GPT (GUID
    Partition Table).
- Master boot record je vždy uložen na samém počátku disku (podle Cylindr-Hlava-
    Sektor = 0- 0 - 1, podle LBA v sektoru 0) a skládá se ze 2 hlavních částí.

### Hlavní tabulka rozdělení disku (MPT)

- **Master Partition Table**
- Obsahuje **seznam logických oddílů** na daném fyzickém disku a **informace o umístění**
    **zaváděcích sektorů** (boot sektorů) jednotlivých disků.
- Tato tabulka může obsahovat **MAXIMÁLNĚ 4 ZÁZNAMY** – je-li potřeba disk rozdělit
    na více logických oblastí, potom některý ze 4 záznamů odkazuje na **tzv. Extended**
    **partition table** (rozšířená tabulka rozdělení disku), která může obsahovat až 4
    záznamy.
- Disk se dělí na **primární oddíly** (primary partition), jeden oddíl z nich může být
    označený jako **rozšířený oddíl** (extended partition) – v rožšířeném oddíle lze vytvořit
    „libovolný“ počet logických oddílů (omezený velikostí disku či možnostmi OS).

### Hlavní spouštěcí kód – kód zavaděče

- Jedná se o krátký úsek kódu, který je při startu počítače zaveden BIOSem do paměti
    počítače a následně je spuštěn.
- Jeho úkolem je načíst do paměti zaváděcí (boot) sektor z oddílu, ze kterého má být
    zaveden OS a spustit ho.


## Fáze bootování operačního systému

- **Bootování je spouštění operačního systému.**
- Bootování se skládá z následujících fází:
    o Diagnostika hardware
    o Kontrola paměti
    o Inicializace vestavěného BIOSu
    o Inicializace doplňkových součástí hardware a jejich BIOSů
    o Nabootování OS

### Bootování do Windows

- Pro pokročilou nabídku startu OS stiskněte při startu počítače F8. To má za výsledek
    to, že na výběr dostaneme možnost spustit stav **běžným způsobem** , **spustit systém**
    **ve stavu nouze** , **spustit s diagnostikou** apod.

### Výběr z více operačních systémů Windows

- Chceme-li na svůj počítač nainstalovat více operačních systémů, postupujte tak, že
    nejprve nainstalujete starší systém a na další diskový oddíl pak nainstalujeme systém
    novější. Opačný postup by měl za následek to, že by nebylo možné původní systém
    spustit = **starší verze systému nezná způsob zavádění nového systému a přepíše jej**.

### Boot manager

- Možnost instalace staršího operačního systému vedle systému novějšího (např.
    instalace Windows 7 vedle Windows 10), nám umožňuje utilita manažer bootování –
    **Boot Manager** = jeho hlavní funkcí je možnost vybrání systému nebo jednotky, ze
    které bude bootování probíhat.

## Geometrie pevných disků

- Všechny jednotlivé disky, ze kterých se celý pevný disk skládá, jsou podobně jako u
    pružného disku **rozděleny do soustředěných kružnic nazývaných stopy** (tracks) a
    každá z těchto stop je rozdělena do **sektorů** (sectors). Množina všech stop na všech
    discích se stejným číslem se u pevných disků označuje jako **válec** (cylinder).
- Geometrie disku udává hodnoty následujících parametrů:

### Hlavy disku (heads)

- **Počet čtecích** (zapisovacích) **hlav pevného disku**.
- Tento počet je shodný s počtem aktivních ploch, na které se provádí záznam.
- Většinou každý jednotlivý disk má dvě aktivní plochy a k nim příslušné čtecí
    (zapisovací) hlavy.

### Stopy disku (tracks)

- **Počet stop na každé aktivní ploše disku**.
- Stopy disku bývají číslovány od nuly, přičemž číslo nula má vnější stopa disku.

### Cylindry disku (cylinders)

- **Počet cylindrů pevného disku** (tento počet je shodný s počtem stop).
- Číslování cylindrů je shodné s číslováním stop.

### Sektory disku (sectors)

- **Počet sektorů, na které je rozdělena každá stopa**.
- Sektory bývají číslovány **od jedničky**.
- U většiny pevných disků je počet sektorů na všech stopách stejný.
- Tento způsob do jisté míry plýtvá médiem, protože vnější stopy jsou delší, a tudíž by
    se na ně mohlo umístit více sektorů – tento problém řeší zonální zápis označovaný
    jako ZBR (Zone Bit Recording), který dovoluje umístit na vnější stopy pevného disku
    větší počet sektorů než na stopy vnitřní.

## Metody přístupu na disk

- Pro přístup k datům disku se používala starší metoda adresace disku **Cylindr-Hlava-**
    **Sektor** , která disk adresuje podle jeho geometrie. Hlavní nevýhodou byla u osobních
    počítačů IBM PC **omezená kapacita** takto adresovaného disku a software **musel**
    **rozlišovat různé geometrie disku**.
- Novější metoda adresování disku se označuje jako **LBA** (Local Block Addressing) a
    **není třeba znát geometrii disku** a je možné adresovat až **144 miliónů GB**.


## Souborové systémy

### FAT

- Vyšel v roce 1997.
- Přináší 32bitové adresy clusterů, kde číslo alokační jednotky využívá 28 bitů, takže
  není vhodný pro ukládání velkých souborů.
- Náchylný k chybám, nemá žurnálování.
- Jednoduchý na implementaci.

### NTFS

- Zaveden ve Windows NT (Windows pro IBM PC).
- Obvykle menší clustery než u FAT32.
- Názvy souborů v UTF8.
- Podporuje šifrování.
- Problematická podpora mimo systém Windows.
- Problémy s fragmentací = nutná pravidelná defragmentace (ve Windows 7 se spouští
  automaticky).
- Upravený systém žurnálování (všechny zápisy na disk se zároveň zaznamenávají do
    speciálního souboru).

### ext2

- Linuxový souborový systém.
- Rozšíření původního systému ext.
- Implementovaný v Unixových systémech, standardní volba pro většinu linuxových
    distribucí.

### ext3

- Kompatibilní s ext2.
- Přidáno žurnálování.
- Chybí klasická defragmentace disku a transparentní komprese.
- Kontrola disku jen v režimu read-only.

### Žurnálování

- Vytváření libovolných podrobných **záznamů o prováděné činnosti** (logů).
    - Do žurnálu je zapsáno, co a kde se bude měnit.
    - Je provedena vlastní série změn.
    - Do žurnálu je zapsáno, že operace byla úspěšně dokončena.
    - Záznam v žurnálu je zrušen.
- Pokud dojde v kterémkoliv okamžiku k přerušení, je možné pomocí dat v žurnálu
    uvést systém souborů do konzistentního stavu.
`
```
Autor: Filip Valenta
Merger: Vít Staniček
Datum: 6.5.2020
```