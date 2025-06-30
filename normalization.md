# Database Normalization to Third Normal Form (3NF)

## Overview

Normalization is a process to organize database tables to reduce redundancy and improve data integrity. The common normal forms are:

- **1NF (First Normal Form):** All table columns hold atomic (indivisible) values; no repeating groups or arrays.
- **2NF (Second Normal Form):** Meets 1NF and all non-key attributes are fully functionally dependent on the whole primary key (no partial dependency).
- **3NF (Third Normal Form):** Meets 2NF and no transitive dependency exists; non-key attributes depend only on the primary key.

---

## Original Schema Review

### Entities and Attributes:

- **User:** user_id, first_name, last_name, email, password_hash, phone_number, role, created_at
- **Property:** property_id, host_id, name, description, location, pricepernight, created_at, updated_at
- **Booking:** booking_id, property_id, user_id, start_date, end_date, total_price, status, created_at
- **Payment:** payment_id, booking_id, amount, payment_date, payment_method
- **Review:** review_id, property_id, user_id, rating, comment, created_at
- **Message:** message_id, sender_id, recipient_id, message_body, sent_at

---

## Normalization Analysis

### 1NF: Atomicity

- All columns hold atomic values (e.g., no arrays or multiple values per field).
- The schema satisfies 1NF.

### 2NF: No Partial Dependency

- All tables use single-column primary keys (UUIDs), so partial dependency is not possible.
- Non-key columns depend on entire primary key.
- Schema satisfies 2NF.

### 3NF: No Transitive Dependency

- Check if any non-key attribute depends on another non-key attribute instead of the primary key.

**Potential Issues:**

1. **Property Table — `location`**
   - The `location` field is a single string.
   - If the location contains multiple pieces (e.g., city, state, country), then storing all in one column can lead to redundancy if multiple properties share the same city/state.
   - To reduce redundancy and better structure, separate Location into its own table.

2. **User Table — `role`**
   - Role is a single value ENUM; no transitive dependency.

3. **Booking — `total_price`**
   - `total_price` can be calculated from `pricepernight` and number of nights.
   - Storing calculated data may lead to inconsistencies if prices or dates change.
   - Consider removing `total_price` or make sure it’s always consistent.

---

## Proposed Changes for 3NF

### 1. Create a `Locations` Table

Split location into structured fields.
