# 9. Databáze...............................................................................................................................................

Databáze (neboli datová základna, též databanka) je systém souborů s pevnou strukturou záznamů. Tyto
soubory jsou mezi sebou navzájem propojeny pomocí klíčů. V širším smyslu jsou součástí databáze i
softwarové prostředky, které umožňují manipulaci s uloženými daty a přístup k nim. Tento software se v
české odborné literatuře nazývá systém řízení báze dat (SŘBD). Běžně se označením _databáze_ – v
závislosti na kontextu – myslí jak uložená data, tak i software (SŘBD).

## Historie................................................................................................................................................

Předchůdcem databází byly papírové kartotéky. Umožňovaly uspořádávání dat podle různých kritérií a
zatřiďování nových položek. Veškeré operace s nimi prováděl přímo člověk. Správa takových kartoték byla
v mnohém podobná správě dnešních databází.

Velkým impulsem pro další rozvoj databází byl překotný vývoj počítačů v padesátých letech 20. století.
Ukázalo se, že původně univerzální používání strojového kódu procesorů je (nejen) pro databázové úlohy
neefektivní, a proto se objevil požadavek na vyšší jazyk pro zpracování dat.

V roce 1970 začínají zveřejněním článku E. F. Codda první **relační databáze** , které pohlížejí na data jako
na tabulky. Kolem roku 1974 se vyvíjí první verze dotazovacího jazyka SQL. Vývoj této technologie po 10
letech přinesl výkonově použitelné systémy, srovnatelné se síťovými a hierarchickými databázemi.

V 90. letech 20. století se začínaly objevovat první **objektově** orientované databáze, jejichž filozofie byla
přebírána z objektově orientovaných jazyků. Tyto databáze měly podle předpokladů vytlačit relační
systémy. Původní předpoklady se však nenaplnily a vznikla kompromisní **objektově-relační** technologie.

## Databázové modely.............................................................................................................................

Z hlediska způsobu ukládání dat a vazeb mezi nimi dělíme databáze do základních typů:

### Hierarchický model dat...................................................................................................................

Data jsou organizována do stromové struktury. Každý záznam představuje uzel ve stromové struktuře,
vzájemný vztah mezi záznamy je typu rodič/potomek. Nalezení dat v hierarchické databázi vyžaduje


navigaci přes záznamy směrem na potomka, zpět na rodiče nebo do strany na dalšího potomka.
Největšími nevýhodami hierarchického uspořádání je složitá operace vkládání a rušení záznamů a v
některých případech i nepřirozená organizace dat.

```
Obr. 1 - Hierarchický model
```
### Síťový model dat............................................................................................................................

Síťový model dat je v podstatě zobecněním hierarchického modelu, který doplňuje o mnohonásobné
vztahy (sety). Tyto sety propojují záznamy různého či stejného typu, přičemž spojení může být
realizováno na jeden nebo více záznamů. Přístup k propojeným záznamům je přímý bez dalšího
vyhledávání, k dispozici jsou operace: nalezení záznamu podle klíče, posun na prvního potomka v
dílčím setu, posun stranou na dalšího potomka v setu, posun nahoru z potomka na jeho rodiče v jiném
setu. Nevýhodou síťové databáze je zejména nepružnost a obtížná změna její struktury.

```
Obr. 2 - Síťový model
```
### Relační model dat...........................................................................................................................

Relační databázový model je z uvedených nejmladší a zároveň nejpoužívanější. V roce 1970 byl popsán
Dr. Coddem. V současnosti je nejčastěji využíván u komerčních SŘBD. Model má jednoduchou
strukturu, data jsou organizována v tabulkách, které se skládají z řádků a sloupců. V těchto tabulkách
jsou prováděny všechny databázové operace.


Obr. 3 - Relační model
Databáze dle relačního modelu musí splňovat tyto dvě vlastnosti:

- Databáze je chápana uživatelem jako množina relací a nic jiného.
- V relačním SŘBD jsou k dispozici minimálně operace selekce, projekce a spojení, aniž by se
vyžadovaly explicitně předdefinované přístupové cesty pro realizaci těchto operací.

## SQL Dotazy.........................................................................................................................................

SELECT *
FROM [Temp].[dbo].[udv_SalesByProducts]
WHERE ProduktSubKategorie LIKE ('%bike%')
AND Rok IN (2013,2014)
AND Mesic BETWEEN 1 AND 6
AND PrumernaTrzba>0;

SELECT TOP 10 *
FROM [Temp].[dbo].[udv_SalesByProducts]
WHERE Rok =2013
ORDER BY Trzba DESC;

SELECT
Rok,
SUM(Trzba) AS Soucet,
COUNT(*) AS Pocet_Zaznamu,
AVG(Trzba) AS Prumer,
MAX(Trzba) AS Maximalni_Trzba,
MIN(Trzba) AS Minimalni_Trzba
FROM [Temp].[dbo].[udv_SalesByProducts]
GROUP BY Rok
ORDER BY Rok ASC;

## Normalizace databáze..........................................................................................................................

je v informatice označení postupu, kdy je struktura dat v relační databázi přeorganizována tak, aby
využívala výhody relačního modelu dat. Normalizace databáze umožňuje data efektivněji ukládat,


prohledávat, třídit i zpracovávat. Při normalizaci jsou v databázi měněny atributy (sloupce) jednotlivých
tabulek a zaváděny mezi nimi výhodné vztahy, je omezována redundance uložených dat (vět) a je brán
ohled na řešení problému s případnou nekonzistencí dat.

Autorem termínu normalizace databáze je britsko-americký matematik a informatik Edgar. F. Codd.

### Nultá normální forma (0NF)...........................................................................................................

**Nultá normální forma** bývá obdobně jako nenormalizovaná forma zřídka v literatuře zmiňována. V
některých případech je uváděna jako součást první normální formy. Obvykle není zvažována, jelikož její
splnění bývá v praxi automaticky zaručeno. Přesto lze nalézt následující definici:

Schéma relace je v nulté normální formě právě tehdy, když existuje alespoň jeden atribut, který obsahuje
více než jednu hodnotu

### První normální forma (1NF)...........................................................................................................

Pro splnění **první normální formy** je zapotřebí zajistit následující:

- splnění nulté normální formy (0NF)
- všechny atributy tabulky musí být atomické, tedy dále nedělitelné

### Druhá normální forma (2NF)..........................................................................................................

Pravidla definovaná **druhou normální formou** lze shrnout na následující:

- tabulka musí být v první normální formě (1NF)
- každý neklíčový atribut musí být plně závislý na každém kandidátním klíči (neklíčovým atributem
rozumíme atribut, který není součástí žádného kandidátního klíče)
Druhá normální forma klade důraz především na odstranění možných duplicit v záznamech.

### Třetí normální forma (3NF)............................................................................................................

**Třetí normální forma** klade následující podmínky:

- tabulka je ve druhé normální formě (2NF)
- neobsahuje tranzitivní závislosti