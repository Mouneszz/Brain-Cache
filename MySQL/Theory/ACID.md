ACID ensures **data integrity, reliability, and consistency** in relational databases like MySQL. It stands for:

#### **1️⃣ Atomicity (All or Nothing)**

- A transaction must be **fully completed** or **rolled back** if any part fails.
- **Example:** In a bank transfer, either **both debit and credit** happen or neither does.

#### **2️⃣ Consistency (Valid State Transitions)**

- The database moves from **one valid state to another**.
- No partial or invalid data should exist after a transaction.
- **Example:** A product’s stock cannot become negative after a purchase.

#### **3️⃣ Isolation (No Interference)**

- Transactions **execute independently** and don’t affect each other.
- Prevents issues like **dirty reads, phantom reads, and lost updates**.
- **Example:** Two users booking the last movie ticket should not cause double booking.

#### **4️⃣ Durability (Permanent Changes)**

- Once a transaction is committed, **data remains saved** even if the system crashes.
- **Example:** A confirmed online order remains even after a power failure.