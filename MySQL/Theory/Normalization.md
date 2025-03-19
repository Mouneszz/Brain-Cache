### **1st Normal Form (1NF)**
- Ensure atomicity: Each column must have **single, indivisible** values.
- Each column must have values of a **single type**.
- Each row must be **unique** (Primary Key required).
- No **repeating groups** (no multiple values in a single column).

**Violates 1NF**

| student_id | Name  | Place              |
| ---------- | ----- | ------------------ |
| 101        | Alice | Newyork,Sowkarpeat |
| 102        | Bob   | Ramnagar           |
|            |       |                    |
"Place" column contains multiple values.

To Normalize the above table we have to create a separate row for `sowkarpeat`

### **2nd Normal Form (2NF)**

- Must be in **1NF**.
- Remove **partial dependencies** (all non-key attributes must depend on the **whole primary key**, not just a part of it).

**Violates 2NF**
`primary key(order_id,product)`

| Order_id | Product | Name  |
| -------- | ------- | ----- |
| 1        | Mango   | Alice |
| 1        | Apple   | Alice |
| 2        | Orange  | Bob   |
Here its 1NF
But  `Name` is only depends on `order_id`,if we remove the product we can still get the `Name` using `order_id` .

To Normalize we have to split the table into two

One table with only `order_id` and `Name` 
`Name`  depends fully on `order_id`

One table with only `order_id` (referenced from above table) and `Product`.


### **3rd Normal Form (3NF)**
- Must be in **2NF**.
- Remove **transitive dependencies** (non-key attributes must depend **only on the primary key**, not on other non-key attributes).

**Violates 3NF**

| order_id | customer_name | customer_city |
| -------- | ------------- | ------------- |
| 1        | Alice         | Chennai       |
| 2        | Bob           | Erode         |
- if we know `customer_name` , without `order_id ` we can get the `customer_city`
Here the `customer_city` not depends on `order_id` only on `customer_name`.
So we have to split the table into two

- **Before 3NF**: `Customer_Name` was used as an identifier, but names are **not unique** and can cause redundancy.
- **After 3NF**: We introduce `Customer_ID` as a **Primary Key** in `Customers`, and use it as a **Foreign Key** in `Orders`.

Customer table
we make a customer table with creating a new `customer_id` as PK and `customer_name` ,`customer_city`.

Order table
we  get the `customer_id` as FK and `order_id` as PK
