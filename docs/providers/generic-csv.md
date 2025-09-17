# Generic CSV (scaffold)

For custom sources. Expect CSVs for entities with required columns.

## Entities & Required Columns (proposed)
- customers: id,email,created_at
- products: id,name
- prices: id,product_id,currency,unit_amount,interval
- subscriptions: id,customer_id,price_id,status,start_date
- invoices: id,customer_id,total,currency,issued_at
- payments: id,invoice_id,amount,currency,paid_at

## Notes
- Use ISO8601 timestamps
- Use lowercase ISO currency codes (e.g., usd, eur)
- Prefer stable external IDs
