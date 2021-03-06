---
layout: post
title: Title
date: 2020-07-15
category: category
---

# Notes on ACID properties in SQL

A **DB transaction** is a set of logically related queries(statements) which access data by reading and writing into the DB. ACID properties when applied to a trasaction helps keep the data consistent on the DB before and after the transaction.

**Automicity, Consistency, Isolation, Durability**
1. Automicity 	- Atomic transaction. A transaction must take place only once.
A transaction must complete or fail altogether. There is no intermidiate state for a transaction. After a successful transaction, a **commit** saves the data. **Abort** happens when there is a problem in the transaction and all the previous steps must be rolled back to keep the data consistent.
2. Consistency 	- Correctness of data. Data must be consistent before and after the transaction
3. Isolation 	- Each transaction is treated as different, runs indepently from the other transaction
Concurrent transactions do not result in data inconsistency. 
4. Durability 	- The changes of a transaction are applied on the DB irrespective of the system status.

**Locking and multi-versioning.**
Concurrent transactions do not result in data inconsistency.
1. Locking 				- DB locks the record(s). 2 main techniques - WAL and Shadow paging (Postgres uses WAL also for replication)
2. multi-versioning

**Note:**
* Complying to ACID properties in distributed DB environment becomes a challenge.

**Further Reading**
* Postgres is a transactional DB. Each statement is executed with an implicit transaction - [Postgres transactions](https://www.postgresql.org/docs/8.3/tutorial-transactions.html)
* [Postgres ACID compliant](https://people.apache.org/~jim/NewArchitect/webtech/2001/09/jepson/index.html)