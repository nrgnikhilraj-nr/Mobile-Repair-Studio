# Database Schema — RepairOS

> In this project, the "database" is an in-memory JavaScript object (`db`) that mimics a relational database. In a production system, this would be replaced with MySQL / PostgreSQL.

---

## Tables

### 1. `tickets`
Stores all repair job records.

| Field      | Type    | Description                              |
|------------|---------|------------------------------------------|
| id         | STRING  | PK — format: TKT-XXXX                   |
| customer   | STRING  | Customer full name                       |
| phone      | STRING  | 10-digit mobile number                   |
| email      | STRING  | Customer email                           |
| brand      | STRING  | Device brand (Apple, Samsung, etc.)      |
| model      | STRING  | Device model name                        |
| issue      | STRING  | Type of repair (Screen, Battery, etc.)  |
| tech       | STRING  | FK → Technician name                     |
| priority   | ENUM    | Normal / High / Urgent                   |
| status     | ENUM    | Pending → Diagnosing → In Progress → Ready → Completed |
| cost       | INTEGER | Estimated repair cost in INR             |
| desc       | TEXT    | Detailed problem description             |
| imei       | STRING  | 15-digit IMEI or serial number           |
| date       | DATE    | Ticket creation date (YYYY-MM-DD)        |

---

### 2. `customers`
Auto-aggregated from tickets. Each unique phone number = one customer.

| Field     | Type    | Description                     |
|-----------|---------|---------------------------------|
| id        | STRING  | PK — format: CUS-XXX            |
| name      | STRING  | Customer name                   |
| phone     | STRING  | Unique phone (natural key)      |
| email     | STRING  | Customer email                  |
| address   | TEXT    | Address                         |
| repairs   | INTEGER | Count of all tickets            |
| spent     | INTEGER | Sum of completed ticket costs   |
| lastVisit | DATE    | Date of most recent ticket      |
| status    | ENUM    | Active / Inactive               |

---

### 3. `inventory`
Parts and components stock ledger.

| Field     | Type    | Description                     |
|-----------|---------|---------------------------------|
| id        | STRING  | PK — format: SKU-XXX            |
| name      | STRING  | Part name                       |
| sku       | STRING  | Stock Keeping Unit code         |
| category  | STRING  | Screen / Battery / Tools / etc. |
| compat    | STRING  | Compatible device models        |
| supplier  | STRING  | Supplier name                   |
| costPrice | INTEGER | Purchase price (INR)            |
| sellPrice | INTEGER | Selling price (INR)             |
| qty       | INTEGER | Current stock quantity          |
| reorder   | INTEGER | Reorder trigger level           |

---

### 4. `invoices`
Billing records linked to completed tickets.

| Field     | Type    | Description                     |
|-----------|---------|---------------------------------|
| id        | STRING  | PK — format: INV-XXXX           |
| ticketId  | STRING  | FK → tickets.id                 |
| customer  | STRING  | Customer name (denormalized)    |
| device    | STRING  | Device summary                  |
| issue     | STRING  | Issue type                      |
| labour    | INTEGER | Labour charge (INR)             |
| parts     | INTEGER | Parts cost (INR)                |
| discount  | INTEGER | Discount applied (INR)          |
| total     | INTEGER | Final amount (INR)              |
| date      | DATE    | Invoice date                    |
| status    | ENUM    | Paid / Unpaid                   |

---

## Relationships

```
tickets ──< invoices    (one ticket → one invoice)
tickets >── customers   (many tickets → one customer via phone)
inventory               (standalone, used by technicians during repair)
```
