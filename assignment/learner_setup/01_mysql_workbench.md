# Setup 01: MySQL and MySQL Workbench

**Goal:** by the end of this page, you can open MySQL Workbench, connect to a local MySQL server, and load the four team CSV files into tables.

**Time needed:** about 45 minutes the first time.

---

## Step 1: Install MySQL Server and Workbench

1. Go to https://dev.mysql.com/downloads/installer/ and download **MySQL Installer for Windows** (the larger file, with the full installer).
2. Run the installer. Choose **Developer Default** when asked. It installs both MySQL Server and MySQL Workbench.
3. When asked for a root password, choose one you will remember and write it in a safe place (not in your repository). Keep the default port **3306**.
4. Finish the installer. Open **MySQL Workbench** from the Start menu.

*Mac and Linux users: download the matching installer from the same site. The steps below are the same.*

---

## Step 2: Create a connection

1. On the Workbench home screen, click the **+** next to "MySQL Connections".
2. Fill in:
   - **Connection name:** `kaveri-local`
   - **Hostname:** `127.0.0.1`
   - **Port:** `3306`
   - **Username:** `root`
3. Click **Test Connection**, type your root password, then click **OK**.
4. Open the connection. The **Navigator** panel on the left shows the server.

**Turn on local file loading** (needed for Step 4):
1. Right-click the connection, choose **Edit Connection**.
2. Open the **Connection** tab, then the **Advanced** sub-tab. In the box called "Others", add this line on its own line: `OPT_LOCAL_INFILE=1`
3. Click **OK**, then reconnect.

---

## Step 3: Create one database per team

Open a new SQL tab (the icon with the `SQL` symbol, or **File > New Query Tab**). Paste and run:

```sql
CREATE DATABASE IF NOT EXISTS raw_sales;
CREATE DATABASE IF NOT EXISTS raw_warehouse;
CREATE DATABASE IF NOT EXISTS raw_finance;
CREATE DATABASE IF NOT EXISTS raw_service;
SET GLOBAL local_infile = 1;
```

Click the lightning-bolt icon (**Execute**) or press **Ctrl+Shift+Enter**. Then press the refresh icon in the Navigator. You should see the four `raw_` databases.

*Why four databases?* Each team's data stays in its own place, the same as in real life. You will link them with queries, not by copying them into one table.

---

## Step 4: Load the CSV files

Use a **raw** table for each file. Raw means every column is text, so nothing is lost while you explore. You will clean and type the data later.

Replace `C:/path/to/data_learners` below with the real folder path on your computer. Use forward slashes.

```sql
-- Sales orders
CREATE TABLE raw_sales.orders (
  order_id VARCHAR(20), customer_name VARCHAR(100), customer_email VARCHAR(150),
  order_date VARCHAR(20), product_name VARCHAR(100), qty VARCHAR(10),
  promised_ship_date VARCHAR(20), sales_rep VARCHAR(50)
);
LOAD DATA LOCAL INFILE 'C:/path/to/data_learners/team_sales/orders.csv'
INTO TABLE raw_sales.orders
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

-- Warehouse stock movements
CREATE TABLE raw_warehouse.stock_movements (
  movement_id VARCHAR(20), sku VARCHAR(20), product_name VARCHAR(100),
  movement_type VARCHAR(5), qty VARCHAR(10), movement_date VARCHAR(20), location VARCHAR(20)
);
LOAD DATA LOCAL INFILE 'C:/path/to/data_learners/team_warehouse/stock_movements.csv'
INTO TABLE raw_warehouse.stock_movements
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

-- Warehouse deliveries
CREATE TABLE raw_warehouse.deliveries (
  delivery_id VARCHAR(20), order_ref VARCHAR(20), sku VARCHAR(20),
  delivered_qty VARCHAR(10), delivery_date VARCHAR(20)
);
LOAD DATA LOCAL INFILE 'C:/path/to/data_learners/team_warehouse/deliveries.csv'
INTO TABLE raw_warehouse.deliveries
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

-- Finance invoices
CREATE TABLE raw_finance.invoices (
  invoice_no VARCHAR(20), customer_code VARCHAR(20), customer_name VARCHAR(100),
  invoice_date VARCHAR(20), total_amount VARCHAR(20), status VARCHAR(20)
);
LOAD DATA LOCAL INFILE 'C:/path/to/data_learners/team_finance/invoices.csv'
INTO TABLE raw_finance.invoices
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

-- Finance invoice lines
CREATE TABLE raw_finance.invoice_lines (
  invoice_no VARCHAR(20), sku VARCHAR(20), billed_qty VARCHAR(10),
  unit_price VARCHAR(20), line_amount VARCHAR(20)
);
LOAD DATA LOCAL INFILE 'C:/path/to/data_learners/team_finance/invoice_lines.csv'
INTO TABLE raw_finance.invoice_lines
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

-- Service returns
CREATE TABLE raw_service.returns (
  return_id VARCHAR(20), customer_email VARCHAR(150), sku VARCHAR(20),
  return_qty VARCHAR(10), return_date VARCHAR(20), reason VARCHAR(100),
  original_order_ref VARCHAR(20)
);
LOAD DATA LOCAL INFILE 'C:/path/to/data_learners/team_service/returns.csv'
INTO TABLE raw_service.returns
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;
```

**Check the load:** each query should return the row count below.

```sql
SELECT COUNT(*) FROM raw_sales.orders;            -- 80
SELECT COUNT(*) FROM raw_warehouse.stock_movements; -- 104
SELECT COUNT(*) FROM raw_warehouse.deliveries;    -- 80
SELECT COUNT(*) FROM raw_finance.invoices;        -- 80
SELECT COUNT(*) FROM raw_finance.invoice_lines;   -- 80
SELECT COUNT(*) FROM raw_service.returns;         -- 15
```

If a count is lower than expected, the usual cause is line endings or a wrong path. Check the path first.

---

## Step 5: Try a first query

```sql
-- How many orders did sales take per product name?
SELECT product_name, COUNT(*) AS orders, SUM(CAST(qty AS UNSIGNED)) AS units
FROM raw_sales.orders
GROUP BY product_name
ORDER BY units DESC;
```

If you see a table of results, your setup works.

---

## Step 6: Save your work in version control

- Save each query in a `.sql` file inside your repository's `sql/` folder.
- Never save the root password in a file.
- Commit with a clear message, for example `add profiling queries`.

---

## Common problems

| Problem | Fix |
|---|---|
| `Error 3950: LOAD DATA LOCAL is disabled` | Run `SET GLOBAL local_infile = 1;` and check the `OPT_LOCAL_INFILE=1` setting in the connection's Advanced tab. Reconnect. |
| `Can't open file` | Check the path. Use forward slashes. The file must exist exactly as named. |
| Count is too low | Make sure the file has a header row and uses Unix or Windows line endings consistently. |
| Accented or odd characters | Open the CSV in Notepad and save it as UTF-8. |
| Workbench is slow | Close other query tabs. Your data is small, so this should be rare. |
