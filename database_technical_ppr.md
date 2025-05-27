
# 📘 Essential Database Concepts: A Technical Overview

## Table of Contents
1. [Introduction](#introduction)
2. [ACID Properties](#acid-properties)
3. [CAP Theorem](#cap-theorem)
4. [Joins](#joins)
5. [Aggregations and Filters](#aggregations-and-filters)
6. [Normalization](#normalization)
7. [Indexes](#indexes)
8. [Transactions](#transactions)
9. [Locking Mechanism](#locking-mechanism)
10. [Database Isolation Levels](#database-isolation-levels)
11. [Triggers](#triggers)
12. [Conclusion](#conclusion)

---

## Introduction

Databases are the backbone of modern software systems, enabling efficient storage, retrieval, and management of data. To design and interact with databases effectively, one must understand foundational concepts that ensure performance, reliability, and consistency.

---

## ACID Properties

ACID is an acronym that represents **Atomicity, Consistency, Isolation, and Durability**, ensuring reliable transaction processing in relational databases.

- **Atomicity**: Ensures that each transaction is "all or nothing". If any part fails, the entire transaction is rolled back.
- **Consistency**: Guarantees that a transaction brings the database from one valid state to another.
- **Isolation**: Transactions occur independently without interference.
- **Durability**: Once a transaction is committed, the changes are permanent, even in the event of a crash.

Example:

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE user_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE user_id = 2;
COMMIT;
```

---

## CAP Theorem

The **CAP Theorem** states that in a distributed data system, you can only guarantee two of the following three:

- **Consistency (C)**: All nodes see the same data at the same time.
- **Availability (A)**: Every request gets a response (success/failure).
- **Partition Tolerance (P)**: The system continues to operate despite network partitions.

| Combination | Description | Example Systems |
|-------------|-------------|-----------------|
| CA (no P)   | Strong but fails under partition | Traditional RDBMS |
| CP (no A)   | Consistent but may reject requests | HBase |
| AP (no C)   | Always responds, but data may be stale | CouchDB |

---

## Joins

Joins combine rows from two or more tables based on a related column.

### Types of Joins:

- **INNER JOIN**: Returns matching rows.
- **LEFT JOIN (OUTER)**: Returns all rows from left table + matches from right.
- **RIGHT JOIN (OUTER)**: All rows from right + matches from left.
- **FULL OUTER JOIN**: All rows when there's a match in one of the tables.
- **CROSS JOIN**: Cartesian product of both tables.

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;
```

---

## Aggregations and Filters

### Aggregation Functions:
- `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`

```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

### Filtering with `WHERE`:

```sql
SELECT * FROM employees WHERE salary > 60000 AND position = 'Manager';
```

---

## Normalization

**Normalization** is the process of organizing data to reduce redundancy and improve integrity.

### Normal Forms:
- **1NF**: Atomic values, unique rows.
- **2NF**: 1NF + no partial dependencies.
- **3NF**: 2NF + no transitive dependencies.
- **BCNF**: Every determinant is a candidate key.

### Benefits:
- Eliminates data redundancy.
- Ensures data integrity.

---

## Indexes

**Indexes** improve query performance by enabling faster data retrieval.

### Types:
- **Single-column index**
- **Composite index**
- **Unique index**
- **Full-text index**
- **B-tree / Hash indexes** (backend dependent)

```sql
CREATE INDEX idx_employee_name ON employees(name);
```

**Pros**:
- Speed up read operations

**Cons**:
- Slower writes (inserts/updates)
- Consumes additional storage

---

## Transactions

A **transaction** is a sequence of operations performed as a single logical unit of work.

```sql
BEGIN;
UPDATE inventory SET stock = stock - 1 WHERE product_id = 101;
INSERT INTO sales(product_id, quantity) VALUES (101, 1);
COMMIT;
```

- Use `ROLLBACK;` to undo operations in case of failure.
- Ensures ACID compliance.

---

## Locking Mechanism

Locks prevent concurrent transaction conflicts.

### Types:
- **Shared Lock (Read)**: Multiple transactions can read but not write.
- **Exclusive Lock (Write)**: Only one transaction can write; no other reads or writes allowed.

### Deadlock:
- Occurs when two or more transactions wait indefinitely for each other to release locks.

Example:

```sql
SELECT * FROM accounts WHERE id = 1 FOR UPDATE;
```

---

## Database Isolation Levels

Isolation levels define the degree to which transactions are isolated from each other.

| Level                | Read Uncommitted | Read Committed | Repeatable Read | Serializable |
|----------------------|------------------|----------------|------------------|--------------|
| Dirty Reads          | ✅               | ❌             | ❌               | ❌           |
| Non-Repeatable Reads | ✅               | ✅             | ❌               | ❌           |
| Phantom Reads        | ✅               | ✅             | ✅               | ❌           |

Set isolation level:

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

---

## Triggers

**Triggers** are procedural code that automatically executes in response to certain events on a table.

### Use Cases:
- Enforce business rules
- Auditing
- Logging changes

```sql
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON employees
FOR EACH ROW
EXECUTE FUNCTION update_modified_column();
```

---

## Conclusion

Understanding these database concepts is essential for designing scalable, efficient, and robust data systems. Mastery of ACID properties, indexing, normalization, and transactional behavior ensures data consistency and performance under various workloads.

---
