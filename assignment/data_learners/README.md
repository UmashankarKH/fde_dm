# Kaveri Kitchen Supplies: learner data

Four teams, four systems, four folders. Each folder is what that team exported. There is **no shared key** between the folders, and that is intentional. Finding and documenting the links is part of your job.

Every file is UTF-8 CSV with a header row. Dates are `YYYY-MM-DD`. All names, emails and figures are fictional.

---

## team_sales/orders.csv (sales CRM export, 80 rows)

| Column | Meaning |
|---|---|
| order_id | Sales order number, format `SO-1001` |
| customer_name | Customer's trading name, as typed by sales |
| customer_email | Customer's email. **Mixed case, and must be masked before AI use** |
| order_date | Date the order was taken |
| product_name | Product name as typed by sales. **No SKU code** |
| qty | Quantity ordered |
| promised_ship_date | Date sales promised the customer |
| sales_rep | Sales person who took the order |

## team_warehouse/stock_movements.csv (warehouse system export, 104 rows)

| Column | Meaning |
|---|---|
| movement_id | Unique movement number |
| sku | Product code, format `KK-001` |
| product_name | Product name as stored by the warehouse |
| movement_type | `IN` (stock received) or `OUT` (stock shipped) |
| qty | Quantity moved |
| movement_date | Date of the movement |
| location | Warehouse location (one location, `MAIN-WH`, in this pilot) |

## team_warehouse/deliveries.csv (warehouse delivery export, 80 rows)

| Column | Meaning |
|---|---|
| delivery_id | Unique delivery number |
| order_ref | The sales order this delivery serves, format `SO1001` (**no dash**) |
| sku | Product code |
| delivered_qty | Quantity actually delivered. Can be less than ordered if stock ran short |
| delivery_date | Date of delivery |

## team_finance/invoices.csv (accounting export, 80 rows)

| Column | Meaning |
|---|---|
| invoice_no | Unique invoice number, format `INV-2026-0001` |
| customer_code | Finance customer code, format `CUST-101` |
| customer_name | Customer's legal name in finance. **May differ slightly from sales** |
| invoice_date | Date the invoice was raised |
| total_amount | Total including 18% GST |
| status | `Paid`, `Open` or `Overdue` |

## team_finance/invoice_lines.csv (accounting export, 80 rows)

| Column | Meaning |
|---|---|
| invoice_no | Invoice this line belongs to |
| sku | Product code |
| billed_qty | Quantity billed to the customer |
| unit_price | Price per unit before GST |
| line_amount | billed_qty multiplied by unit_price, before GST |

**Note:** finance has no order number on any invoice. You will need to link invoices to orders another way.

## team_service/returns.csv (customer service log, 15 rows)

| Column | Meaning |
|---|---|
| return_id | Unique return number |
| customer_email | Customer's email, **lower case, must be masked before AI use** |
| sku | Product code |
| return_qty | Quantity returned |
| return_date | Date the return was logged |
| reason | Reason given by the customer |
| original_order_ref | Order number typed by the service agent. **May be blank, or in either format** |

---

## Product list (for reference)

| SKU | Product name |
|---|---|
| KK-001 | Pressure Cooker 5L |
| KK-002 | Non-stick Kadai 26cm |
| KK-003 | Gas Stove 3 Burner |
| KK-004 | Mixer Grinder 750W |
| KK-005 | Chef Knife Set |
| KK-006 | Steel Tiffin Box |
| KK-007 | Induction Cooktop |
| KK-008 | Water Filter 10L |
| KK-009 | Cutting Board Set |
| KK-010 | Electric Kettle 1.5L |

Prices are in the finance `invoice_lines` file, in the `unit_price` column.
