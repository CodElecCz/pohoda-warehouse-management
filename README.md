# WarehouseUIv1

WarehouseUIv1 is a Qt desktop application that extends [POHODA](https://www.stormware.cz/) with warehouse management.

## Features

- Synchronize stock items, suppliers, and warehouses with POHODA through mServer.
- Create goods receipts and issues, and review stock movement history.
- Track item variants and up to four levels of warehouse locations.
- Review stock levels, location occupancy, and rack loads.
- Switch between light and dark themes.

## Run the Windows build

A 64-bit Windows build and its Qt runtime files are included in [`bin/MSVC2017_64/`](bin/MSVC2017_64/). Run `Warehouse.exe` from that directory. Configure the POHODA mServer connection in `Warehouse.ini` for your accounting unit before synchronizing data.

## Build from source

The project uses Qt 5.11.2 and qmake. Open [`WarehouseUI_64.pro`](WarehouseUI_64.pro) in Qt Creator with a matching 64-bit MSVC 2017 kit, then build the `Warehouse` target. The qmake project uses the Qt Core, GUI, Widgets, SQL, XML, and Network modules.

## Interface

![Warehouse application interface](screenshots/warehouse01.png)
![Warehouse application interface in dark mode](screenshots/warehouse02.png)

## Project articles

- [English article](https://codeleccz.github.io/en/blog/sklad-pohoda/)
- [Český článek](https://codeleccz.github.io/blog/sklad-pohoda/)

The source articles and screenshots are also available in [`blog/`](blog/).
