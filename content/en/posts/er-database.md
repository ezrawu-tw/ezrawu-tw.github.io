---
slug: er-database
title: er_database
date: 2025-10-28 12:11:00
tags:
- database
categories:
  - Note
---
slug: er-database
# ER Database Normalization

## **Purpose — Leave a comment / Edit here**

The purpose is to reduce data **redundancy** and avoid **update anomalies**.

![Untitled](https://hackmd.io/_uploads/SJUsusQ4a.png)


1NF (First Normal Form)

- Each cell (every row and column) can hold only one value
- Each record must have a unique primary key for identification

2NF (Second Normal Form)

- Satisfies 1NF
- Eliminates partial dependencies

3NF (Third Normal Form)

- Satisfies 1NF and 2NF
- Eliminates transitive dependencies

## 1NF (First Normal Form)

- Avoid columns with indeterminate length
- Avoid having two completely identical records

# Database Normalization

---
slug: er-database

## Purpose

The purpose is to reduce data **redundancy** and avoid **update anomalies**.

---
slug: er-database

### Sample Order Table

| Purchase Date | Customer ID | Customer Name | Product Name | Unit Price | Quantity (kg) |
| --- | --- | --- | --- | --- | --- |
| 12/24 | p001 | Ken | Banana | 10 | 5 |
| 12/24 | p002 | Howard | Apple, Banana, Orange | 30, 10, 20 | 2, 4, 1 |
| 12/25 | p003 | Chris | Apple | 30 | 2 |
| 12/25 | p003 | Chris | Apple | 30 | 2 |
| 12/25 | p004 | May | Apple, Orange | 30, 20 | 1, 1 |

---
slug: er-database

1NF (First Normal Form)

- Each cell (every row and column) can hold only one value
- Each record must have a unique primary key for identification

2NF (Second Normal Form)

- Satisfies 1NF
- Eliminates partial dependencies

3NF (Third Normal Form)

- Satisfies 1NF and 2NF
- Eliminates transitive dependencies

---
slug: er-database

## 1NF

- Avoid columns with indeterminate length
- Avoid having two completely identical records

---
slug: er-database

First, split any rows containing multiple values, then assign each order a unique key.

| Purchase Date | Customer ID | Customer Name | Product Name | Unit Price | Quantity (kg) |
| --- | --- | --- | --- | --- | --- |
| 12/24 | p002 | Howard | Apple, Banana, Orange | 30, 10, 20 | 2, 4, 1 |

| Purchase Date | Customer ID | Customer Name | Product Name | Unit Price | Quantity (kg) |
| --- | --- | --- | --- | --- | --- |
| 12/24 | p002 | Howard | Apple | 30 | 2 |
| 12/24 | p002 | Howard | Banana | 10 | 4 |
| 12/24 | p002 | Howard | Orange | 20 | 1 |

---
slug: er-database

The table below is the result of my first normalization pass:

| ID | Purchase Date | Customer ID | Customer Name | Product Name | Unit Price | Quantity (kg) |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 12/24 | p001 | Ken | Banana | 10 | 5 |
| 2 | 12/24 | p002 | Howard | Apple | 30 | 2 |
| 3 | 12/24 | p002 | Howard | Banana | 10 | 4 |
| 4 | 12/24 | p002 | Howard | Orange | 20 | 1 |
| 5 | 12/25 | p003 | Chris | Apple | 30 | 2 |
| 6 | 12/25 | p003 | Chris | Apple | 30 | 2 |
| 7 | 12/25 | p004 | May | Apple | 30 | 1 |
| 8 | 12/25 | p004 | May | Orange | 20 | 1 |

This loses the authenticity of the original data — you can no longer tell that rows 002–004 were actually part of the same order. The same applies to other multi-item orders. So let's restructure it like this:

---
slug: er-database

### Orders

| ID | Order Number | Purchase Date | Customer ID | Customer Name | Product Name | Unit Price | Quantity (kg) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | d001 | 12/24 | p001 | Ken | Banana | 10 | 5 |
| 2 | d002 | 12/24 | p002 | Howard | Apple | 30 | 2 |
| 3 | d002 | 12/24 | p002 | Howard | Banana | 10 | 4 |
| 4 | d002 | 12/24 | p002 | Howard | Orange | 20 | 1 |
| 5 | d003 | 12/25 | p003 | Chris | Apple | 30 | 2 |
| 6 | d004 | 12/25 | p003 | Chris | Apple | 30 | 2 |
| 7 | d005 | 12/25 | p004 | May | Apple | 30 | 1 |
| 8 | d005 | 12/25 | p004 | May | Orange | 20 | 1 |

The data seems to have grown even more!

---
slug: er-database

## 2NF

Eliminate partial dependencies

- Extract product name and unit price into a separate table

---
slug: er-database

### Orders

| ID | Order Number | Purchase Date | Customer ID | Customer Name | Product Name | Quantity (kg) |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | d001 | 12/24 | p001 | Ken | Banana | 5 |
| 2 | d002 | 12/24 | p002 | Howard | Apple | 2 |
| 3 | d002 | 12/24 | p002 | Howard | Banana | 4 |
| 4 | d002 | 12/24 | p002 | Howard | Orange | 1 |
| 5 | d003 | 12/25 | p003 | Chris | Apple | 2 |
| 6 | d004 | 12/25 | p003 | Chris | Apple | 2 |
| 7 | d005 | 12/25 | p004 | May | Apple | 1 |
| 8 | d005 | 12/25 | p004 | May | Orange | 1 |

### Product Info

| Product Name | Unit Price |
| --- | --- |
| Banana | 10 |
| Apple | 30 |
| Orange | 20 |

---
slug: er-database

## 3NF

Eliminate transitive dependencies

- What is a transitive dependency? X->Y, Y->Z therefore X->Z
- Extract customer ID and customer name into a separate table

---
slug: er-database

### Orders

| ID | Order Number | Purchase Date | Customer ID | Product Name | Quantity (kg) |
| --- | --- | --- | --- | --- | --- |
| 1 | d001 | 12/24 | p001 | Banana | 5 |
| 2 | d002 | 12/24 | p002 | Apple | 2 |
| 3 | d002 | 12/24 | p002 | Banana | 4 |
| 4 | d002 | 12/24 | p002 | Orange | 1 |
| 5 | d003 | 12/25 | p003 | Apple | 2 |
| 6 | d004 | 12/25 | p003 | Apple | 2 |
| 7 | d005 | 12/25 | p004 | Apple | 1 |
| 8 | d005 | 12/25 | p004 | Orange | 1 |

### Customer Data

| Customer ID | Customer Name |
| --- | --- |
| p001 | Ken |
| p002 | Howard |
| p003 | Chris |
| p004 | May |

### Product Info

| Product Name | Unit Price |
| --- | --- |
| Banana | 10 |
| Apple | 30 |
| Orange | 20 |

---
slug: er-database

### Normalization Practice

![image](https://hackmd.io/_uploads/HJlltsXN6.png)



- Timesheet needs more entries, so to get the Invoice ID you should remove the TimesheetID from Invoice.
- Employee Address1 and Address2 violate First Normal Form.
- Employee ZIP violates normalization rules.
- Addresses in a database must be split into city, street, lane, etc. to comply with normalization rules.
- Vehicle's EmployeeID and VehicleID should form a new table together.
- EmployeeType and Employee should have a 1-to-many relationship.
- Salary does not belong in the Employee table.
- Because Timesheet contains ClientID, Client should have a 1-to-many relationship with Timesheet.

Revised version:
![image](https://hackmd.io/_uploads/HkHbtimV6.png)


