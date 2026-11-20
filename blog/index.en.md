# Warehouse for the POHODA Accounting System

An example warehouse management application built as an extension to the POHODA accounting system. It is intended to provide POHODA's stock functions and extend them with item variants and warehouse locations.

Planned features include:

- goods receipts and issues,
- tracking and reporting item variants such as type or color,
- receiving and issuing goods by warehouse location,
- an overview of warehouse space usage and current stock levels.

## 1. Configure POHODA

In POHODA, open the accounting unit and select **Database / POHODA mServer**. In the dialog, create a new record with a name, the selected accounting unit, and port `666`.

## 2. Configure the warehouse application

In the application directory, edit `warehouse.ini` and set the company ID (IČO) of the accounting unit selected in POHODA mServer:

```ini
[Pohoda]
AccountingUnitIco="06109918"
```

After starting the application, the **POHODA - Export/Import log** window shows the accounting units it has read. The POHODA mServer window shows the incoming HTTP POST request.

## 3. Import data into the warehouse application

In the application, synchronize these records in order:

1. **StockView / Sync** – stock items (existing stock cards) from POHODA.
2. **SupplierView / Sync** – the supplier list from POHODA.
3. **StorageView / Sync** – the warehouse list from POHODA.

The data is stored in the local `warehouse.db` database and used for warehouse operations:

- **Goods receipt** – putting goods into stock.
- **Goods issue** – taking goods out of stock.

## 4. Goods receipt

A goods receipt records materials put into stock. Enter:

- the receipt date,
- a supplier from the POHODA supplier list,
- the item (material, variant, and unit) from the imported stock cards,
- the quantity and warehouse location.

## 5. Goods issue

A goods issue records materials taken out of stock. Enter:

- the issue date,
- the customer available from POHODA data,
- the item (material, variant, and unit) from the imported stock cards,
- the quantity and warehouse location.

## 6. Stock movements

Each goods receipt and issue is recorded as a stock movement. The record includes the POHODA document number and status (OK or error), the item and supplier or customer, the date and movement type, the quantity moved, and the total stock level after the movement.

## 7. Warehouse locations

A warehouse location can have up to four levels: section, rack, shelf, and place on the rack. For each movement, the application checks:

- whether goods are received into an empty location or one holding the same material,
- whether an issue is made from a location containing the requested material and quantity,
- the total load on the rack.

The application also supports dark mode.

## Application screenshots

![Warehouse application interface](../screenshots/warehouse01.png)
![Warehouse application interface in dark mode](../screenshots/warehouse02.png)

## Downloads

The application source and files are available in the [WarehouseUIv1 repository](https://github.com/CodElecCz/pohoda-warehouse-management).
