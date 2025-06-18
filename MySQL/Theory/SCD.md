#### **Slowly Changing Dimensions**
#### **1️⃣ SCD Type 1 (Overwrite Data)**

- Updates the existing record, **no history maintained**.
- Used when historical changes are **not important**.
- **Example:** If a customer's address changes, the old address is replaced with the new one.

#### **2️⃣ SCD Type 2 (Maintain History)**

- Keeps **historical versions** of data.
- Uses **effective date, end date, and active flag** to track changes.
- **Example:** If a product price changes, a new row is inserted with a new date range.

#### **3️⃣ SCD Type 3 (Add New Column)**

- Stores the **previous value** in a separate column.
- Limited history is maintained.
- **Example:** A table has `current_address` and `previous_address` columns.
