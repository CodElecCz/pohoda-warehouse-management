# Sklad pro účetní program POHODA

Ukázka aplikace pro správu skladu jako nástavby účetního programu POHODA. Aplikace má nabídnout funkce skladu z POHODY a rozšířit je o evidenci variant zboží a skladových pozic.

Mezi zamýšlené funkce patří:

- příjemky a výdejky,
- evidence a reportování variant zboží, například typu nebo barvy,
- příjem a výdej zboží podle pozice ve skladu,
- přehled vytížení prostoru skladu a aktuálního stavu zásob.

## 1. Nastavení programu POHODA

V programu POHODA otevřete účetní jednotku a zvolte **Databáze / POHODA mServer**. V dialogovém okně vytvořte nový záznam s názvem, vybranou účetní jednotkou a portem `666`.

## 2. Nastavení programu Sklad

V adresáři aplikace upravte v souboru `warehouse.ini` identifikátor IČO účetní jednotky, kterou jste vybrali v POHODA mServeru:

```ini
[Pohoda]
AccountingUnitIco="06109918"
```

Po spuštění aplikace se v okně **POHODA - Export/Import log** zobrazí načtené účetní jednotky. V okně POHODA mServeru se objeví záznam příchozího požadavku HTTP POST.

## 3. Import dat do programu Sklad

V aplikaci postupně synchronizujte:

1. **StockView / Sync** – skladové položky (založené skladové karty) z POHODY.
2. **SupplierView / Sync** – seznam dodavatelů z POHODY.
3. **StorageView / Sync** – seznam skladů z POHODY.

Data se uloží do lokální databáze `warehouse.db`. Z ní aplikace vybírá podklady pro skladové operace:

- **Příjemka** – naskladnění zboží.
- **Výdejka** – vyskladnění zboží.

## 4. Příjemka

Příjemka slouží k naskladnění materiálu. Vyplňují se tyto údaje:

- datum naskladnění,
- dodavatel vybraný z importovaného seznamu POHODY,
- položka: materiál, varianta a měrná jednotka podle importovaných skladových karet,
- množství a pozice ve skladu.

## 5. Výdejka

Výdejka slouží k vyskladnění materiálu. Vyplňují se tyto údaje:

- datum vyskladnění,
- odběratel podle dat dostupných z POHODY,
- položka: materiál, varianta a měrná jednotka podle importovaných skladových karet,
- množství a pozice ve skladu.

## 6. Skladové pohyby

Každá příjemka a výdejka se zaznamená jako skladový pohyb. Záznam obsahuje číslo dokladu z POHODY a jeho stav (OK nebo chyba), identifikaci zboží a dodavatele či odběratele, datum a typ pohybu, množství položek a celkový stav skladu po provedení pohybu.

## 7. Skladové pozice

Skladová pozice může mít až čtyři úrovně: sekci, regál, patro a místo v regálu. Při skladových pohybech aplikace kontroluje:

- zda se zboží přijímá na prázdnou pozici nebo na pozici obsazenou stejným materiálem,
- zda výdej probíhá z pozice obsahující daný materiál a požadované množství,
- celkové zatížení regálu.

Aplikace podporuje také tmavý režim.

## Ukázky aplikace

![Rozhraní aplikace Sklad](../screenshots/warehouse01.png)
![Rozhraní aplikace Sklad v tmavém režimu](../screenshots/warehouse02.png)

## Soubory ke stažení

Zdrojový kód a soubory aplikace jsou dostupné v [repozitáři WarehouseUIv1](https://github.com/CodElecCz/pohoda-warehouse-management).
