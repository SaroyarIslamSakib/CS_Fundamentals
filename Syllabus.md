# DBMS Master Syllabus — Software Engineer / Backend Engineer Job Preparation

> **Version:** 2.0 (audited and restructured edition)
> **Scope:** Database theory + SQL + design + transactions + internals + operations + distributed systems + backend engineering + interview practice.

---

## Purpose

This is a **single master syllabus** for DBMS preparation for Software Engineer (SDE), Backend Engineer, and Full-Stack roles. It is organized to be studied **in order**, from "what is a database" to "how would you design and scale the database for a payment system".

It is built on three principles:

1. **Theory first, vendor second.** Concepts are taught independent of any product. Section 45 then maps them to PostgreSQL, SQL Server and MySQL.
2. **Three levels of mastery for every important topic:** *Definition* → *Internal mechanism* → *Practical engineering* (see §53).
3. **Coverage without bloat.** Specialized topics are tagged 🟢 Advanced or *Optional* instead of being forced into the core.

## Target Audience

- Fresh graduates and early-career engineers preparing for SDE interviews.
- Backend / full-stack engineers (especially .NET, Java, Node, Python) who want database depth.
- Engineers moving toward senior roles who need internals, scaling and distributed-database knowledge.

## How to Use This Syllabus

- Follow the **Parts** in order. Do not skip Part III (SQL) or Part V (Transactions) — they dominate interviews.
- Each major section has a **Priority** and **Level** tag, a topic list, and (for key topics) a **"What You Should Be Able to Do"** block. Treat that block as the exit criteria.
- Section 47 (SQL patterns), 48 (paper problems) and 46 (design) are the *practice* sections. Start sampling them as soon as the related theory is done; do not leave them for the end.
- Use §52 (Mastery Checklist) for tracking and §53 for a phased study plan.

## Priority Legend

| Icon | Meaning | Rule of thumb |
|---|---|---|
| 🔴 **Critical** | Must know for most Software Engineer interviews | Asked in most DB-related rounds |
| 🟠 **High** | Strongly recommended | Asked in mid/senior or backend-focused rounds |
| 🟡 **Medium** | Useful for deeper interviews | Asked when you claim DB depth |
| 🟢 **Advanced** | Specialized / senior-level | Differentiator for senior/DB-heavy roles |

## Level Legend

`Core` (everyone) · `Intermediate` (most engineers with 1–3 yrs) · `Advanced` (senior/specialist) · `Optional` (role-specific awareness)

---

# Table of Contents

**Part I — Foundations**
1. Database Fundamentals 🔴
2. DBMS Architecture 🟠
3. Data Models and the Database Landscape 🟠

**Part II — Relational Model and Data Modeling**
4. The Relational Model 🔴
5. Keys and Integrity Constraints 🔴
6. ER and EER Modeling 🔴
7. Relational Algebra and Calculus 🟠

**Part III — SQL**
8. SQL Foundations: Language, Data Types, DDL, DML 🔴
9. Querying: SELECT, Filtering, NULL, Expressions, Functions 🔴
10. Joins 🔴
11. Aggregation and Grouping 🔴
12. Subqueries, CTEs, and Set Operations 🔴
13. Window Functions 🔴
14. Database Objects and Programmability 🟠
15. Modern SQL Features (JSON, Full-Text, Pagination, Temporal, Geospatial) 🟠

**Part IV — Database Design Theory and Practice**
16. Functional Dependencies 🔴
17. Normalization and Decomposition 🔴
18. Practical Schema Design Patterns 🟠

**Part V — Transactions and Concurrency**
19. Transactions and ACID 🔴
20. Schedules, Serializability, Recoverability 🟠
21. Lock-Based Concurrency Control 🔴
22. Isolation Levels and Anomalies 🔴
23. Deadlocks 🔴
24. Timestamp Ordering, Optimistic Control, MVCC, Snapshot Isolation 🟠
25. Recovery and Logging 🟠

**Part VI — Storage, Indexing, and the Query Engine**
26. Storage Internals 🟠
27. Indexing 🔴
28. B-Trees and B+ Trees 🔴
29. Hashing and Other Index Structures 🟠
30. Query Processing and Join Algorithms 🟠
31. Query Optimization 🔴
32. Execution Plans 🔴
33. Performance Engineering and Observability 🔴

**Part VII — Database Operations**
34. Database Security 🔴
35. Backup, Restore, and Disaster Recovery 🟠
36. Replication and High Availability 🟠
37. Partitioning and Sharding 🟠

**Part VIII — Distributed and Alternative Data Systems**
38. Distributed Databases 🟠
39. NoSQL Databases 🟠
40. NewSQL and Specialized Data Stores 🟡
41. OLTP, OLAP, and Data Warehousing 🟠

**Part IX — Backend Engineering with Databases**
42. Application Integration: Connections, Pooling, Transactions 🔴
43. ORM and EF Core Concepts 🟠
44. Data Evolution and Integration Patterns (Migrations, CDC, Outbox, CQRS) 🟠
45. PostgreSQL, SQL Server, and MySQL Practical Knowledge 🟠

**Part X — Practice and Interview Preparation**
46. Database Design Method and Case Studies 🔴
47. SQL Interview Pattern Catalog 🔴
48. Numerical and Paper Problem Catalog 🟠
49. Interview Question Bank 🔴
50. Comparison Cheat Sheet 🔴

**Part XI — Planning and Tracking**
51. Priority Tiers 
52. Final Mastery Checklist
53. Recommended Learning Sequence

**Appendices**
- A. Audit Report (gap analysis of the original syllabus)
- B. Summary of Changes

---

# PART I — FOUNDATIONS

---

# 1. Database Fundamentals 🔴

> **Level:** Core

## 1.1 Core Concepts
- Data vs information vs knowledge
- Database, database system, DBMS, RDBMS
- Database server vs database client; embedded (SQLite) vs server databases
- Structured, semi-structured (JSON/XML), unstructured data
- Schema (intension) vs instance/state (extension)
- Metadata and the catalog (system tables, `information_schema`)

## 1.2 Why a DBMS? (File System vs DBMS)
- Problems of file-based storage: redundancy, inconsistency, difficult access, data isolation, integrity, atomicity, concurrent access, security
- Characteristics of the database approach: self-describing, program–data independence, multiple views, data sharing, multiuser transactions
- Advantages and disadvantages/costs of a DBMS (complexity, cost, overhead, single point of failure)
- When *not* to use a full DBMS (small config, immutable logs, simple caches)

## 1.3 DBMS Responsibilities
- Storage, retrieval, modification, definition
- Query processing and optimization
- Integrity enforcement, security and authorization
- Transaction management, concurrency control, recovery
- Backup and metadata management

## 1.4 Database Users and Roles
- DBA (duties: schema, security, tuning, backup, monitoring), database designer, application developer
- End users: naive, casual, sophisticated, specialized
- Data analyst, data engineer, database engineer / SRE
- Cloud era: managed DBaaS (RDS, Cloud SQL, Azure SQL) and what the provider handles vs what you still own

## 1.5 Language Families (preview)
- DDL, DML, DCL, TCL, and query language (detail in §8)

### What You Should Be Able to Do
- Explain DBMS vs RDBMS vs file system with concrete failure examples.
- List what a DBMS does behind a single `UPDATE` (parse, authorize, optimize, lock, log, write, commit).
- Describe a DBA's responsibilities and what a backend engineer is expected to own.

---

# 2. DBMS Architecture 🟠

> **Level:** Core → Intermediate

## 2.1 Three-Schema Architecture
```text
External Level (views, per user/application)
        ↕  external/conceptual mapping
Conceptual Level (logical schema of the whole DB)
        ↕  conceptual/internal mapping
Internal Level (physical storage, files, indexes)
```
- External, conceptual, internal schemas and the mappings between them

## 2.2 Data Independence
- Logical data independence (change conceptual schema without changing external schemas/apps)
- Physical data independence (change storage/indexes without changing the logical schema)
- Practical examples: adding an index, adding a column, replacing a table with a view

## 2.3 DBMS Component Architecture
- **Query processor:** DDL interpreter, DML compiler/parser, query rewriter, optimizer, execution engine
- **Storage manager:** file manager, buffer manager, authorization & integrity manager, transaction manager, recovery manager, lock manager
- **Catalog/data dictionary:** tables, columns, indexes, constraints, statistics, permissions
- Disk structures: data files, index files, log files (WAL), control files, temp files

## 2.4 Server Process Models
- Process-per-connection (PostgreSQL), thread-per-connection (MySQL), scheduler/worker model (SQL Server)
- Why connection count matters (memory per connection, context switching) → motivates pooling (§42)

## 2.5 Deployment Architectures
- Single-node, client-server, embedded
- Shared-nothing vs shared-disk vs shared-memory (awareness)
- Managed cloud databases; serverless databases (awareness)
- Where primary, replicas, caches, and warehouses sit in a typical backend system

### What You Should Be Able to Do
- Draw the path of a query through parser → optimizer → executor → buffer manager → disk.
- Give a real example of logical vs physical data independence.
- Explain why opening a new DB connection per request is expensive.

---

# 3. Data Models and the Database Landscape 🟠

> **Level:** Core (awareness) → Intermediate

## 3.1 Levels of Data Modeling
- Conceptual (ER) → Logical (relational) → Physical (types, indexes, partitions)
- Data model vs schema vs instance

## 3.2 Data Models
- Hierarchical, network (historical context)
- **Relational** (dominant)
- Object-oriented and object-relational
- Key-value, document, wide-column, graph (detail in §39)
- Time-series, search, vector (awareness; §40)

## 3.3 Choosing a Model
- Match the model to access patterns, consistency needs, scale, and team skill
- Polyglot persistence: using more than one store in a system and the cost of doing so
- "Default to a relational database unless you can state the specific reason not to"

### What You Should Be Able to Do
- Justify a model choice for: banking ledger, product catalog, social graph, session store, analytics events.

---

# PART II — RELATIONAL MODEL AND DATA MODELING

---

# 4. The Relational Model 🔴

> **Level:** Core

## 4.1 Terminology
- Relation, tuple, attribute, domain, relation schema, relation instance
- Degree (number of attributes) vs cardinality (number of tuples)
- Formal terms ↔ SQL terms (relation ↔ table, tuple ↔ row, attribute ↔ column)

## 4.2 Properties of Relations
- Atomic (indivisible) values — first normal form precondition
- No duplicate tuples in the pure model (SQL tables are *bags* unless constrained)
- Tuple order and attribute order are irrelevant (SQL `ORDER BY` is a presentation concern)

## 4.3 NULL
- Meanings: unknown, inapplicable, missing
- NULL ≠ 0 ≠ empty string
- Three-valued logic (TRUE / FALSE / UNKNOWN) and truth tables for `AND`, `OR`, `NOT`
- `IS NULL` / `IS NOT NULL`; `IS DISTINCT FROM` (where supported)
- NULL in comparisons, `NOT IN` (classic trap), aggregates, `UNIQUE`, `ORDER BY`, and joins
- Design guidance: when to forbid NULL; alternatives (separate table, default value)

### What You Should Be Able to Do
- Predict the result of `WHERE x = NULL`, `x NOT IN (1, NULL)`, `COUNT(col)` vs `COUNT(*)`.
- Explain why a relation is a set but a SQL result may be a bag.

---

# 5. Keys and Integrity Constraints 🔴

> **Level:** Core (this section is the single home for constraints; SQL syntax for them is in §8)

## 5.1 Keys
- Super key, candidate key, primary key, alternate key
- Composite key, simple key
- Foreign key (and self-referencing foreign key)
- Natural key vs surrogate key (trade-offs: stability, size, meaning, joins, merging data)
- Surrogate key generation: auto-increment / identity, sequences, UUIDs (v4 vs time-ordered v7/ULID, index locality impact), snowflake-style IDs (awareness)
- Business key vs technical key

## 5.2 Integrity Constraints
- **Domain** constraints (type, range, `CHECK`)
- **Entity integrity** (PK not null, unique)
- **Referential integrity** (FK must match an existing key or be NULL)
- **Key** constraints (`UNIQUE`)
- **Business rules** (check constraints, triggers, application logic — and where each belongs)
- Semantic/assertion constraints (`CREATE ASSERTION` is rarely implemented; emulate with triggers/constraints)

## 5.3 Constraint Mechanics in SQL
- `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`, `DEFAULT`
- Named constraints and why naming matters for migrations
- Immediate vs deferred constraint checking (`DEFERRABLE INITIALLY DEFERRED`; where supported)
- `UNIQUE` and NULL behavior differences across vendors
- Composite unique constraints; partial unique constraints (e.g., unique among non-deleted rows)

## 5.4 Referential Actions
- `ON DELETE` / `ON UPDATE`: `CASCADE`, `SET NULL`, `SET DEFAULT`, `RESTRICT`, `NO ACTION`
- When cascade is dangerous (accidental mass delete; audit requirements)
- Indexing foreign key columns (join performance, delete/lock behavior)

## 5.5 Constraints as a Concurrency and Correctness Tool
- Unique constraints are the only fully reliable defense against duplicate inserts under concurrency
- Idempotency keys implemented via unique constraints (see §42, §44)

### What You Should Be Able to Do
- Given a relation and FDs, list super keys and candidate keys (links to §16).
- Write DDL with all six constraint types and explain each failure message.
- Argue for/against a surrogate key in a given scenario, and choose a UUID strategy with index impact in mind.

---

# 6. ER and EER Modeling 🔴

> **Level:** Core (ER) · Intermediate (EER)

## 6.1 ER Concepts
- Entity, entity set, entity type; attribute; relationship, relationship set
- Attribute types: simple, composite, single-valued, multi-valued, derived/stored, key
- Relationship degree: unary (recursive), binary, ternary (when a ternary cannot be decomposed into binaries)
- Relationship attributes

## 6.2 Constraints on Relationships
- **Cardinality ratios:** 1:1, 1:N, N:1, M:N
- **Participation:** total vs partial
- Structural constraints `(min, max)` notation
- Notations: Chen, crow's foot (practical), UML class diagrams (awareness)

## 6.3 Weak Entities
- Weak entity, owner entity, identifying relationship, partial key (discriminator)

## 6.4 EER Concepts
- Specialization and generalization; superclass/subclass; inheritance
- Constraints: **disjoint vs overlapping**, **total vs partial** (completeness)
- Category / union type
- **Aggregation** (treating a relationship as an entity to relate to other entities)

## 6.5 ER-to-Relational Mapping
- Strong entities, weak entities
- Attributes: composite (flatten), multi-valued (new table), derived (compute)
- 1:1 (merge or FK on total-participation side), 1:N (FK on the N side), M:N (junction table with composite PK and relationship attributes)
- N-ary relationships
- Specialization mapping options: single table (with type discriminator), table per subclass (joined), table per concrete class — trade-offs (links to ORM inheritance mapping, §43)

## 6.6 Common Modeling Pitfalls
- Fan traps and chasm traps
- Modeling a many-to-many as two one-to-many incorrectly
- Storing lists in a single column
- Missing junction-table attributes (e.g., `quantity` in order items)

### What You Should Be Able to Do
- Convert a requirement paragraph into an ER diagram, then into relational tables with keys.
- Choose the right mapping for a 1:1 relationship and for an inheritance hierarchy.
- Spot fan/chasm traps in a given diagram.

---

# 7. Relational Algebra and Calculus 🟠

> **Level:** Intermediate (algebra is 🟠; calculus is 🟡)

## 7.1 Relational Algebra
- **Basic operators:** selection σ, projection π, union ∪, set difference −, Cartesian product ×, rename ρ
- **Derived operators:** intersection, theta join, equijoin, natural join, semi-join, anti-join, outer joins (left/right/full)
- **Division ÷** (for "for all" queries — e.g., students who took *all* required courses)
- Extended operators: aggregation/grouping γ, generalized projection, sorting τ
- Union compatibility
- Algebra expression trees (links to optimization, §31) and equivalence rules (selection cascade, commutativity of join, pushing selection through join)

## 7.2 Relational Calculus 🟡
- Tuple relational calculus (TRC): `{ t | P(t) }`, free and bound variables, ∃ and ∀
- Domain relational calculus (DRC)
- Safe expressions
- Expressive power: relational algebra ≡ safe TRC ≡ safe DRC (Codd's theorem)

## 7.3 Mapping Algebra ↔ SQL
- σ → `WHERE`, π → `SELECT`, ⋈ → `JOIN`, ÷ → double `NOT EXISTS` or grouping with `HAVING COUNT`
- Why SQL is bag semantics while algebra is set semantics

### What You Should Be Able to Do
- Translate English queries into algebra, and algebra into SQL.
- Express "students who enrolled in **all** courses offered by CS" using division, and in SQL.
- Write the same query in TRC and algebra (calculus-level only for university-style exams).


---

# PART III — SQL

> Recommended approach: practice every section on a real engine (PostgreSQL preferred; also try SQL Server or MySQL for differences) using a small sample schema: `employees`, `departments`, `customers`, `orders`, `order_items`, `products`, `logins`.

---

# 8. SQL Foundations: Language, Data Types, DDL, DML 🔴

> **Level:** Core

## 8.1 SQL Language Categories
- **DDL:** `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`
- **DML:** `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE` / upsert
- **DCL:** `GRANT`, `REVOKE`
- **TCL:** `BEGIN/START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, `ROLLBACK TO SAVEPOINT`
- SQL standard vs vendor dialects (T-SQL, PL/pgSQL, MySQL dialect)
- Syntax basics: keywords, identifiers, quoting, literals, operators, aliases, comments, case sensitivity, statement terminators

## 8.2 Data Types
- Numeric: `SMALLINT/INT/BIGINT`, `DECIMAL/NUMERIC(p,s)`, `FLOAT/REAL` (**never use floating point for money**)
- Character: `CHAR`, `VARCHAR`, `TEXT`; collation and case sensitivity; Unicode (`NVARCHAR` in SQL Server)
- Date/time: `DATE`, `TIME`, `TIMESTAMP` (with/without time zone), `INTERVAL`; store UTC, convert at the edge
- Boolean, binary/blob, enum (trade-offs vs lookup table)
- UUID, JSON/JSONB, arrays, XML (where supported)
- Type conversion: implicit vs explicit `CAST/CONVERT`; implicit conversion as a performance trap (§31 sargability)
- Choosing types: size affects index size and cache efficiency

## 8.3 DDL
- Create database/schema/table; `CREATE TABLE ... AS`
- `ALTER TABLE`: add/drop/modify column, add/drop constraint, rename
- `DROP` vs `TRUNCATE` vs `DELETE` (logging, rollback ability, triggers, identity reset, locks, speed)
- Defaults, generated/computed columns, identity/auto-increment/sequence
- Online vs blocking DDL (why `ALTER TABLE` on a big table can take an outage; links to §44 migrations)
- Constraint syntax is in §5.3

## 8.4 DML
- `INSERT`: single row, multi-row, `INSERT ... SELECT`, default values
- `UPDATE`: with expressions, with joins/`FROM` (vendor syntax differs)
- `DELETE`: with predicates, with joins/subqueries
- **Upsert/MERGE:** `INSERT ... ON CONFLICT` (PG), `ON DUPLICATE KEY UPDATE` (MySQL), `MERGE` (SQL Server/standard) — behavior, concurrency caveats (`MERGE` has known pitfalls in SQL Server)
- `RETURNING` / `OUTPUT` clauses to avoid a second round trip
- Bulk operations: bulk insert / `COPY` / batching; why row-by-row loops are slow
- Safe modification practice: `SELECT` first, wrap in a transaction, check affected row count

## 8.5 TCL in Practice
- Autocommit behavior; explicit transactions
- Savepoints for partial rollback
- DDL transactionality differs (PG: transactional DDL; MySQL: implicit commit)

### What You Should Be Able to Do
- Create a full schema (tables, PK/FK, unique, check, default, indexes) from an ER diagram.
- Explain exactly how `DELETE`, `TRUNCATE`, `DROP` differ on logging, rollback and locks.
- Write an idempotent upsert and explain its behavior under concurrent inserts.

---

# 9. Querying: SELECT, Filtering, NULL, Expressions, Functions 🔴

> **Level:** Core

## 9.1 SELECT Fundamentals
- `SELECT`, `FROM`, `WHERE`, `DISTINCT`, `ORDER BY`, aliases
- Row limiting: `LIMIT/OFFSET`, `TOP`, `FETCH FIRST n ROWS ONLY` (deterministic ordering requires tie-breaker)
- Avoid `SELECT *` in production code and why (I/O, covering indexes, schema drift)

## 9.2 Logical Query Processing Order
```text
FROM / JOIN → WHERE → GROUP BY → HAVING → SELECT (window functions evaluated here)
            → DISTINCT → ORDER BY → LIMIT/OFFSET
```
- Why a `SELECT` alias cannot be used in `WHERE` (but can in `ORDER BY`)
- Why window functions cannot appear in `WHERE` (use a subquery/CTE)

## 9.3 Filtering
- `AND/OR/NOT` precedence, `BETWEEN` (inclusive; dangerous with timestamps), `IN`, `NOT IN` (NULL trap), `LIKE`, `IS NULL`
- Pattern matching: `%`, `_`, escape characters, case-insensitive matching (`ILIKE`, collation), regex (awareness)
- Date-range filtering best practice: `>= start AND < next_day` (half-open interval)

## 9.4 Expressions and Conditional Logic
- `CASE` (simple and searched); `IIF`/`IF` dialects
- `COALESCE`, `NULLIF`, vendor NULL functions (`ISNULL`, `IFNULL`, `NVL`)
- Safe division with `NULLIF`

## 9.5 Scalar Functions
- String: `LOWER/UPPER`, `LENGTH/LEN`, `SUBSTRING`, `TRIM`, `CONCAT/||`, `REPLACE`, `POSITION/CHARINDEX`, `LEFT/RIGHT`, regex functions
- Numeric: `ROUND`, `CEILING`, `FLOOR`, `ABS`, `MOD/%`, `POWER`, integer-division pitfalls
- Date/time: current date/time, date arithmetic, `EXTRACT/DATEPART`, `DATEDIFF`, truncation (`DATE_TRUNC`), formatting, time zones, generating date series
- Conversion: `CAST`, `CONVERT`, `TO_CHAR` and friends

### What You Should Be Able to Do
- Write correct filters over dates, strings and NULLs without off-by-one or three-valued-logic bugs.
- Explain the logical processing order and use it to explain "why does this alias not work in WHERE".
- Page through a result deterministically.

---

# 10. Joins 🔴

> **Level:** Core — *one of the highest-yield SQL topics*

## 10.1 Join Types
- `INNER`, `LEFT [OUTER]`, `RIGHT [OUTER]`, `FULL [OUTER]`, `CROSS`
- `SELF` join, `NATURAL` join (and why it is discouraged), equijoin, theta (non-equi) join
- Semi-join (`EXISTS`) and anti-join (`NOT EXISTS` / `LEFT JOIN ... IS NULL`)
- `LATERAL` / `CROSS APPLY` / `OUTER APPLY` (🟡: top-N per row, correlated table functions)
- `USING` vs `ON`

## 10.2 Join Semantics That Interviewers Probe
- `ON` vs `WHERE` placement in outer joins (filtering right-table columns in `WHERE` silently turns a `LEFT JOIN` into an `INNER JOIN`)
- Join cardinality: one-to-many multiplies rows; **fan-out** breaks `SUM`/`COUNT` (aggregate before joining or use `COUNT(DISTINCT)`)
- NULL join keys never match
- Many-to-many via junction tables; multi-table joins; join order is logical, not physical (the optimizer reorders)

## 10.3 Practice Patterns
- Unmatched rows (customers with no orders; products never ordered)
- Employee–manager self-join; employees earning more than their manager
- Pairs/duplicates in self joins (`a.id < b.id`)
- Hierarchies via self join (fixed depth) vs recursive CTE (variable depth)

### What You Should Be Able to Do
- Predict row counts of any join given the cardinalities.
- Convert between `LEFT JOIN ... IS NULL`, `NOT EXISTS`, and `NOT IN`, and state their NULL-behavior differences.
- Debug a "my totals doubled" report caused by join fan-out.

---

# 11. Aggregation and Grouping 🔴

> **Level:** Core → Intermediate

## 11.1 Aggregates
- `COUNT(*)`, `COUNT(col)`, `COUNT(DISTINCT col)`, `SUM`, `AVG`, `MIN`, `MAX`
- NULL handling in aggregates; `AVG` over NULLs; empty-set results
- String/array aggregation (`STRING_AGG`, `GROUP_CONCAT`)
- Statistical aggregates, percentiles (`PERCENTILE_CONT`) — 🟡

## 11.2 Grouping
- `GROUP BY` with single/multiple columns; rule: every non-aggregated select column must be grouped
- `HAVING` vs `WHERE` (row filter vs group filter; aggregate placement)
- `DISTINCT` vs `GROUP BY`

## 11.3 Conditional Aggregation (high-yield)
- `SUM(CASE WHEN ... THEN 1 ELSE 0 END)`, `COUNT(*) FILTER (WHERE ...)` (PG)
- Pivot using conditional aggregation; unpivot using `UNION ALL` / `CROSS APPLY` / `UNPIVOT`

## 11.4 Advanced Grouping 🟡
- `ROLLUP`, `CUBE`, `GROUPING SETS`, `GROUPING()` function

### What You Should Be Able to Do
- Compute per-group metrics (counts, ratios, conditional counts) in a single scan.
- Pivot rows to columns without vendor-specific `PIVOT`.
- Choose between `HAVING` and a pre-filter in `WHERE` for performance.

---

# 12. Subqueries, CTEs, and Set Operations 🔴

> **Level:** Core → Intermediate

## 12.1 Subqueries
- Scalar, row, table (derived table), multi-row subqueries
- Subqueries in `SELECT`, `FROM`, `WHERE`, `HAVING`
- **Correlated** subqueries and their execution model (conceptually once per outer row; optimizers often decorrelate)
- `IN` / `NOT IN`, `EXISTS` / `NOT EXISTS`, `ANY/SOME`, `ALL`
- `NOT IN` + NULL trap; `EXISTS` for semi-joins; `ALL` for "greater than every"
- Subquery vs join: when each is clearer/faster

## 12.2 CTEs
- Non-recursive and multiple CTEs; readability benefits
- CTE vs subquery vs view vs temp table (materialization, optimization-fence behavior differs by engine/version: PG ≥12 inlines by default, `MATERIALIZED` hint available)
- **Recursive CTE:** anchor + recursive member, termination, cycle prevention; use cases (org charts, bill of materials, category trees, graph traversal, number/date series)

## 12.3 Set Operations
- `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT` / `MINUS`
- Duplicate handling; column count/type compatibility; ordering of results
- Performance: `UNION ALL` avoids the sort/dedup cost
- Emulating `INTERSECT/EXCEPT` where unsupported (older MySQL)

### What You Should Be Able to Do
- Rewrite a correlated subquery as a join or window function, and vice versa.
- Write a recursive CTE listing all reports under a manager with their depth.
- Explain precisely why `NOT IN` can return zero rows when the subquery contains NULL.

---

# 13. Window Functions 🔴

> **Level:** Intermediate — *extremely high interview frequency*

## 13.1 Syntax and Concepts
- `func() OVER (PARTITION BY ... ORDER BY ... frame)`
- Window vs `GROUP BY`: windows keep individual rows
- Named windows (`WINDOW w AS (...)`)

## 13.2 Function Families
- **Ranking:** `ROW_NUMBER`, `RANK`, `DENSE_RANK`, `NTILE`, `PERCENT_RANK`, `CUME_DIST`
- **Value/offset:** `LAG`, `LEAD`, `FIRST_VALUE`, `LAST_VALUE`, `NTH_VALUE`
- **Aggregate windows:** running `SUM`, moving `AVG`, partitioned `COUNT`/`MAX`

## 13.3 Frames
- `ROWS` vs `RANGE` vs `GROUPS` (🟡)
- Frame boundaries: `UNBOUNDED PRECEDING`, `n PRECEDING`, `CURRENT ROW`, `n FOLLOWING`
- **Default frame trap:** with `ORDER BY`, default is `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` → ties get the same running value and `LAST_VALUE` surprises

## 13.4 Core Patterns
- Top-N per group; Nth highest per department
- Running total, cumulative percent, moving average
- Row-to-previous-row comparison (`LAG`) — growth, deltas, session gaps
- Deduplication with `ROW_NUMBER()`
- Gaps-and-islands with `ROW_NUMBER` difference
- Percentile / quartile bucketing (`NTILE`)

### What You Should Be Able to Do
- Choose correctly between `ROW_NUMBER`, `RANK`, `DENSE_RANK` for a tie scenario.
- Compute a 7-day moving average and a running total per customer.
- Filter on a window result via CTE/subquery (and `QUALIFY` where available).

---

# 14. Database Objects and Programmability 🟠

> **Level:** Intermediate

## 14.1 Views
- Create/query views; updatable views and their restrictions; `WITH CHECK OPTION`
- Security via views (column/row hiding); abstraction layer for schema changes
- Performance: views are usually macro-expanded, not stored

## 14.2 Materialized Views
- Stored results; refresh (complete vs incremental), on-demand vs scheduled; staleness trade-offs
- Vendor differences: PG materialized views (manual refresh, `CONCURRENTLY`), SQL Server indexed views, MySQL (emulated)

## 14.3 Stored Procedures and Functions
- Parameters (in/out), return values, scalar vs table-valued functions
- Procedure vs function (side effects, usage in queries, transactions)
- Advantages (round trips, security, plan caching) and disadvantages (versioning, testing, vendor lock-in, logic split across tiers)
- Dynamic SQL and injection risk; error handling (`TRY/CATCH`, `EXCEPTION`)

## 14.4 Triggers
- `BEFORE`/`AFTER`/`INSTEAD OF`; row-level vs statement-level; `INSERT/UPDATE/DELETE`; `OLD`/`NEW` (`inserted`/`deleted` in SQL Server)
- Use cases: audit trails, derived data, enforcing complex rules
- Risks: hidden side effects, debugging, performance, cascading/recursive triggers, bulk operation behavior
- Trigger vs application logic vs constraint — decision rule: *prefer declarative constraints → application logic → triggers for audit/guaranteed invariants*

## 14.5 Sequences, Identity, and Generated Values
- Identity/auto-increment vs sequences; gaps are normal (rollback, cache); not for gapless numbering
- Hot-spot and ordering implications of sequential vs random keys
- Computed/generated columns (stored vs virtual)

## 14.6 Temporary Structures
- Temporary tables, table variables (SQL Server), CTEs, derived tables — scope, statistics, indexing, logging, and when each is appropriate

## 14.7 Cursors 🟡
- Server-side cursors; why set-based thinking beats row-by-row (RBAR); legitimate uses (streaming large results)

### What You Should Be Able to Do
- Decide between view, materialized view, CTE, temp table for a reporting query.
- Write an audit trigger and explain its failure modes.
- Explain why sequences can have gaps and why that's acceptable.

---

# 15. Modern SQL Features 🟠

> **Level:** Intermediate → Advanced (selected features Optional)

## 15.1 Pagination 🔴
- `OFFSET/LIMIT`: cost grows with offset (database still reads and discards rows); unstable under inserts
- **Keyset (seek/cursor) pagination:** `WHERE (created_at, id) < (:last_created_at, :last_id) ORDER BY created_at DESC, id DESC LIMIT n` — requires a matching composite index and a unique tie-breaker
- Trade-offs: no random page jumps; opaque cursor tokens; total counts are expensive (`COUNT(*)` on large tables)

## 15.2 JSON and Semi-Structured Data
- JSON vs JSONB (PG), JSON functions in SQL Server/MySQL, JSON path queries
- Indexing JSON (GIN, generated columns, functional indexes)
- When JSON columns are fine (sparse, rarely-queried attributes) and when they signal a missing relational design

## 15.3 Full-Text Search
- Inverted index concept; tokenization, stemming, stop words; ranking (TF-IDF/BM25 awareness)
- `tsvector/tsquery` (PG), `FULLTEXT` (MySQL), Full-Text Search (SQL Server)
- When to move to a dedicated engine (Elasticsearch/OpenSearch) — 🟡

## 15.4 Temporal Data
- Valid time vs transaction time; temporal (system-versioned) tables (SQL Server, MariaDB; PG via extensions/patterns)
- `valid_from/valid_to` slowly-changing history; audit tables; point-in-time queries
- Soft delete (`deleted_at`/`is_deleted`) — pros/cons: unique constraints, query filters, index design (partial indexes), GDPR deletion conflicts

## 15.5 Geospatial and Specialized Types 🟢 Optional
- Basic awareness: spatial types, R-tree/GiST indexes, PostGIS, "find nearby" queries
- Range types, array types, enum types (vendor-specific)

## 15.6 Row-Level Features
- Row-level security (RLS) policies — see §34
- Optimistic concurrency columns (`rowversion`/`xmin`/version int) — see §24, §42

### What You Should Be Able to Do
- Implement keyset pagination for a feed and design its index.
- Decide when JSON, EAV, or normalized columns are appropriate.
- Model soft delete without breaking uniqueness.

---

# PART IV — DATABASE DESIGN THEORY AND PRACTICE

---

# 16. Functional Dependencies 🔴

> **Level:** Core → Intermediate (paper-problem heavy)

## 16.1 Functional Dependency Concepts
- `X → Y`: X determines Y; FDs are semantic constraints on *all* valid instances (not inferred from one instance)
- Types: trivial, non-trivial, completely non-trivial, full, partial, transitive
- Determinant, dependent

## 16.2 Reasoning About FDs
- **Armstrong's axioms:** reflexivity, augmentation, transitivity (sound and complete)
- Derived rules: union, decomposition, pseudotransitivity
- **Closure of FD set F⁺** and **attribute closure X⁺** (algorithm)
- Checking whether an FD is implied by F
- **Equivalence** of two FD sets
- **Canonical / minimal cover:** remove extraneous attributes (left side), remove redundant FDs, single-attribute right sides

## 16.3 Keys from FDs
- Super keys via closure; candidate-key derivation (prime vs non-prime attributes)
- Shortcut: attributes never on any right side must be in every key; attributes only on right sides are in none
- Counting candidate keys

## 16.4 Multivalued and Join Dependencies 🟡
- Multivalued dependency (MVD) `X →→ Y`; trivial MVDs; relationship to FDs
- Join dependency (JD)
- Inference rules for MVDs (awareness)

### What You Should Be Able to Do
- Compute X⁺ and all candidate keys for a relation with 5–7 attributes by hand.
- Find a canonical cover of a given FD set.
- Decide whether two FD sets are equivalent.

---

# 17. Normalization and Decomposition 🔴

> **Level:** Core (1NF–BCNF) → Intermediate (decomposition) → Advanced (4NF/5NF)

## 17.1 Why Normalize
- Redundancy; update, insert, delete anomalies; storage vs consistency trade-off

## 17.2 Normal Forms
- **1NF:** atomic values, no repeating groups (what "atomic" means in practice; JSON/arrays debate)
- **2NF:** 1NF + no partial dependency of a non-prime attribute on part of a candidate key
- **3NF:** 2NF + no transitive dependency; formal condition: for every non-trivial `X → A`, X is a superkey **or** A is prime
- **BCNF:** for every non-trivial `X → Y`, X is a superkey
- **4NF (🟡):** no non-trivial MVD unless the determinant is a superkey
- **5NF / PJNF (🟢):** no join dependency not implied by candidate keys
- 3NF vs BCNF: when BCNF decomposition loses dependency preservation

## 17.3 Decomposition Properties
- **Lossless-join decomposition:** binary test (`R1 ∩ R2 → R1` or `R1 ∩ R2 → R2`); tableau/chase method (🟡)
- **Dependency preservation:** projecting F onto each fragment and checking closure equivalence
- Why 3NF guarantees both properties (synthesis algorithm) while BCNF guarantees only lossless
- Algorithms: BCNF decomposition; 3NF synthesis from canonical cover

## 17.4 Determining the Highest Normal Form
- Procedure: find candidate keys → classify prime/non-prime → check each FD for 2NF, 3NF, BCNF

## 17.5 Denormalization
- Why: read performance, fewer joins, reporting, caching computed values
- Techniques: duplicated columns, precomputed aggregates/counters, summary tables, materialized views, JSON snapshots (e.g., order line price at purchase time — *historical truth, not redundancy*)
- Risks: update anomalies, drift; mitigation via triggers, transactions, async rebuilds
- Normalize for correctness first; denormalize on measured evidence

### What You Should Be Able to Do
- Take an unnormalized table (e.g., an invoice spreadsheet) to 3NF/BCNF with justification at every step.
- Test a decomposition for losslessness and dependency preservation.
- Identify the highest normal form of a relation given its FDs.
- Defend a specific denormalization choice with its consistency strategy.

---

# 18. Practical Schema Design Patterns 🟠

> **Level:** Intermediate (the bridge between theory and real systems)

## 18.1 Relationship Patterns
- One-to-many, many-to-many junction tables with composite PK or surrogate PK
- Self-referencing hierarchies: adjacency list, materialized path, nested sets, closure table — trade-offs, recursive CTE support
- Polymorphic associations (and why they break FK integrity), supertype/subtype tables

## 18.2 Common Structures
- Lookup/reference tables vs enums
- Status/state machines (`status` column + transition table or constraints); append-only status history
- EAV (entity-attribute-value) and why it is usually an anti-pattern; JSON as the modern alternative
- Money, quantities and units; currency and rounding; ledger (double-entry, append-only, no updates)
- Price/quantity snapshots on order lines; address and contact modeling

## 18.3 Operational Columns
- `created_at`, `updated_at`, `created_by`, `version`
- Soft delete; archival tables; audit/history tables; temporal tables
- Natural vs surrogate keys; UUID vs bigint IDs

## 18.4 Multi-Tenancy
- Shared table with `tenant_id` + RLS, schema-per-tenant, database-per-tenant: isolation, cost, migration and noisy-neighbor trade-offs

## 18.5 Common Anti-Patterns
- Comma-separated lists in a column; one giant table; "God" status flags; missing FKs; overuse of NULL; wrong data types (dates as strings, money as float); no indexes on FKs; unbounded `TEXT` everywhere; naming inconsistencies

### What You Should Be Able to Do
- Choose a hierarchy model for a category tree and explain query and update costs.
- Design an auditable ledger table that never updates balances in place.
- Spot and fix five anti-patterns in a given schema.

---

# PART V — TRANSACTIONS AND CONCURRENCY

---

# 19. Transactions and ACID 🔴

> **Level:** Core

## 19.1 Transaction Concept
- Definition, boundaries, `BEGIN` / `COMMIT` / `ROLLBACK` / `SAVEPOINT`
- Autocommit; implicit vs explicit transactions
- Transaction operations: read, write, commit, abort

## 19.2 Transaction States
```text
Active → Partially Committed → Committed
   └──→ Failed → Aborted (rollback, then restart or kill)
```

## 19.3 ACID
- **Atomicity** (undo log / rollback), **Consistency** (application invariants + constraints; the "C" in ACID vs "C" in CAP), **Isolation** (concurrency semantics, §22), **Durability** (WAL + fsync, §25)
- Which DBMS component provides each property (recovery manager, lock/MVCC manager, WAL)
- Worked example: bank transfer (debit A, credit B, with failure at each step)

## 19.4 Practical Transaction Design
- Keep transactions short; no user interaction or remote calls inside a transaction
- Transaction boundaries in a use case; read-modify-write hazards
- Retry on serialization failure and deadlock; idempotent retry logic
- Savepoints and partial rollback; nested transactions (usually emulated)
- Long-running transactions: bloat (MVCC), lock holding, replication lag

### What You Should Be Able to Do
- Explain how each ACID property is enforced mechanically.
- Describe what the DB does on crash between `UPDATE A` and `UPDATE B`.
- Design transaction boundaries for "place order" (stock decrement + order insert + payment record).

---

# 20. Schedules, Serializability, and Recoverability 🟠

> **Level:** Intermediate (paper-problem heavy; most common in university-style and some FAANG-style rounds)

## 20.1 Schedules
- Serial vs concurrent (interleaved) schedules; complete schedules; notation `R1(X) W2(X) C1 ...`
- Number of serial schedules (n!), number of interleavings

## 20.2 Serializability
- **Conflicting operations:** different transactions, same item, at least one write (RW, WR, WW)
- **Conflict equivalence and conflict serializability:** precedence (serialization) graph; cycle ⇒ not conflict-serializable; topological order gives the equivalent serial schedule
- **View equivalence and view serializability:** initial reads, read-from, final writes; blind writes; testing is NP-complete (awareness)
- Relationship: conflict-serializable ⊂ view-serializable ⊂ all schedules

## 20.3 Recoverability
- Recoverable, cascadeless (ACA), strict schedules; cascading rollback
- Hierarchy: strict ⊂ cascadeless ⊂ recoverable
- Relationship between serializability and recoverability (independent properties)

## 20.4 Concurrency Anomalies (preview; full treatment in §22)
- Lost update, dirty read, non-repeatable read, phantom read, incorrect summary, write skew

### What You Should Be Able to Do
- Draw a precedence graph and decide conflict serializability for a 3–4 transaction schedule.
- Classify a schedule as recoverable / cascadeless / strict.
- Produce an equivalent serial order.

---

# 21. Lock-Based Concurrency Control 🔴

> **Level:** Core → Intermediate

## 21.1 Lock Basics
- Shared (S) and exclusive (X) locks; lock compatibility matrix; lock upgrade/downgrade
- Update locks (U) (SQL Server) and why they exist (avoid conversion deadlocks)
- Lock manager: lock table, wait queues, lock timeouts

## 21.2 Two-Phase Locking (2PL)
- Growing and shrinking phases; lock point; guarantees conflict serializability
- Variants: basic, **conservative (static)** 2PL (deadlock-free, but impractical), **strict** 2PL (holds X locks to commit; avoids cascading rollbacks), **rigorous** 2PL (holds all locks to commit)
- 2PL does not prevent deadlock

## 21.3 Lock Granularity
- Database, table, page, row, key/range; trade-off: concurrency vs lock-management overhead
- **Multiple granularity locking:** intention locks IS, IX, SIX; compatibility matrix; lock escalation (SQL Server)
- Predicate locks, key-range/next-key/gap locks (how `REPEATABLE READ`/`SERIALIZABLE` prevent phantoms in InnoDB and SQL Server)

## 21.4 Pessimistic Locking in Practice
- `SELECT ... FOR UPDATE`, `FOR SHARE`, `NOWAIT`, `SKIP LOCKED` (job queues!), `UPDLOCK/HOLDLOCK` hints (SQL Server)
- Table locks, advisory locks (PG `pg_advisory_lock`, MySQL `GET_LOCK`, SQL Server `sp_getapplock`) for cross-process mutual exclusion
- Lock ordering to avoid deadlock; lock timeouts

### What You Should Be Able to Do
- Fill in S/X/IS/IX/SIX compatibility from memory and reason about a table lock vs row lock request.
- Decide whether a given schedule is allowed by strict 2PL.
- Implement a safe "claim next job" query using `FOR UPDATE SKIP LOCKED`.

---

# 22. Isolation Levels and Anomalies 🔴

> **Level:** Core — *near-universal interview question*

## 22.1 Anomalies (definitions and examples)
- **Dirty read** (read uncommitted data of another transaction)
- **Non-repeatable (fuzzy) read** (same row, different value on re-read)
- **Phantom read** (same predicate, different row set)
- **Lost update** (two read-modify-write cycles overwrite one another)
- **Write skew** (two transactions read overlapping data, write disjoint rows, jointly violate an invariant — e.g., on-call doctors)
- **Read skew** / inconsistent snapshot (awareness)

## 22.2 ANSI/ISO Isolation Levels

| Isolation level | Dirty read | Non-repeatable read | Phantom read | Lost update* | Write skew* |
|---|:-:|:-:|:-:|:-:|:-:|
| **Read Uncommitted** | Possible | Possible | Possible | Possible | Possible |
| **Read Committed** | Prevented | Possible | Possible | Possible | Possible |
| **Repeatable Read** (ANSI definition) | Prevented | Prevented | Possible | Engine-dependent | Possible |
| **Serializable** | Prevented | Prevented | Prevented | Prevented | Prevented |

\* The ANSI standard defines levels only through dirty/non-repeatable/phantom reads. Lost update and write skew behavior depends on the implementation (see below). **Learn both the textbook table and the real engine behavior.**

## 22.3 Real Engine Behavior (the part interviews and production incidents care about)
- **PostgreSQL:** Read Uncommitted behaves as Read Committed. `REPEATABLE READ` is **snapshot isolation** (no phantoms in practice; first-updater-wins ⇒ serialization failure instead of lost update; **write skew still possible**). `SERIALIZABLE` uses **SSI** (serializable snapshot isolation) and may abort transactions with serialization failures ⇒ **applications must retry**.
- **MySQL/InnoDB:** default `REPEATABLE READ` using MVCC snapshot for plain reads plus **next-key/gap locks** for locking reads; lost updates still possible with read-then-write unless `SELECT ... FOR UPDATE` or atomic `UPDATE` is used; `SERIALIZABLE` turns plain reads into shared locking reads.
- **SQL Server:** default `READ COMMITTED` using locks (shared locks released after read) **or** row versioning if `READ_COMMITTED_SNAPSHOT` is on (default in Azure SQL Database); separate `SNAPSHOT` isolation (opt-in); `SERIALIZABLE` uses key-range locks.
- **Oracle** (awareness): Read Committed default; no true Repeatable Read; "Serializable" is snapshot isolation.

## 22.4 Practical Anomaly Defenses
- Atomic updates: `UPDATE accounts SET balance = balance - 100 WHERE id = 1 AND balance >= 100` (check affected rows)
- Pessimistic locking: `SELECT ... FOR UPDATE`
- Optimistic concurrency: version column / `rowversion` / `xmin`; `UPDATE ... WHERE id = ? AND version = ?`
- Unique constraints and `INSERT ... ON CONFLICT` for check-then-insert races
- Raising isolation to `SERIALIZABLE` + retry loop
- Materializing conflicts (lock a parent row) for write-skew scenarios

## 22.5 Choosing an Isolation Level
- Throughput vs correctness; analytics replicas vs OLTP; long reads on snapshot
- Per-transaction isolation level setting; defaults per engine

### What You Should Be Able to Do
- Reproduce each anomaly with two sessions on a real database.
- State, from memory, what each ANSI level prevents and what PostgreSQL, MySQL and SQL Server actually do.
- Prevent a double-spend / overselling bug three different ways and compare them.

---

# 23. Deadlocks 🔴

> **Level:** Core → Intermediate

## 23.1 Fundamentals
- Definition; **four necessary (Coffman) conditions:** mutual exclusion, hold-and-wait, no preemption, circular wait
- Typical causes: inconsistent lock ordering, lock upgrades (S→X), missing indexes causing wider locks, long transactions, foreign-key locks

## 23.2 Detection
- Wait-for graph; cycle detection; detection frequency; lock timeouts as a crude alternative
- **Victim selection:** cost of rollback, age, work done, number of times victimized (starvation avoidance)
- Engine behavior: PG `deadlock_timeout` and error 40P01; MySQL error 1213 (InnoDB picks a victim); SQL Server error 1205

## 23.3 Prevention and Avoidance
- Timestamp-based schemes: **wait-die** (non-preemptive), **wound-wait** (preemptive); starvation properties
- Conservative 2PL; global lock ordering; no-wait / timeouts
- Deadlock avoidance vs prevention vs detection (Banker's-algorithm awareness)

## 23.4 Application-Level Handling
- Retry with backoff on deadlock/serialization failures; idempotent operations
- Consistent access order (e.g., always update lower account ID first); short transactions; proper indexes
- Reading engine deadlock graphs/logs (`SHOW ENGINE INNODB STATUS`, PG logs, SQL Server deadlock graph/extended events)

## 23.5 Related Problems
- Livelock, starvation, lock convoys, lock escalation, blocking chains (blocking ≠ deadlock)

### What You Should Be Able to Do
- Detect a deadlock in a given lock-wait table by drawing the wait-for graph.
- Apply wait-die and wound-wait to a timestamped scenario.
- Diagnose a production deadlock from an engine log and fix it via ordering/indexing/retry.

---

# 24. Timestamp Ordering, Optimistic Control, MVCC, Snapshot Isolation 🟠

> **Level:** Intermediate (MVCC is practical-critical; the others are theory)

## 24.1 Timestamp Ordering (TO) 🟡
- Transaction timestamps; `R-TS(X)`, `W-TS(X)`; read/write rules; Thomas write rule; rollbacks on late operations
- Strict TO for recoverability; TO vs 2PL comparison

## 24.2 Optimistic Concurrency Control (OCC)
- Phases: read → validation → write; backward/forward validation
- When OCC wins (low conflict, read-mostly) vs loses (high contention ⇒ many aborts)
- Application-level OCC: version columns, ETags, `rowversion`, compare-and-swap, `WHERE version = :v`

## 24.3 MVCC 🔴 (practical)
- Core idea: **readers don't block writers; writers don't block readers**
- Row versions (xmin/xmax in PG; undo-log version chain in InnoDB; version store in `tempdb` for SQL Server)
- Snapshots and visibility rules; read view; transaction ID horizon
- Garbage collection: PG `VACUUM`/autovacuum, bloat, transaction ID wraparound (awareness); InnoDB purge; SQL Server version cleanup
- Costs: write amplification, long transactions pin old versions, storage bloat

## 24.4 Snapshot Isolation (SI)
- Definition: reads from a consistent snapshot; first-committer-wins on write-write conflicts
- Prevents dirty, non-repeatable and (practically) phantom reads; **allows write skew**
- SSI (serializable snapshot isolation) as the fix (PG)

## 24.5 Pessimistic vs Optimistic vs Multi-Version (comparison)
- Lock-based, timestamp, optimistic, MVCC — which engines use which

### What You Should Be Able to Do
- Walk through two concurrent transactions under MVCC and say which row versions each sees.
- Explain why a long-running transaction can bloat a PostgreSQL table.
- Implement optimistic locking in SQL and in an ORM, including the retry/conflict-message path.

---

# 25. Recovery and Logging 🟠

> **Level:** Intermediate (concepts) → Advanced (ARIES)

## 25.1 Failure Classification
- Transaction failure (logical error, deadlock victim), system crash (volatile memory lost), media/disk failure, network/communication failure, human error (`DROP TABLE`, bad `UPDATE`)
- Stable storage concept; non-volatile vs volatile

## 25.2 Logging Fundamentals
- Log records: `<T, X, old, new>`, `<T start>`, `<T commit>`, `<T abort>`; log sequence numbers (LSN)
- **Write-Ahead Logging (WAL):** log before data; force log at commit; why durable commit needs `fsync`
- Steal / no-steal and force / no-force buffer policies; why *steal + no-force* needs both undo and redo
- Group commit and its throughput effect; synchronous_commit / durability settings trade-offs

## 25.3 Recovery Techniques
- **Deferred update** (NO-UNDO/REDO), **immediate update** (UNDO/REDO)
- Undo and redo rules; idempotent redo; compensation log records (CLRs)
- **Checkpoints:** sharp vs fuzzy; recovery starting point; checkpoint tuning vs I/O spikes
- **Shadow paging** (alternative; used conceptually in LMDB-style copy-on-write stores)

## 25.4 ARIES 🟢
- Three phases: **Analysis → Redo → Undo**; dirty page table, transaction table; pageLSN; repeating history; physiological logging

## 25.5 Crash Recovery Walkthrough
- Given a log with checkpoint and a crash point: list which transactions are redone, undone, ignored

## 25.6 Practical Link
- PG WAL/`pg_wal`, InnoDB redo/undo logs, SQL Server transaction log and recovery models (simple/full/bulk-logged)
- WAL is reused for replication (§36) and PITR (§35) and CDC (§44)

### What You Should Be Able to Do
- Explain what happens, step by step, when the DB crashes with committed and uncommitted transactions in flight.
- Process a log by hand and identify redo/undo sets.
- Explain why `COMMIT` returning guarantees durability, and what relaxing it risks.

---

# PART VI — STORAGE, INDEXING, AND THE QUERY ENGINE

---

# 26. Storage Internals 🟠

> **Level:** Intermediate

## 26.1 Storage Hierarchy and Hardware
- Registers/cache → RAM → SSD → HDD → network/object storage; latency orders of magnitude
- HDD: seek time, rotational latency, transfer rate; sequential vs random I/O
- SSD/NVMe: no seek, page-read/block-erase, write amplification, wear; why random reads are cheap but not free
- Implications: minimize page reads; sequential access; cache hit ratio

## 26.2 Pages, Blocks, Records
- Page/block as the unit of I/O (4–16 KB typical; 8 KB PG, 16 KB InnoDB, 8 KB SQL Server)
- **Slotted page** layout: header, slot directory, free space, record area; record IDs (page, slot); record movement/forwarding
- Fixed-length vs variable-length records; null bitmaps; offset arrays; spanned vs unspanned records
- Large objects/TOAST/off-row storage (awareness)
- Row store vs column store (preview of §41)

## 26.3 File Organization
- **Heap file** (unordered; fast insert; slow search), **sorted/sequential file**, **hash file**, **clustered/index-organized table** (InnoDB, SQL Server clustered index) vs heap tables (PG)
- Comparison on insert, point lookup, range query, update, space
- Free-space management: free-space map, page fill factor, row migration, fragmentation

## 26.4 Buffer Manager
- Buffer pool; frames; page table; pin/unpin; dirty pages; flushing and background writers
- Replacement: LRU, Clock, LRU-K/2Q (awareness); **scan resistance** (sequential flooding)
- Buffer hit ratio; double buffering with OS cache; prefetch/read-ahead
- Interaction with WAL (steal/no-force, §25)

## 26.5 Storage Engines
- InnoDB (MySQL), heap + MVCC (PG), LSM-based engines (RocksDB; §29), in-memory engines (awareness)

## 26.6 Row-Oriented vs Column-Oriented (preview)
- Compression, vectorized execution, analytic scan efficiency — details in §41

### What You Should Be Able to Do
- Compute blocking factor, number of blocks, and I/O cost for a file (see §48).
- Explain why a `SELECT *` on a wide table is slower than selecting a few columns.
- Explain buffer pool sizing and why a cold cache makes queries slow after restart.

---

# 27. Indexing 🔴

> **Level:** Core → Intermediate

## 27.1 Why Indexes Work
- Avoid full scans; reduce page reads; ordered access; enforce uniqueness
- Cost model: reads faster; writes slower; extra storage; maintenance and fragmentation

## 27.2 Classic Index Taxonomy (ordered-file indexes)
- **Primary index** (on ordering key of a sorted file), **clustering index**, **secondary index**
- **Dense vs sparse** index; multilevel index (→ ISAM → B+ tree)
- Block-access calculations with index levels (§48)

## 27.3 Modern Index Types and Terminology
- **Clustered vs non-clustered** (SQL Server/InnoDB: table is stored in clustered-key order; secondary indexes store the clustering key / PK as row locator → the "double lookup" cost)
- **Composite (multi-column)** indexes; **covering index** (`INCLUDE` columns; index-only scan); **unique** index
- **Partial / filtered** index; **expression / functional** index
- Index on foreign keys; on computed columns; on JSON paths

## 27.4 Designing Composite Indexes
- **Leftmost-prefix rule** (B-tree indexes)
- Column order: equality columns first, then range column, then sort/other columns (the "ESR"-style rule)
- Matching `ORDER BY` direction to avoid sorts; index for `GROUP BY`
- Selectivity vs cardinality; low-selectivity columns (booleans); statistics and histograms
- Redundant/duplicate/unused indexes; over-indexing write penalty

## 27.5 Index Maintenance
- Page splits, fill factor, fragmentation, bloat; rebuild vs reorganize (`REINDEX`, `VACUUM`, `ALTER INDEX`)
- Online index builds (`CREATE INDEX CONCURRENTLY`, `ONLINE = ON`)
- Statistics updates (`ANALYZE`, `UPDATE STATISTICS`)
- Finding unused/missing indexes via system views

## 27.6 When an Index Is Not Used
- Non-sargable predicates, functions on columns, leading wildcards, implicit conversions, low selectivity, small tables, stale statistics, mismatched collation, `OR` conditions, wrong column order

### What You Should Be Able to Do
- Design the best index for a query with equality, range and `ORDER BY` clauses.
- Explain clustered vs non-clustered, and why a PK choice (random UUID vs sequential) affects InnoDB/SQL Server performance.
- Predict whether a given query can use a given index, and why not.
- Estimate how much an extra index costs each `INSERT`.

---

# 28. B-Trees and B+ Trees 🔴

> **Level:** Core (concepts) → Intermediate (paper problems)

## 28.1 B-Tree
- Properties of order *m*: node capacity, minimum occupancy, balanced height
- Search, insertion with node split, deletion with borrow/merge

## 28.2 B+ Tree
- Internal nodes store separator keys only; all data/pointers in leaves; leaves linked in a list
- Higher fan-out ⇒ lower height; efficient range scans; predictable lookup cost
- Insertion (split and promote/copy-up), deletion (redistribute/merge), bulk loading
- Handling duplicates and variable-length keys; prefix compression (awareness)

## 28.3 B-Tree vs B+ Tree
- Search consistency, range queries, fan-out, storage, internal-node data

## 28.4 Why Databases Use B+ Trees
- Disk-page-aligned nodes, shallow height (3–4 levels for billions of rows), sorted order, range support, good cache behavior for upper levels

## 28.5 Concurrency and Variants (🟢)
- Latch crabbing; Blink trees; fractal trees; Bw-tree (awareness)

## 28.6 Numerical Problems
- Order/fan-out from block size, key size, pointer size
- Max/min keys per node; height for N records; number of leaf blocks; I/Os for point and range lookup
- Step-by-step insertion/deletion sequences with splits (draw trees)

### What You Should Be Able to Do
- Insert and delete a given sequence into a B+ tree of given order, drawing each state.
- Compute the height of a B+ tree for 100 million rows with given page/key sizes.
- Explain in one minute why B+ trees (not binary trees or hash tables) dominate database indexing.

---

# 29. Hashing and Other Index Structures 🟠

> **Level:** Intermediate → Advanced

## 29.1 Hash-Based Indexing
- Hash function, buckets, collisions (chaining/overflow, open addressing concept)
- **Static hashing:** overflow chains, fixed bucket count problems
- **Dynamic hashing:** **extendible hashing** (directory, global/local depth, splitting, directory doubling), **linear hashing** (split pointer, no directory)
- Hash index vs B+ tree: equality only vs range/order; PG hash indexes, MySQL MEMORY/adaptive hash index

## 29.2 Other Index Structures (awareness; each tied to a use case)
- **LSM trees** (memtable, SSTables, compaction, bloom filters; RocksDB/Cassandra/LevelDB): write-optimized, read amplification trade-offs — 🟡
- **Bitmap indexes** (low-cardinality, analytic/warehouse; Oracle) — 🟢
- **GIN / inverted indexes** (full-text, JSON, arrays), **GiST/SP-GiST**, **R-tree** (spatial), **BRIN** (block-range, huge append-only tables), **trie/radix** — 🟢
- **Skip lists**, **bloom filters** (membership tests), **columnstore indexes** — 🟢
- Vector indexes (HNSW, IVF) for similarity search — 🟢 Optional

## 29.3 Choosing an Index Structure
- Decision table: equality, range, text, spatial, high write volume, analytic scans

### What You Should Be Able to Do
- Perform inserts into an extendible hash directory with splits and depth changes.
- Compare B+ tree and LSM tree on read, write, space amplification.
- Choose an index type for: full-text search, JSON containment, geographic radius, time-ordered log table.

---

# 30. Query Processing and Join Algorithms 🟠

> **Level:** Intermediate

## 30.1 Query Processing Pipeline
```text
SQL text → Parser (syntax) → Semantic analysis/binder (names, types, permissions)
   → Rewriter (views, rules, simplification) → Logical plan (relational algebra tree)
   → Optimizer (cost-based) → Physical plan → Executor → Storage/Buffer/Index
```
- Parse tree; algebra tree; plan caching and prepared statements

## 30.2 Physical Operators
- **Access paths:** sequential/table scan, index scan, index seek (range), index-only scan, bitmap index scan, key/RID lookup
- **Selection and projection** operators
- **External merge sort** (runs, passes, memory), top-N heap sort
- **Aggregation:** hash aggregate vs sort (stream) aggregate
- **Duplicate elimination:** hash vs sort
- Execution models: iterator/Volcano (pull), materialization, vectorized, pipeline breakers (sort, hash build)

## 30.3 Join Algorithms 🔴 (explicit coverage)
- **Nested-loop join (NLJ):** tuple-at-a-time; cost `b_r + n_r × b_s`
- **Block nested-loop join (BNLJ):** cost `b_r + ⌈b_r / (M−2)⌉ × b_s`
- **Index nested-loop join (INLJ):** cost `b_r + n_r × c` where c = index lookup cost; great for selective outer + indexed inner
- **Sort-merge join:** sort both (or use sorted order from indexes), merge; cost `sort(R) + sort(S) + b_r + b_s`; good for pre-sorted inputs, non-equi/range joins support partially, produces sorted output
- **Hash join:** build hash table on smaller input, probe with larger; in-memory vs **Grace hash join** (partition then join); cost ≈ `3(b_r + b_s)` when partitioning is required; equality joins only
- When each wins; memory dependence; skew effects; hybrid hash join (🟡)
- Semi-join and anti-join implementations

## 30.4 Parallel and Distributed Execution (🟢 awareness)
- Parallel scans, partition-wise joins, exchange operators; shuffle/broadcast joins in distributed engines

### What You Should Be Able to Do
- Choose and justify a join algorithm for given table sizes, indexes and memory.
- Compute I/O costs of NLJ, BNLJ, hash and sort-merge joins for given block counts.
- Draw the operator tree for a three-table query.

---

# 31. Query Optimization 🔴

> **Level:** Intermediate → Advanced

## 31.1 Why Optimize
- One SQL statement ⇒ many equivalent plans with large cost differences

## 31.2 Heuristic (Rule-Based) Optimization
- Push selections down; push projections down; combine selection with Cartesian product into join
- Algebra equivalence rules; subquery unnesting/decorrelation; view merging; constant folding; transitive predicate inference

## 31.3 Cost-Based Optimization (CBO)
- Cost model: I/O, CPU, memory, (network in distributed)
- **Statistics:** row counts, distinct counts, min/max, null fraction, **histograms**, most-common values, correlation, multi-column statistics
- **Selectivity estimation** (equality `1/V(A)`, range, conjunction under independence assumption, join selectivity)
- **Cardinality estimation** and why errors compound through joins (the main reason for bad plans)
- Join ordering: left-deep vs bushy trees; dynamic programming (System R) search; search-space pruning; greedy/genetic fallback for many tables
- Interesting orders; physical properties

## 31.4 Sargability and SQL-Level Optimization
- **Sargable** predicates (index-friendly) vs non-sargable (function on column, expression on column, leading `%`, implicit conversion, `OR` across columns, `<>`)
- Rewrite patterns: `WHERE DATE(col) = x` → range predicate; `OR` → `UNION ALL`; `IN (subquery)` ↔ `EXISTS`; avoid `SELECT *`; avoid `DISTINCT` as a bandage for join bugs; pre-aggregate before joining
- Parameter sniffing and plan caching (SQL Server/PG generic vs custom plans)

## 31.5 Plan Problems
- Stale/missing statistics; skewed data; correlated columns; plan regressions after upgrades or data growth; hints and plan guides (last resort); forcing plans (Query Store, `pg_hint_plan`)

### What You Should Be Able to Do
- Rewrite a slow query into a sargable form and justify the index it needs.
- Estimate output cardinality of a filter + join using given statistics.
- Explain why the optimizer may choose a seq scan over an available index.

---

# 32. Execution Plans 🔴

> **Level:** Core (reading) → Intermediate

## 32.1 Tooling
- `EXPLAIN` (estimated), `EXPLAIN ANALYZE` (actual; **executes the statement**—wrap DML in a rolled-back transaction), `EXPLAIN (ANALYZE, BUFFERS)` (PG), `SET SHOWPLAN`/actual execution plan (SQL Server), `EXPLAIN FORMAT=TREE/JSON`/`EXPLAIN ANALYZE` (MySQL 8)
- Estimated vs actual rows; cost units (relative, not time)

## 32.2 Reading a Plan
- Operator tree order of execution (bottom-up, inner to outer); startup vs total cost; loops
- Operators: Seq/Table Scan, Index Scan, Index Seek, Index-Only Scan, Bitmap Heap Scan, Key/RID Lookup, Sort, Hash Aggregate, Stream Aggregate, Nested Loop, Hash Join, Merge Join, Filter, Limit, Materialize, Gather (parallel)
- Predicates: index condition vs filter (post-fetch), rows removed by filter, seek predicate vs residual predicate

## 32.3 Warning Signs
- Large gap between estimated and actual rows
- Seq scan on large table with highly selective filter
- Sorts spilling to disk / hash spills; temp files
- Nested loop with huge outer row count; repeated key lookups
- Missing join predicate (Cartesian product)
- High buffer reads / low cache-hit; parallelism skew

## 32.4 Systematic Tuning Workflow
```text
Capture slow query → get actual plan → compare estimated vs actual rows
→ find most expensive node → check predicate sargability & statistics
→ check indexes (missing / wrong order / not covering)
→ rewrite query or add index → re-measure (time + I/O) → check write impact
```

### What You Should Be Able to Do
- Read an `EXPLAIN ANALYZE` output and identify the bottleneck node.
- Predict the plan change when adding a composite/covering index.
- Explain index scan vs index seek vs table scan in a SQL Server and PG context.

---

# 33. Performance Engineering and Observability 🔴

> **Level:** Intermediate → Advanced (practical)

## 33.1 Performance Investigation Method
- Define the symptom (latency, throughput, errors); locate layer (app, network, pool, DB); measure before changing; change one thing at a time

## 33.2 Query Performance
- Slow query logs (`log_min_duration_statement`, `slow_query_log`, Query Store, `pg_stat_statements`)
- Top queries by total time vs by mean time vs by calls
- Missing indexes, over-fetching columns/rows, large scans, bad join order, stale statistics, non-sargable predicates, temp-table spills, function calls per row, implicit conversions
- Query plan regression (after stats refresh, upgrade, parameter sniffing)

## 33.3 Application-Level Causes
- **N+1 query problem** (cause: lazy loading in loops; fix: join/eager load, batch `IN`, DataLoader pattern)
- Chatty APIs; ORMs generating poor SQL; unbounded result sets; missing pagination
- Large `OFFSET`; `COUNT(*)` on huge tables; `SELECT *`
- Connection pool exhaustion/leaks; long transactions held by app code
- Cache stampede; cache invalidation (relation to DB load)

## 33.4 Resource Bottlenecks
- **CPU:** expensive queries, parsing/planning storms (no prepared statements), JSON/regex functions
- **Memory:** buffer pool too small, work_mem/sort/hash spills, connection memory
- **Disk I/O:** random reads, checkpoint spikes, WAL fsync latency, temp file usage
- **Network:** result size, round trips, cross-AZ latency
- **Lock contention:** blocking chains, hot rows (counters), lock escalation, long transactions; diagnosing via `pg_locks`/`pg_stat_activity`, `sys.dm_tran_locks`, `performance_schema`
- **Connection limits** and pooling (§42)
- Temp tables / temp storage pressure

## 33.5 Write-Path Performance
- Batch inserts, multi-row statements, `COPY`/bulk load, transaction batching; index and trigger overhead; hot-spot inserts (monotonic keys), fill factor; group commit; `UPDATE` hot rows (counter contention → sharded counters)

## 33.6 Observability
- Metrics: QPS, p50/p95/p99 latency, error rates, active connections, replication lag, cache-hit ratio, lock waits, deadlocks, checkpoint/WAL rate, disk/IOPS, table/index size growth, bloat
- Tools/views: `pg_stat_*`, `sys.dm_*`, Query Store, `performance_schema`/`sys` schema, APM tracing with SQL spans
- Alerting and capacity planning; baselines

## 33.7 Caching Strategies
- Cache-aside, read-through, write-through, write-behind; TTL and invalidation; stampede protection; when caching hides vs fixes problems

### What You Should Be Able to Do
- Walk through "a production query takes 10 seconds" from symptom to fix (see §53 closing framework).
- Diagnose CPU spike, lock contention, and connection-pool exhaustion using DB views.
- Identify and fix an N+1 problem in code and verify via query count.

---

# PART VII — DATABASE OPERATIONS

---

# 34. Database Security 🔴

> **Level:** Core (SQL injection, least privilege) → Intermediate

## 34.1 Authentication
- Database users/logins, password policies, certificate/Kerberos/IAM-based auth, SSO; service accounts; rotating credentials

## 34.2 Authorization
- Roles and role hierarchies; `GRANT`/`REVOKE`/`DENY`; object-, column-, schema-level privileges; ownership; default privileges
- **Least privilege:** separate app (DML-only), migration (DDL), read-only/reporting, admin accounts
- **Row-level security** (PG policies, SQL Server RLS), views and column masking for restricted access

## 34.3 SQL Injection 🔴
- Mechanism: untrusted input concatenated into SQL; in-band, blind, second-order injection
- **Defenses:** parameterized queries / prepared statements (primary), ORM parameterization, allow-listing for identifiers (table/column/order-by), stored procedures *without* dynamic SQL, input validation, least-privilege accounts, error-message hygiene
- ORMs are not automatically safe (raw SQL interpolation: e.g., `FromSqlRaw` with string interpolation vs `FromSqlInterpolated`)

## 34.4 Data Protection
- Encryption in transit (TLS), at rest (TDE, disk/volume encryption), column-level/application-level encryption, key management (KMS/HSM)
- Password storage: salted adaptive hashing (bcrypt/scrypt/Argon2) — never reversible encryption
- Secrets management: no credentials in code/repos; vaults; rotation
- Data masking, tokenization, anonymization; PII/PCI/GDPR/HIPAA awareness; right to erasure vs backups/soft delete

## 34.5 Auditing and Governance
- Audit logs (who/what/when), trigger-based vs native auditing (`pgaudit`, SQL Server Audit), tamper-evidence; retention
- Network controls: private subnets, firewalls, no public DB endpoints; bastion/proxy

### What You Should Be Able to Do
- Demonstrate an injection attack and fix it with parameters.
- Design a role/privilege model for app, migration, analyst and admin users.
- List the encryption and key-management layers for a payment database.

---

# 35. Backup, Restore, and Disaster Recovery 🟠

> **Level:** Intermediate

## 35.1 Backup Types
- Full, incremental, differential; logical (`pg_dump`, `mysqldump`) vs physical (file/snapshot/`pg_basebackup`); hot vs cold; snapshot backups
- Continuous archiving of the transaction log / WAL

## 35.2 Restore and PITR
- Restore procedure; **point-in-time recovery** = base backup + log replay up to a timestamp/LSN/transaction
- Recovery models (SQL Server: simple/full/bulk-logged)
- Partial restores; table-level recovery; recovering from accidental `DELETE`/`DROP`

## 35.3 Objectives and Strategy
- **RPO** (acceptable data loss) and **RTO** (acceptable downtime); how they drive backup frequency, replication mode, standby design
- 3-2-1 rule; retention policy; off-site/cross-region copies; encryption of backups
- **Backup verification:** test restores, checksums, restore drills (an untested backup is not a backup)

## 35.4 Disaster Recovery
- DR patterns: backup/restore, pilot light, warm standby, hot standby/multi-region active-active
- Failover runbooks, DNS/connection-string failover, split-brain prevention, failback
- Ransomware and logical-corruption scenarios; immutable backups

### What You Should Be Able to Do
- Choose a backup/replication design to meet RPO = 5 min, RTO = 30 min.
- Describe, step by step, how to recover a database to 14:05 yesterday.
- Distinguish backup, replication, and HA (replication is not a backup).

---

# 36. Replication and High Availability 🟠

> **Level:** Intermediate

## 36.1 Why Replicate
- High availability, read scaling, geographic latency, DR, analytics offload, zero-downtime maintenance

## 36.2 Replication Models
- **Leader–follower (primary–replica)**, multi-leader (multi-primary), leaderless (Dynamo-style quorum; see §38/§39)
- **Synchronous vs asynchronous vs semi-synchronous**; durability vs latency vs availability
- Physical (WAL/binary) vs logical (row/statement-based) replication; statement-based pitfalls (non-determinism)
- Streaming vs log shipping; cascading replicas; snapshot + catch-up for new replicas

## 36.3 Operational Issues
- **Replication lag** and its consequences: stale reads, read-your-writes violations, monotonic reads
- Mitigations: read from primary after write, session stickiness, wait-for-LSN/GTID, lag-aware routing
- **Failover:** detection, promotion, fencing (STONITH), lost writes in async failover, client reconnection
- **Split brain** and how quorum/consensus/fencing prevent it
- **Conflict resolution** in multi-primary: last-write-wins, vector clocks, CRDTs (awareness), application-level merge
- Replica identity, schema changes across replicas, replication slots and WAL retention

## 36.4 Read/Write Splitting
- Router/proxy vs app-level routing; consistency pitfalls; transactional reads must go to primary

## 36.5 HA Technologies (awareness)
- PostgreSQL streaming replication + Patroni/repmgr; MySQL async/semisync/Group Replication/InnoDB Cluster; SQL Server Always On Availability Groups; cloud managed multi-AZ

### What You Should Be Able to Do
- Explain what data can be lost on async failover and how sync replication changes that.
- Design a read-replica strategy with correct read-your-writes behavior.
- Describe how a cluster avoids split brain.

---

# 37. Partitioning and Sharding 🟠

> **Level:** Intermediate → Advanced

## 37.1 Partitioning (within one database)
- Horizontal vs vertical partitioning
- Strategies: **range** (time-series), **list** (region), **hash** (even spread), **composite**
- **Partition pruning**; partition-wise joins; local vs global indexes; partition key in PK/unique constraints
- Maintenance benefits: dropping old partitions instead of mass `DELETE`; archival; parallelism
- Pitfalls: queries without partition key scan all partitions; too many partitions; skew

## 37.2 Sharding (across databases/servers)
- Shard, shard key selection (cardinality, even distribution, query locality, immutability)
- Routing: client-side, proxy/router, directory/lookup table, consistent hashing, virtual nodes
- Strategies: range, hash, directory-based, geo-sharding
- **Hot shards/keys** (celebrity problem), time-based hotspots, uneven tenant sizes
- **Rebalancing and resharding:** consistent hashing, split/merge, online migration, double-write/backfill/cutover
- **Cross-shard queries and joins** (scatter-gather), **cross-shard transactions** (2PC, sagas, avoiding them via data locality)
- Global unique IDs (Snowflake, UUID, ranges), global secondary indexes, auto-increment pitfalls
- When *not* to shard: vertical scaling, read replicas, caching, partitioning, archiving come first

## 37.3 Comparison
- Partitioning vs sharding vs replication — what problem each solves

### What You Should Be Able to Do
- Choose a shard key for orders, chats, and multi-tenant SaaS, and justify.
- Describe an online resharding plan with no downtime.
- Explain why a query without the shard key becomes expensive.

---

# PART VIII — DISTRIBUTED AND ALTERNATIVE DATA SYSTEMS

---

# 38. Distributed Databases 🟠

> **Level:** Intermediate → Advanced

## 38.1 Fundamentals
- Distributed vs parallel databases; transparency (location, replication, fragmentation); data fragmentation and allocation
- Failure modes: node crash, network partition, partial failure, message loss/delay, clock skew
- Distributed query processing basics (ship data vs ship query; semi-join reduction) — 🟡

## 38.2 CAP and PACELC
- **CAP:** consistency (linearizability), availability, partition tolerance — only a choice during a partition; common misreadings
- **PACELC:** if Partition → A vs C; Else → Latency vs Consistency
- Classifying real systems (e.g., Spanner-like CP, Dynamo/Cassandra-like AP tunable)

## 38.3 Consistency Models
- Linearizability/strong consistency, sequential, **causal**, **read-your-writes**, monotonic reads/writes, session guarantees, **eventual consistency**
- Quorum reads/writes: `R + W > N`; tunable consistency; read repair, hinted handoff, anti-entropy (awareness)
- Clocks: wall-clock vs logical (Lamport) vs vector clocks; hybrid logical clocks; TrueTime (awareness)

## 38.4 Distributed Transactions
- **Two-Phase Commit (2PC):** coordinator/participants, prepare (vote) phase, commit/abort phase; blocking on coordinator failure; recovery with logs; failure scenarios at each step
- Three-phase commit (awareness); XA/MS-DTC
- **Sagas** and compensating transactions (alternative to 2PC; eventual consistency), TCC; idempotency requirements
- Outbox + idempotent consumers (see §44)

## 38.5 Consensus (introductory) 🟡
- Why consensus: leader election, replicated state machines, consistent metadata
- **Raft** (leader election, log replication, terms, majority quorum, safety) at conceptual level; **Paxos** awareness
- Used in etcd, Consul, CockroachDB, TiDB, Spanner-like systems; ZooKeeper/ZAB
- Fencing tokens and leases for distributed locks (and why naive Redis locks can be unsafe) — 🟡

### What You Should Be Able to Do
- Explain CAP/PACELC precisely and apply them to a design decision.
- Walk through 2PC and describe what happens if the coordinator crashes after prepare.
- Choose between 2PC and saga for an order–payment–inventory workflow.
- Explain at a high level how Raft elects a leader and commits a log entry.

---

# 39. NoSQL Databases 🟠

> **Level:** Intermediate

## 39.1 Why NoSQL
- Flexible schema, horizontal scale, high write throughput, low latency, specialized data shapes
- Trade-offs: weaker joins/ad-hoc queries, limited multi-document transactions (varies), application-enforced integrity

## 39.2 Categories
- **Key-value** (Redis, DynamoDB, Riak): access by key; caching, sessions, counters, rate limiters; data structures (Redis lists/sets/sorted sets/streams)
- **Document** (MongoDB, Couchbase, Firestore): JSON/BSON docs; embedding vs referencing; secondary indexes; aggregation pipeline; multi-document transactions
- **Wide-column** (Cassandra, HBase, Bigtable, ScyllaDB): partition key + clustering key; LSM storage; tunable consistency; query-first modeling
- **Graph** (Neo4j, Neptune): nodes/edges/properties; traversals (Cypher/Gremlin); recommendations, fraud, social graphs
- Also: time-series, search, vector (see §40)

## 39.3 NoSQL Data Modeling
- **Access-pattern-driven design** (list queries first, then model)
- Denormalization and duplication; embedding vs referencing; precomputed views per query
- Partition key design (cardinality, hot partitions), sort/clustering key, single-table design (DynamoDB)
- Secondary indexes (local/global) and their consistency costs
- Handling relationships without joins; schema versioning in schemaless stores
- Replication, consistency levels, conflict resolution (LWW, vector clocks)

## 39.4 SQL vs NoSQL Decision
- Compare: schema, transactions, joins, scaling model, consistency, query flexibility, maturity, operational cost, typical use cases
- Pitfalls: choosing NoSQL for hype; reinventing joins in application code; MongoDB-without-schema chaos
- Modern convergence: PG JSONB, multi-model DBs, document stores with ACID

### What You Should Be Able to Do
- Model a chat/feed/shopping-cart/IoT workload in a document store and in DynamoDB/Cassandra style.
- Justify (or reject) NoSQL for a given product requirement.
- Explain partition-key hotspots and fixes.

---

# 40. NewSQL and Specialized Data Stores 🟡

> **Level:** Intermediate → Optional

## 40.1 NewSQL / Distributed SQL
- Goals: SQL + ACID + horizontal scale (Google Spanner, CockroachDB, TiDB, YugabyteDB, Aurora-style architectures)
- Typical internals: range-partitioned key-value store + Raft replication + distributed transactions
- Trade-offs vs traditional RDBMS and NoSQL (latency of cross-region commits, operational complexity)

## 40.2 Specialized Stores (awareness)
- **Cache/in-memory:** Redis, Memcached
- **Search:** Elasticsearch/OpenSearch (inverted index)
- **Time-series:** TimescaleDB, InfluxDB (retention, downsampling, compression)
- **Vector databases / pgvector:** embeddings, ANN search
- **Message/streaming logs:** Kafka as a log (not a DB, but central to data pipelines; CDC target)
- **Embedded:** SQLite, RocksDB; **object storage** + lakehouse (Parquet, Iceberg, Delta) — 🟢

## 40.3 Choosing Datastores
- Source of truth vs derived data; keep one system of record; rebuildable derived stores

### What You Should Be Able to Do
- Explain what makes a database "NewSQL" and name its core mechanism.
- Pick the right store for: search, rate limiting, metrics, embeddings, job queue.

---

# 41. OLTP, OLAP, and Data Warehousing 🟠

> **Level:** Intermediate

## 41.1 OLTP vs OLAP
- OLTP: many short transactions, point reads/writes, normalized schema, row store, low latency
- OLAP: large scans/aggregations, historical data, denormalized/dimensional schema, column store, throughput
- HTAP (awareness)

## 41.2 Data Warehouse Concepts
- Data warehouse, data mart, data lake, lakehouse; staging layer; ODS
- **ETL vs ELT**; batch vs streaming; orchestration; data quality, idempotent loads, incremental loads/watermarks
- CDC-driven pipelines (see §44)

## 41.3 Dimensional Modeling
- **Fact tables** (transaction, periodic snapshot, accumulating snapshot), **dimension tables**, **grain** (declare it first!), measures (additive, semi-additive, non-additive)
- **Star schema** vs **snowflake schema**; surrogate keys in dimensions; conformed dimensions; degenerate dimensions; junk dimensions
- **Slowly changing dimensions (SCD):** Type 1 (overwrite), Type 2 (history rows), Type 3 (previous-value column)
- Date dimension

## 41.4 Analytical Engines
- Columnar storage, compression, vectorized execution, partition/cluster pruning, materialized views, aggregates/cubes (Snowflake, BigQuery, Redshift, ClickHouse) — awareness 🟢
- Row vs column store trade-offs

### What You Should Be Able to Do
- Design a star schema for sales analytics with a stated grain.
- Explain SCD Type 2 and write the SQL to expire/insert versions.
- Explain why the same data lives in different shapes in OLTP and OLAP systems.

---

# PART IX — BACKEND ENGINEERING WITH DATABASES

---

# 42. Application Integration: Connections, Pooling, Transactions 🔴

> **Level:** Core for backend engineers

## 42.1 Connectivity Stack
```text
Application code → ORM / data-access library → Driver (ADO.NET / JDBC / psycopg …)
→ Connection pool → Network (TLS) → DB server → Parser/Optimizer → Storage → Result stream
```
- Connection strings, credentials, TLS settings, command vs connection timeouts, retries

## 42.2 Connection Pooling
- Why: connection setup cost, server connection limits, memory per connection
- Pool sizing (not "bigger is better"; pool size ≈ cores × small factor; Little's Law thinking), max/min pool, idle timeout, max lifetime, acquisition timeout
- Leaks (not disposing connections/transactions), exhaustion symptoms, long-held connections
- External poolers: PgBouncer (transaction vs session pooling and prepared-statement/session-state caveats), ProxySQL, RDS Proxy
- Serverless/lambda connection storms

## 42.3 Prepared Statements and Plan Reuse
- Parameterization for security and plan-cache reuse; server-side vs client-side preparation; parameter sniffing; generic vs custom plans

## 42.4 Transactions from Application Code
- Unit-of-work scope; begin/commit/rollback with `using`/try-finally/`@Transactional`; transaction per request pattern
- Isolation level selection per transaction; read-only transactions
- Retry policies for deadlocks, serialization failures, transient faults (exponential backoff + jitter; idempotency)
- Pitfalls: network call inside transaction, swallowed exceptions, nested/ambient transactions, `TransactionScope` escalating to distributed transactions, transaction + message publish (dual write problem)
- Optimistic concurrency from code (version column; handle conflict exception)

## 42.5 Idempotency and Constraints
- Idempotency keys stored under a unique constraint; `INSERT ... ON CONFLICT DO NOTHING`; exactly-once-effect via at-least-once + dedupe
- Safe retries for payments and orders

## 42.6 Bulk, Streaming, and Batch Operations
- Batching inserts, bulk copy APIs, streaming large result sets, cursor/keyset iteration, avoiding loading millions of rows into memory

## 42.7 Distributed Locking and Coordination (awareness)
- DB-based locks (advisory locks, `SELECT FOR UPDATE`), lease rows, `SKIP LOCKED` queues; Redis/ZooKeeper/etcd locks; fencing tokens

### What You Should Be Able to Do
- Configure and tune a connection pool; diagnose "too many connections" and "timeout expired waiting for pool" errors.
- Write a retry wrapper that is safe (idempotent) for deadlock/serialization failures.
- Implement an idempotent payment-creation endpoint backed by a unique constraint.

---

# 43. ORM and EF Core Concepts 🟠

> **Level:** Intermediate (concepts transfer to Hibernate/JPA, SQLAlchemy, Django ORM, Sequelize, Prisma)

## 43.1 ORM Fundamentals
- Object-relational impedance mismatch; entity mapping (tables, columns, keys, relationships, owned types, value converters, inheritance mapping TPH/TPT/TPC)
- **Unit of Work** and **Identity Map** patterns; `DbContext`/Session lifecycle (short-lived, not thread-safe)
- **Change tracking** (snapshot vs notification), tracked vs `AsNoTracking`; `SaveChanges` batching and implicit transaction
- Repository pattern: when it adds value vs redundant over an ORM

## 43.2 Loading Strategies
- **Lazy**, **eager** (`Include`/`JOIN FETCH`), **explicit** loading; projection (`Select`) as the best default for reads
- **N+1** detection and fixes; **cartesian explosion** and split queries (`AsSplitQuery`)
- Over-fetching entire entities; pagination in ORM (keyset), compiled queries

## 43.3 Query Translation and Generated SQL
- LINQ/Criteria → SQL; client vs server evaluation; logging generated SQL (`LogTo`, `ToQueryString`, Hibernate `show_sql`); parameterization of values
- Raw SQL / stored procedure / Dapper escape hatches; ORM vs raw SQL vs micro-ORM trade-offs (productivity, control, performance, maintainability)

## 43.4 Concurrency and Transactions in ORMs
- Optimistic concurrency tokens (`[Timestamp]`, `IsConcurrencyToken`, `@Version`); `DbUpdateConcurrencyException` handling
- Explicit transactions, savepoints, `ExecuteUpdate/ExecuteDelete` bulk operations (bypass change tracker)
- Execution strategies (connection resiliency)

## 43.5 Migrations
- Code-first vs database-first; migration scripts; idempotent scripts; applying in CI/CD; rollback strategy; seed data; drift detection (see §44)

## 43.6 ORM Pitfalls
- Hidden queries in loops, tracking overhead on large reads, lazy-loading in serialization, mapping unbounded collections, leaking entities into API contracts, `Contains` with huge lists, ignoring indexes the ORM relies on

### What You Should Be Able to Do
- Explain what `SaveChanges()` does (detect changes, order operations, batch, transaction).
- Find and fix an N+1 and a cartesian-explosion problem in an EF Core query from its generated SQL.
- Decide when to drop to raw SQL.

---

# 44. Data Evolution and Integration Patterns 🟠

> **Level:** Intermediate → Advanced

## 44.1 Schema Migrations and Versioning
- Versioned migration scripts (Flyway, Liquibase, EF Migrations, Alembic); migration table; forward-only vs reversible
- **Zero-downtime migrations: expand → migrate → contract** (add nullable column → dual-write/backfill in batches → switch reads → drop old)
- Dangerous operations: adding non-null column with default on huge tables (engine-dependent), index builds, type changes, renames, locks taken by `ALTER`; lock timeouts; online DDL tools (`gh-ost`, `pt-online-schema-change`, `CONCURRENTLY`)
- Backward/forward compatibility between app versions and schema during rolling deploys
- Environments, seed/reference data, test data, drift

## 44.2 Change Data Capture (CDC) and Change Tracking
- Log-based CDC (WAL/binlog; Debezium), trigger-based, timestamp/polling; SQL Server CDC vs Change Tracking vs temporal tables
- Use cases: cache invalidation, search indexing, warehouse loading, microservice integration, audit
- Ordering, exactly-once vs at-least-once, schema evolution, initial snapshot

## 44.3 Outbox / Inbox Pattern
- Solves the **dual-write problem**: write business row + outbox row in one transaction; relay (poller/CDC) publishes to broker; consumers dedupe via inbox/idempotency table
- Delivery guarantees (at-least-once) and ordering per aggregate

## 44.4 CQRS and Event Sourcing (database considerations)
- CQRS: separate write model and read model(s); read stores (denormalized tables, replicas, search); eventual consistency between them
- Event sourcing: append-only event store, aggregate streams, optimistic concurrency by stream version, snapshots, projections/rebuilds, event schema evolution, GDPR conflicts
- When these patterns are over-engineering

## 44.5 Audit, History, and Archival
- Audit tables/triggers, temporal tables, event logs, immutability; retention, archival to cold storage, partition drop strategies

## 44.6 Data Quality and Reference Data
- Idempotent data loads; reconciliation jobs; constraint-based data quality; enumerations/reference data management

### What You Should Be Able to Do
- Plan a zero-downtime column rename on a billion-row table.
- Implement the outbox pattern and explain how it avoids lost or phantom events.
- Explain when CDC is preferable to polling or dual writes.

---

# 45. PostgreSQL, SQL Server, and MySQL Practical Knowledge 🟠

> **Level:** Intermediate — *concepts first; syntax second*

## 45.1 PostgreSQL
- Process-per-connection; MVCC with heap tuples (xmin/xmax), `VACUUM`/autovacuum, `ANALYZE`, HOT updates, bloat
- Rich indexes (B-tree, hash, GIN, GiST, BRIN, SP-GiST), partial/expression indexes, `INCLUDE`
- JSONB, arrays, CTEs, `RETURNING`, `ON CONFLICT`, `LISTEN/NOTIFY`, advisory locks, extensions (PostGIS, pg_trgm, pgvector), transactional DDL
- Isolation: RC (default), RR = snapshot isolation, SSI Serializable; `EXPLAIN (ANALYZE, BUFFERS)`; `pg_stat_statements`
- Streaming + logical replication; partitioning (declarative); roles/RLS

## 45.2 SQL Server
- Clustered index (table = B-tree) vs heap; non-clustered with key lookups; `INCLUDE`; filtered indexes; columnstore
- Locking default RC with optional RCSI/Snapshot; lock escalation; `tempdb` usage and version store; recovery models; transaction log
- Execution plans (actual/estimated), Query Store, parameter sniffing, missing-index DMVs, statistics
- T-SQL: `TOP`, `OFFSET/FETCH`, `IDENTITY`, `MERGE` (caveats), `OUTPUT`, `CROSS APPLY`, table variables vs temp tables, `TRY/CATCH`, `rowversion`, temporal tables
- Always On AG; Agent jobs; logins vs users; Azure SQL specifics

## 45.3 MySQL (InnoDB)
- Clustered index organized storage (PK matters: secondary indexes store PK); redo/undo logs; buffer pool; adaptive hash index
- Default RR with next-key/gap locks; `SELECT ... FOR UPDATE` behaviors; deadlock reporting (`SHOW ENGINE INNODB STATUS`)
- `AUTO_INCREMENT`, `ON DUPLICATE KEY UPDATE`, `EXPLAIN`/`EXPLAIN ANALYZE`, `sql_mode` (strictness), character sets/collations (`utf8mb4`), implicit commit on DDL
- Replication (binlog, GTID), Group Replication; MyISAM vs InnoDB (historical)

## 45.4 Vendor Difference Matrix (know these cold)

| Concept | PostgreSQL | SQL Server | MySQL (InnoDB) |
|---|---|---|---|
| Default isolation | Read Committed | Read Committed (locks; RCSI in Azure SQL) | Repeatable Read |
| MVCC storage | Heap tuples + vacuum | Version store in `tempdb` (when enabled) | Undo log version chain |
| Table storage | Heap (indexes separate) | Clustered B-tree or heap | Clustered by PK |
| Pagination | `LIMIT/OFFSET` | `OFFSET/FETCH`, `TOP` | `LIMIT/OFFSET` |
| Upsert | `ON CONFLICT` | `MERGE` | `ON DUPLICATE KEY UPDATE` |
| Auto IDs | `GENERATED AS IDENTITY`, sequences | `IDENTITY`, sequences | `AUTO_INCREMENT` |
| Return inserted data | `RETURNING` | `OUTPUT` | `LAST_INSERT_ID()` (limited) |
| Transactional DDL | Yes | Mostly yes | No (implicit commit) |
| Procedural language | PL/pgSQL | T-SQL | SQL/PSM |
| JSON | JSON/JSONB + GIN | JSON functions, `OPENJSON` | JSON type + generated-column indexes |
| Plan inspection | `EXPLAIN (ANALYZE)` | Graphical/actual plan, Query Store | `EXPLAIN`, `EXPLAIN ANALYZE` |
| Covering index | `INCLUDE` | `INCLUDE` | Composite index (no `INCLUDE`) |
| Partial/filtered index | Yes | Filtered index | No (use generated columns) |

### What You Should Be Able to Do
- Explain how one concept (e.g., isolation, indexing, upsert) differs across all three engines.
- Name the first diagnostic tool you'd use in each engine for slow queries, locks, and bloat.
- Port a query using pagination/upsert/date functions across dialects.

---

# PART X — PRACTICE AND INTERVIEW PREPARATION

---

# 46. Database Design Method and Case Studies 🔴

> **Level:** Intermediate → Advanced — *the capstone skill: turn vague requirements into a defensible schema*

## 46.1 The 20-Step Design Method

| # | Step | Question to answer |
|---|---|---|
| 1 | Requirement analysis | Who uses it? What are the use cases, volumes, SLAs, compliance needs? |
| 2 | Identify entities | What are the nouns that have identity and lifecycle? |
| 3 | Identify relationships | How do entities relate? Verbs and ownership. |
| 4 | Define cardinality & participation | 1:1, 1:N, M:N? Mandatory or optional? |
| 5 | Define primary keys | Natural vs surrogate? Type and generation strategy? |
| 6 | Define foreign keys | Referential actions? Indexed? |
| 7 | Define constraints | `NOT NULL`, `UNIQUE`, `CHECK`, defaults, state rules |
| 8 | Normalize | At least 3NF/BCNF for OLTP; justify any exception |
| 9 | Identify access patterns | Top 10 reads and writes, their frequency and latency targets |
| 10 | Design indexes | Support each access pattern; consider write cost |
| 11 | Decide transaction boundaries | Which operations must be atomic? Isolation level? |
| 12 | Consider concurrency | Hot rows, double-spend, overselling, uniqueness races, locking vs OCC |
| 13 | Consider scaling | Data volume growth, read/write ratio, vertical → replicas → partition → shard |
| 14 | Consider partitioning | Time-based or key-based? Retention via partition drop? |
| 15 | Consider replication | HA, read replicas, consistency expectations (read-your-writes) |
| 16 | Consider caching | What to cache, TTL, invalidation, stampede |
| 17 | Consider archival | Hot/warm/cold data, retention policy |
| 18 | Consider auditing | Who changed what and when; immutable history; legal needs |
| 19 | Consider backup & recovery | RPO/RTO, PITR, DR region |
| 20 | Consider security | PII, encryption, roles, row-level access, masking |

## 46.2 Case Studies (design each fully; compare with a reference solution)

| System | Core entities | Key design challenges to analyze |
|---|---|---|
| **E-commerce** | users, addresses, products, variants, categories, carts, orders, order_items, payments, inventory, reviews, coupons | Price snapshot on order lines; inventory reservation and overselling prevention; order state machine; category hierarchy; search; flash-sale hot rows; product-attribute modeling (JSON vs EAV) |
| **Banking** | customers, accounts, transactions/ledger entries, branches, beneficiaries, cards | Double-entry ledger; atomic transfers; deadlock-free ordering; idempotent transfers; audit/immutability; balance derivation vs stored balance; regulatory retention; strict serializable needs |
| **Payment system** | merchants, payment intents, charges, refunds, ledger, idempotency keys, webhooks, settlements | Idempotency keys; state machine; exactly-once effects with external gateways; reconciliation; outbox for webhooks; PCI scope reduction (tokenization) |
| **Food delivery** | customers, restaurants, menus, menu_items, orders, drivers, deliveries, payments, ratings | Order lifecycle states; driver assignment concurrency (`SKIP LOCKED`); geo queries; menu versioning/price changes; surge/hot restaurants; real-time location (not in the OLTP DB) |
| **Ride sharing** | riders, drivers, vehicles, trips, locations, fares, payments | Geospatial indexing (geohash/H3/PostGIS); high-frequency location writes (cache/stream, not row updates); matching concurrency; trip state machine; fare computation history; sharding by city/region |
| **Social media** | users, posts, comments, likes, follows, messages, notifications | Follower graph (M:N self-relation); feed generation (fan-out on write vs read); like counters (denormalized, sharded); celebrity hot keys; cursor pagination; soft deletes; sharding by user |
| **Booking system** | users, resources (rooms/seats/slots), availability, reservations, payments, cancellations | Double-booking prevention (exclusion constraints / unique slot rows / `FOR UPDATE`); holds with expiry; time-range overlap queries; time zones; waitlists; cancellation policy history |
| **Library** | books, copies, authors, members, loans, reservations, fines | Book vs copy separation; M:N books–authors; loan state and due dates; fine calculation; availability queries |
| **Inventory / warehouse** | products, SKUs, warehouses, stock levels, stock movements, purchase orders, suppliers | Movement ledger vs mutable stock count; reservations; concurrent decrement with non-negative check; batch/lot tracking; reconciliation |

## 46.3 Evaluation Rubric (self-grade each design)
- Correct entities/relationships and keys? Constraints enforce invariants in the DB?
- Normalized with justified denormalization? Money/time/ID types correct?
- Indexes tied to concrete queries? Write-path cost considered?
- Concurrency anomalies named and prevented? Transaction boundaries explicit?
- Growth plan: partition/shard key and cross-shard consequences?
- Audit, retention, security, backup considered?
- Can you explain trade-offs and alternatives, not just one answer?

### What You Should Be Able to Do
- Take a 3-sentence prompt ("design the database for a ride-sharing app"), ask clarifying questions, and produce ER diagram, DDL, indexes, key queries, and scaling story in 30–40 minutes.
- Defend every decision with a trade-off.

---

# 47. SQL Interview Pattern Catalog 🔴

> **Level:** Core → Advanced. Practice each pattern in **at least two different ways** (e.g., window function and subquery/join), on a real database, and compare plans.

## 47.1 Pattern Map

| # | Pattern | Primary technique(s) | Variations to practice |
|---|---|---|---|
| 1 | Second highest salary | `MAX` with subquery; `DENSE_RANK`; `LIMIT/OFFSET` | Return NULL when none; per department; handling ties |
| 2 | Nth highest salary | `DENSE_RANK() = N`; correlated count; `OFFSET` | Function/procedure parameter version |
| 3 | Duplicate records | `GROUP BY ... HAVING COUNT(*) > 1` | Duplicates across multiple columns; show full duplicate rows |
| 4 | Delete duplicates | `ROW_NUMBER()` + delete; self-join delete; CTE delete (PG/SQL Server) | Keep latest vs earliest; MySQL derived-table restriction |
| 5 | Employee earns more than manager | Self join | Earns more than department average (subquery/window) |
| 6 | Top N per group | `ROW_NUMBER`/`RANK` partitioned; `LATERAL`/`APPLY` | Top 3 products per category; ties inclusive |
| 7 | Department-wise maximum | `GROUP BY`; join back; window `MAX() OVER` | Employee(s) with max salary per dept |
| 8 | Running total | `SUM() OVER (ORDER BY ... ROWS ...)` | Per customer; reset per month; correct tie handling |
| 9 | Moving average | `AVG() OVER (ROWS BETWEEN n PRECEDING AND CURRENT ROW)` | Date-based window with `RANGE`; missing days |
| 10 | Ranking | `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `NTILE`, `PERCENT_RANK` | Leaderboards; percentile cut-offs |
| 11 | Consecutive dates / sequences | `LAG/LEAD`; date − `ROW_NUMBER` | Consecutive numbers; streaks |
| 12 | Gaps and islands | Difference-of-row-numbers grouping; `LAG` flag + cumulative sum | Sessionization; contiguous ranges; missing ranges |
| 13 | Missing records | Calendar/number table (`generate_series`, recursive CTE) `LEFT JOIN` | Missing IDs, missing dates, missing months |
| 14 | Customers with no orders | `NOT EXISTS`; `LEFT JOIN ... IS NULL` | Customers with no orders in last 30 days |
| 15 | Products never ordered | Anti-join | Products not ordered in a given period |
| 16 | Monthly / yearly aggregation | `DATE_TRUNC`/`EXTRACT` + `GROUP BY` | Month-over-month growth with `LAG`; YoY; fill empty months |
| 17 | Date-range problems | Half-open intervals; overlap test `a.start < b.end AND b.start < a.end` | Overlapping bookings; active-on-date; business days |
| 18 | Consecutive login days | Islands on distinct dates; `HAVING COUNT(*) >= n` | Longest streak; current streak; users active 3+ days in a row |
| 19 | Retention / cohort | First-activity CTE → join activity → period offset → pivot | D1/D7/D30 retention; weekly cohorts; churn |
| 20 | Pivot / unpivot | Conditional aggregation; `UNION ALL`/`CROSS APPLY`/`UNNEST` | Dynamic pivot (needs dynamic SQL) |
| 21 | Conditional aggregation | `SUM(CASE ...)`, `COUNT(*) FILTER` | Ratios/percentages; multi-metric single pass |
| 22 | Complex joins | Multi-table joins; join to aggregated subquery; fan-out control | Many-to-many reports; joins with inequality conditions |
| 23 | Recursive hierarchy | Recursive CTE | All descendants; depth/path; ancestors; cycle protection; category breadcrumbs |
| 24 | Median / percentiles | `PERCENTILE_CONT`; row-number pairing | Median per group |
| 25 | Running distinct / first-time events | `MIN` per user then count; window `ROW_NUMBER = 1` | New vs returning customers per month |
| 26 | Top-K by aggregate | `GROUP BY` + `ORDER BY` + `LIMIT`; rank on aggregate | Ties; customers contributing 80% of revenue (cumulative share) |
| 27 | Relational division ("for all") | Double `NOT EXISTS`; `HAVING COUNT(DISTINCT) = total` | Students who took all required courses |
| 28 | Set comparison | `INTERSECT`, `EXCEPT`, anti-joins | Users in A but not B; symmetric difference |
| 29 | Deduplicated "latest row per entity" | `ROW_NUMBER() ... DESC = 1`; `DISTINCT ON` (PG); `MAX` join | Latest status per order; SCD current rows |
| 30 | Pagination | Keyset pagination | Bidirectional paging; stable ordering |
| 31 | Self-join pairs / comparisons | Self join with `a.id < b.id` | Friend-of-friend; same-department pairs |
| 32 | Data cleaning in SQL | `COALESCE`, `NULLIF`, `TRIM`, regex, `CASE` | Standardizing phones/emails; flagging invalid rows |

## 47.2 Canonical Solutions to Know by Heart (PostgreSQL-flavored; adapt dialect)

**Nth highest salary (handles ties via DENSE_RANK)**
```sql
SELECT DISTINCT salary
FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
  FROM employees
) t
WHERE rnk = :n;
```

**Second highest without window functions (returns NULL if absent)**
```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

**Delete duplicates, keep the lowest id**
```sql
DELETE FROM users
WHERE id IN (
  SELECT id FROM (
    SELECT id, ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) AS rn
    FROM users
  ) x
  WHERE rn > 1
);
```

**Top 3 per group**
```sql
SELECT *
FROM (
  SELECT e.*, ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC, id) AS rn
  FROM employees e
) t
WHERE rn <= 3;
```

**Running total and 7-row moving average**
```sql
SELECT order_date,
       SUM(amount) OVER (ORDER BY order_date, id ROWS UNBOUNDED PRECEDING)           AS running_total,
       AVG(amount) OVER (ORDER BY order_date, id ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS moving_avg_7
FROM orders;
```

**Gaps and islands — consecutive login days (PG date arithmetic)**
```sql
WITH d AS (
  SELECT DISTINCT user_id, login_date::date AS d FROM logins
), g AS (
  SELECT user_id, d,
         d - (ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY d))::int AS grp
  FROM d
)
SELECT user_id, MIN(d) AS streak_start, MAX(d) AS streak_end, COUNT(*) AS streak_days
FROM g
GROUP BY user_id, grp
HAVING COUNT(*) >= 3;
```

**Customers with no orders (anti-join)**
```sql
SELECT c.*
FROM customers c
WHERE NOT EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
```

**Month-over-month growth**
```sql
WITH m AS (
  SELECT DATE_TRUNC('month', order_date) AS month, SUM(amount) AS revenue
  FROM orders GROUP BY 1
)
SELECT month, revenue,
       revenue - LAG(revenue) OVER (ORDER BY month) AS delta,
       ROUND(100.0 * (revenue - LAG(revenue) OVER (ORDER BY month))
             / NULLIF(LAG(revenue) OVER (ORDER BY month), 0), 2) AS pct_growth
FROM m;
```

**Cohort retention skeleton**
```sql
WITH first_seen AS (
  SELECT user_id, DATE_TRUNC('month', MIN(event_date)) AS cohort FROM events GROUP BY user_id
), activity AS (
  SELECT DISTINCT user_id, DATE_TRUNC('month', event_date) AS active_month FROM events
)
SELECT f.cohort,
       (EXTRACT(YEAR FROM a.active_month) - EXTRACT(YEAR FROM f.cohort)) * 12
     + (EXTRACT(MONTH FROM a.active_month) - EXTRACT(MONTH FROM f.cohort)) AS month_offset,
       COUNT(DISTINCT a.user_id) AS active_users
FROM first_seen f JOIN activity a USING (user_id)
GROUP BY 1, 2
ORDER BY 1, 2;
```

**Recursive hierarchy (all reports under manager :m)**
```sql
WITH RECURSIVE org AS (
  SELECT id, name, manager_id, 0 AS depth FROM employees WHERE id = :m
  UNION ALL
  SELECT e.id, e.name, e.manager_id, o.depth + 1
  FROM employees e JOIN org o ON e.manager_id = o.id
)
SELECT * FROM org;
```

**Keyset pagination**
```sql
SELECT id, created_at, title
FROM posts
WHERE (created_at, id) < (:last_created_at, :last_id)
ORDER BY created_at DESC, id DESC
LIMIT 20;
-- supporting index: CREATE INDEX ON posts (created_at DESC, id DESC);
```

**Relational division: students who took all required courses**
```sql
SELECT s.id
FROM students s
WHERE NOT EXISTS (
  SELECT 1 FROM required_courses rc
  WHERE NOT EXISTS (
    SELECT 1 FROM enrollments e WHERE e.student_id = s.id AND e.course_id = rc.course_id
  )
);
```

## 47.3 How to Practice
- Create a schema + seed script; write each solution **two ways**; run `EXPLAIN ANALYZE`; add the right index; re-measure.
- Always state assumptions: ties, NULLs, duplicates, empty groups, time zones.
- Verbalize the approach before coding (clarify → example → logic → edge cases → complexity/performance).

### What You Should Be Able to Do
- Solve any pattern above in under 10–15 minutes, in at least two ways, naming edge cases proactively.
- Choose the version that performs best at scale and say why.

---

# 48. Numerical and Paper Problem Catalog 🟠

> **Level:** Intermediate. Common in university exams (GATE-style), and in interviews when the interviewer wants to see internal-mechanics reasoning.

## 48.1 Problem Types (practice 10+ of each)

| Area | Problem types |
|---|---|
| **Relational algebra** | Translate English ↔ algebra ↔ SQL; division; expression-tree rewriting; result cardinality bounds of joins/unions |
| **FDs & keys** | Attribute closure; candidate keys; number of super keys; implied FDs; FD set equivalence; canonical cover |
| **Normalization** | Highest normal form; decomposition into 3NF/BCNF; lossless test; dependency-preservation test; synthesis algorithm; 4NF via MVD |
| **Schedules** | Count serial schedules/interleavings; conflict-serializability via precedence graph; view-serializability; recoverable/cascadeless/strict classification |
| **Locking** | Lock-compatibility reasoning; legal under 2PL/strict 2PL?; granularity (IS/IX/S/SIX/X) requests; lock-point order |
| **Deadlock** | Build wait-for graph; detect cycle; choose victim; apply wait-die vs wound-wait with timestamps; timestamp-ordering accept/reject |
| **Recovery** | Given log + checkpoint + crash: redo/undo lists; ARIES analysis/redo/undo; WAL rule violations |
| **Storage / I/O** | Blocking factor; number of blocks; file scan/binary search cost; variable-length record sizing |
| **Indexing** | Dense/sparse index size and block accesses; multilevel index levels; B+ tree order, height, capacity |
| **B+ tree** | Insert/delete sequences with splits/merges/redistribution; tree after each step |
| **Hashing** | Extendible hashing inserts with directory growth; linear hashing split sequence; static hashing overflow |
| **Join cost** | NLJ, BNLJ, INLJ, hash, sort-merge block-transfer + seek costs |
| **Sorting** | External merge sort runs and passes; memory vs passes |
| **Query cost & selectivity** | Estimate result rows from selectivity; choose between index and scan; plan comparison |
| **Distributed** | Quorum `R+W>N` analysis; 2PC state/failure tables; CAP classification; consistent hashing placement |
| **Capacity** | Table/index size estimate; rows per page; growth over time; sizing shards and partitions |

## 48.2 Formula Sheet
```text
Blocking factor        bf = ⌊B / R⌋               (B = block size, R = record size)
Blocks in file         b  = ⌈r / bf⌉              (r = number of records)
Linear scan cost       b block reads (≈ b/2 average for unique-key equality)
Binary search (sorted) ⌈log2 b⌉ block reads
Dense index entries    = r ; Sparse index entries = number of data blocks
Index blocking factor  bfi = ⌊B / (K + P)⌋        (K = key size, P = pointer size)
Multilevel index levels  x = ⌈log_bfi (first-level blocks)⌉ + 1
B+ tree order p (internal): p·P + (p−1)·K ≤ B
B+ tree height          h ≈ ⌈log_fanout(N)⌉  ; lookup cost = h (+1 for data block)
Max keys in height-h tree ≈ fanout^h × (keys per leaf)
Serial schedules        n!
Interleavings of T1..Tk with ni ops   (Σni)! / Π(ni!)
NLJ cost (blocks)       b_r + n_r · b_s
BNLJ cost               b_r + ⌈b_r / (M−2)⌉ · b_s
INLJ cost               b_r + n_r · c
Hash join (partitioned) 3(b_r + b_s) (+ build in-memory if fits: b_r + b_s)
Sort-merge join         sort cost(R) + sort cost(S) + b_r + b_s
External sort passes    1 + ⌈log_{M−1}(⌈b / M⌉)⌉ ; total I/O ≈ 2b · passes
Selectivity (equality)  1 / V(A,R) ; conjunction (independent) = Π selectivities
Join result size        n_r · n_s / max(V(A,R), V(A,S))
Quorum condition        R + W > N  (read/write overlap)
Availability of N nodes tolerating f crashes via majority: N ≥ 2f + 1
Pool sizing intuition   connections ≈ (core_count × 2) + effective_spindle_count (starting point; measure!)
```

## 48.3 Method Checklists
- **Attribute closure:** start with X; repeatedly add RHS of any FD whose LHS ⊆ current set; stop when unchanged.
- **Conflict serializability:** list conflicts per item in order → edges Ti→Tj → cycle check → topological order.
- **B+ tree insertion:** insert in leaf → if overflow, split (leaf: copy-up middle key; internal: push-up) → recurse to root.
- **Wait-die / wound-wait:** compare timestamps of requester and holder; older = smaller timestamp; apply rule; restarted transaction keeps its original timestamp.
- **Crash recovery:** find last checkpoint → determine committed vs uncommitted transactions → redo committed updates after checkpoint, undo uncommitted in reverse.

### What You Should Be Able to Do
- Solve each problem type on paper correctly and quickly, showing intermediate steps.
- Cross-check a paper answer against a real engine's behavior (e.g., `EXPLAIN`, lock views).

---

# 49. Interview Question Bank 🔴

> **Level:** All. De-duplicated and organized by theme; each ✱ question is a "senior differentiator". For each, practice a 1-minute answer and a deep-dive answer.

## 49.1 Fundamentals and Modeling
1. DBMS vs RDBMS vs file system? What problems does a DBMS solve?
2. Three-schema architecture and data independence — give examples.
3. Super key vs candidate key vs primary key vs alternate key vs foreign key?
4. Natural vs surrogate key? UUID vs auto-increment — trade-offs?
5. Entity integrity vs referential integrity? What does `ON DELETE CASCADE` risk?
6. Cardinality vs participation; weak entity; specialization/generalization; mapping ER to tables.
7. What is NULL? Explain three-valued logic and the `NOT IN` trap.
8. ✱ Why is a SQL table a bag while a relation is a set?

## 49.2 SQL
9. `DELETE` vs `TRUNCATE` vs `DROP`?
10. `WHERE` vs `HAVING`? Logical order of query execution?
11. `UNION` vs `UNION ALL`; `INTERSECT`/`EXCEPT`?
12. All join types; `ON` vs `WHERE` in outer joins; self join; anti-join patterns.
13. `IN` vs `EXISTS` vs join; correlated vs uncorrelated subquery.
14. CTE vs subquery vs view vs temp table; recursive CTE use cases.
15. `ROW_NUMBER` vs `RANK` vs `DENSE_RANK`; `LAG/LEAD`; default window frame pitfalls.
16. How do you find the Nth highest salary / duplicates / latest row per group / consecutive days?
17. `COUNT(*)` vs `COUNT(col)` vs `COUNT(DISTINCT col)`?
18. What is a view? Updatable? Materialized view vs view?
19. Stored procedure vs function vs trigger — when to use or avoid?
20. How do you implement upsert? What are its concurrency issues?
21. OFFSET pagination vs keyset pagination?
22. ✱ How does the query planner treat a CTE in PostgreSQL vs SQL Server?

## 49.3 Design and Normalization
23. What is normalization? Explain 1NF, 2NF, 3NF, BCNF with examples.
24. 3NF vs BCNF; when is BCNF not dependency-preserving?
25. What is a functional dependency? How do you compute closure and candidate keys?
26. Lossless decomposition and dependency preservation?
27. When and how do you denormalize? Consistency strategy?
28. Soft delete vs hard delete; audit tables; temporal tables?
29. ✱ Design a schema for e-commerce / bank / ride-sharing / booking (see §46).

## 49.4 Transactions and Concurrency
30. What is a transaction? Explain ACID with a bank transfer.
31. Isolation levels and the anomalies each prevents; defaults of PG/MySQL/SQL Server?
32. Dirty read vs non-repeatable read vs phantom read vs lost update vs write skew.
33. Conflict serializability and precedence graphs; view serializability?
34. Recoverable, cascadeless, strict schedules?
35. 2PL, strict 2PL, rigorous 2PL — differences and guarantees?
36. Shared/exclusive/intention locks; lock escalation; row vs table locks.
37. What is a deadlock? Conditions, detection, prevention (wait-die, wound-wait), handling?
38. Optimistic vs pessimistic concurrency; how do you implement each?
39. What is MVCC? How do readers avoid blocking writers? What's the cost (bloat/vacuum)?
40. ✱ Snapshot isolation vs serializable — explain write skew with an example.
41. ✱ How do you prevent overselling inventory under concurrent requests?
42. ✱ `SELECT ... FOR UPDATE SKIP LOCKED` — what is it for?
43. What happens to a transaction when the application crashes mid-way?

## 49.5 Recovery and Storage
44. What is WAL and why is it needed? Steal/no-force?
45. Undo vs redo; checkpoints; what happens on crash recovery?
46. ARIES phases; shadow paging vs WAL?
47. Pages, slotted pages, heap vs clustered organization; buffer pool and eviction?

## 49.6 Indexing and Query Performance
48. How does an index work? Why B+ trees? B-tree vs B+ tree?
49. Clustered vs non-clustered; primary vs secondary; dense vs sparse; covering index; composite index column order.
50. Hash index vs B+ tree; extendible/linear hashing; LSM vs B+ tree.
51. Why might the database ignore an index? What is sargability?
52. Index scan vs index seek vs table scan vs index-only scan?
53. How does the optimizer pick a plan? Statistics, cardinality estimation, join ordering?
54. Nested-loop vs hash vs merge join — when each?
55. How do you read an execution plan (`EXPLAIN ANALYZE`)?
56. ✱ A production query is slow — walk through your investigation (§53).
57. What is the N+1 problem and how do you fix it?
58. How would you investigate high DB CPU / lock contention / connection pool exhaustion?
59. Why is `OFFSET 1000000` slow? Why can `COUNT(*)` be slow?
60. Do indexes always speed things up? What are their costs?

## 49.7 Scaling and Distributed Systems
61. Replication types (sync/async), replication lag, failover, split brain?
62. Read-your-writes with read replicas — how do you achieve it?
63. Partitioning vs sharding vs replication — what problem does each solve?
64. How do you choose a shard key? What are hot shards? How do you reshard?
65. Cross-shard joins and transactions — options?
66. CAP and PACELC — explain precisely, with examples.
67. Strong vs eventual consistency; quorum reads/writes; causal consistency?
68. 2PC — how does it work, and what are its failure modes? Saga alternative?
69. ✱ Raft in a few minutes — leader election and log replication.
70. NoSQL types, when to choose each; SQL vs NoSQL; data modeling for DynamoDB/Cassandra/MongoDB?
71. OLTP vs OLAP; star vs snowflake; ETL vs ELT; row vs column store; SCD types?

## 49.8 Security, Operations, Backend
72. How do you prevent SQL injection? Why are prepared statements safe?
73. Authentication vs authorization; least privilege; row-level security?
74. Encryption at rest vs in transit; how do you store passwords?
75. Backup types; PITR; RPO vs RTO; how do you verify backups?
76. How do you perform a zero-downtime schema migration?
77. What is connection pooling? How do you size a pool? PgBouncer modes?
78. ORM pros and cons; lazy vs eager loading; change tracking; unit of work; when to use raw SQL?
79. What is the outbox pattern? CDC? CQRS/event sourcing trade-offs?
80. How do you implement idempotency for a payment API?
81. ✱ Compare PostgreSQL, MySQL, and SQL Server on isolation, MVCC, indexing and replication.

---

# 50. Comparison Cheat Sheet 🔴

| Comparison | Priority | Key distinction to articulate |
|---|---|---|
| DBMS vs File System | 🔴 | Integrity, concurrency, recovery, query ability |
| DBMS vs RDBMS | 🔴 | Relational model, SQL, constraints, keys |
| Primary key vs Unique key | 🔴 | One per table, NOT NULL vs multiple, NULL rules vary |
| Candidate key vs Super key | 🔴 | Minimality |
| Natural vs Surrogate key | 🔴 | Meaning/stability vs simplicity/size |
| DELETE vs TRUNCATE vs DROP | 🔴 | Rows vs all rows vs object; logging; rollback; locks |
| WHERE vs HAVING | 🔴 | Row filter before grouping vs group filter |
| UNION vs UNION ALL | 🔴 | Deduplication and cost |
| INNER vs LEFT/RIGHT/FULL JOIN | 🔴 | Unmatched row handling |
| `IN` vs `EXISTS` vs `JOIN` | 🟠 | Semantics, NULL behavior, plans |
| `NOT IN` vs `NOT EXISTS` vs `LEFT JOIN IS NULL` | 🔴 | NULL trap |
| CTE vs Subquery vs Temp table | 🟠 | Readability, materialization, statistics |
| View vs Materialized view | 🟠 | Virtual vs stored; freshness |
| Procedure vs Function | 🟠 | Side effects, return, usage in SQL |
| Trigger vs Constraint vs App logic | 🟠 | Declarative vs procedural, visibility |
| `ROW_NUMBER` vs `RANK` vs `DENSE_RANK` | 🔴 | Tie handling |
| `ROWS` vs `RANGE` frame | 🟠 | Physical rows vs value peers |
| 2NF vs 3NF vs BCNF | 🔴 | Partial vs transitive vs determinant-is-key |
| 3NF vs BCNF | 🟠 | Dependency preservation |
| Normalization vs Denormalization | 🔴 | Integrity vs read performance |
| Serial vs serializable schedule | 🟠 | Order vs equivalence |
| Conflict vs View serializability | 🟡 | Test complexity and coverage |
| Recoverable vs Cascadeless vs Strict | 🟠 | Rollback propagation |
| Shared vs Exclusive vs Intention locks | 🟠 | Compatibility, granularity |
| 2PL vs Strict 2PL vs Rigorous 2PL | 🟠 | When locks release |
| Deadlock prevention vs detection vs avoidance | 🟠 | Wait-die/wound-wait vs wait-for graph |
| Pessimistic vs Optimistic concurrency | 🟠 | Locks vs validation/retry |
| 2PL vs Timestamp ordering vs MVCC | 🟡 | Blocking vs abort; readers/writers |
| Read Committed vs Repeatable Read vs Serializable | 🔴 | Anomalies, engine behavior |
| Snapshot isolation vs Serializable | 🟠 | Write skew |
| Deferred vs Immediate update recovery | 🟡 | When DB changes happen |
| WAL vs Shadow paging | 🟡 | Logging vs copy-on-write |
| Heap vs Clustered storage | 🟠 | Row location and secondary index cost |
| Primary vs Secondary index | 🟠 | Ordering key vs other |
| Clustered vs Non-clustered index | 🔴 | Physical order, count, lookups |
| Dense vs Sparse index | 🟡 | Entry per record vs per block |
| Composite vs Covering index | 🟠 | Multiple columns vs index-only access |
| B-tree vs B+ tree | 🔴 | Data location, range scans, fan-out |
| B+ tree vs Hash index | 🟠 | Range/order vs equality |
| B+ tree vs LSM tree | 🟡 | Read vs write optimization |
| Table scan vs Index scan vs Index seek | 🔴 | Access path cost |
| Nested loop vs Hash vs Merge join | 🟠 | Input size, sortedness, memory |
| Heuristic vs Cost-based optimization | 🟠 | Rules vs statistics |
| Estimated vs Actual plan | 🟠 | Optimizer prediction vs reality |
| `OFFSET` vs Keyset pagination | 🔴 | O(offset) cost, stability |
| Authentication vs Authorization | 🟠 | Who vs what |
| Encryption at rest vs in transit | 🟠 | Storage vs network |
| Full vs Incremental vs Differential backup | 🟠 | Scope and restore chain |
| Logical vs Physical backup | 🟡 | Portability vs speed |
| Backup vs Replication | 🔴 | Protects against corruption/human error vs availability |
| RPO vs RTO | 🟠 | Data loss vs downtime |
| Sync vs Async replication | 🟠 | Durability vs latency |
| Replication vs Partitioning vs Sharding | 🔴 | Copies vs split within DB vs split across DBs |
| Partitioning vs Sharding | 🔴 | Single node vs multi-node |
| Vertical vs Horizontal scaling | 🟠 | Bigger machine vs more machines |
| Strong vs Eventual consistency | 🟠 | Latency/availability trade-off |
| ACID "C" vs CAP "C" | 🟠 | Invariants vs linearizability |
| 2PC vs Saga | 🟠 | Atomic blocking vs compensation |
| SQL vs NoSQL vs NewSQL | 🔴 | Model, scale, consistency |
| OLTP vs OLAP | 🟠 | Workload shape |
| Star vs Snowflake schema | 🟡 | Denormalized vs normalized dimensions |
| ETL vs ELT | 🟡 | Transform before vs after load |
| Row store vs Column store | 🟠 | Point access vs analytic scans |
| Lazy vs Eager vs Explicit loading | 🟠 | When related data loads |
| ORM vs Raw SQL vs Micro-ORM | 🟠 | Productivity vs control |
| Soft delete vs Hard delete | 🟠 | Recoverability vs integrity/privacy |
| UUID vs Auto-increment | 🟠 | Distribution/security vs locality/size |

---

# PART XI — PLANNING AND TRACKING

---

# 51. Priority Tiers

## 🔴 Tier 1 — Critical (must master for most SDE interviews)
- **Fundamentals:** DBMS vs RDBMS vs file system; relational model; keys; constraints; NULL and three-valued logic
- **SQL:** joins (all types, `ON` vs `WHERE`), `GROUP BY/HAVING`, conditional aggregation, subqueries (`IN/EXISTS/NOT IN` NULL trap), CTEs, recursive CTEs, set operations, **window functions**, `CASE`, DML including upsert, pagination (keyset vs offset)
- **Design:** ER modeling, cardinality, ER→tables, FDs, attribute closure, candidate keys, 1NF–BCNF, denormalization, design method (§46)
- **Transactions:** ACID, anomalies, **isolation levels and real engine behavior**, locks, 2PL, deadlocks, optimistic vs pessimistic control, MVCC concept
- **Indexing:** clustered vs non-clustered, composite/covering, B+ tree, selectivity, sargability, index trade-offs
- **Performance:** execution plans (`EXPLAIN ANALYZE`), scan vs seek, N+1, connection pooling, systematic slow-query investigation
- **Security:** SQL injection and parameterized queries, least privilege
- **Backend:** transactions from application code, idempotency, retries
- **Interview practice:** SQL pattern catalog (§47), design case studies (§46)

## 🟠 Tier 2 — High (strongly recommended)
- Relational algebra (incl. division); schedules, serializability, recoverability; multiple granularity locks; timestamp ordering and OCC
- WAL, undo/redo, checkpoints, crash recovery; storage pages, buffer pool, heap vs clustered organization
- Hashing (static/extendible/linear); join algorithms and cost; query optimization, statistics, cardinality estimation, join ordering
- Views, materialized views, stored procedures, triggers, sequences; JSON; full-text basics; soft delete, audit, temporal data
- Backup/restore, PITR, RPO/RTO; replication, lag, failover, read/write splitting; partitioning and sharding; CAP/PACELC, consistency models, 2PC and sagas
- NoSQL types and modeling; OLTP vs OLAP; star schema
- ORM concepts (EF Core), migrations, outbox, CDC, caching strategies; PostgreSQL/SQL Server/MySQL differences; database observability

## 🟡 Tier 3 — Medium (useful for deeper interviews)
- Relational calculus; 4NF/5NF, MVDs/JDs, tableau chase; view serializability; shadow paging
- Advanced grouping (`ROLLUP/CUBE`); lateral joins; recursive CTE optimization
- LSM trees; bitmap/GIN/GiST/BRIN indexes; hybrid hash join; bushy join trees
- Raft/Paxos basics; fencing tokens and distributed locks; NewSQL internals; vector/time-series/search stores
- Data warehousing details: SCD types, conformed dimensions, columnar engines; CQRS/event sourcing

## 🟢 Tier 4 — Advanced / Optional (senior or specialist)
- ARIES in depth; B-tree latching (crabbing, B-link trees); Bw-tree
- Optimizer internals (Cascades/Volcano frameworks); vectorized execution; adaptive query execution
- Advanced MVCC garbage collection and wraparound; SSI internals
- Distributed transaction protocols (Percolator, Calvin, Spanner TrueTime); CRDTs; Paxos variants
- Geospatial indexing, graph query optimization, DBMS implementation projects (build a toy B+ tree / buffer pool / WAL)

---

# 52. Final Mastery Checklist

> Tick an item only when you can (a) define it, (b) explain how it works, and (c) apply it to a concrete problem.

## Foundations
- [ ] Data/information, database, DBMS, RDBMS, DBMS vs file system, DBMS responsibilities, users/DBA
- [ ] Three-schema architecture, logical/physical data independence, DBMS components, catalog/metadata
- [ ] Data models and when to use each; polyglot persistence

## Relational Model and Modeling
- [ ] Relation/tuple/attribute/domain/degree/cardinality; NULL and three-valued logic
- [ ] Super, candidate, primary, alternate, foreign, composite, natural, surrogate keys
- [ ] Domain, entity, referential integrity; `CHECK/UNIQUE/DEFAULT/NOT NULL`; referential actions; deferred constraints
- [ ] ER: entities, attributes, relationships, cardinality, participation, weak entities
- [ ] EER: specialization, generalization, aggregation, disjoint/overlap, total/partial
- [ ] ER-to-relational mapping for all constructs
- [ ] Relational algebra (σ π ∪ − × ρ ⋈ ÷), set vs bag semantics; TRC/DRC awareness

## SQL
- [ ] DDL, DML, DCL, TCL; data types; type conversion; identity/sequence/UUID
- [ ] `SELECT/INSERT/UPDATE/DELETE/MERGE/UPSERT/RETURNING`
- [ ] Logical query processing order; `WHERE/ORDER BY/GROUP BY/HAVING/DISTINCT`
- [ ] `CASE`, `COALESCE/NULLIF`, aggregate/string/date/numeric/NULL functions
- [ ] All join types, self joins, anti/semi-joins, `LATERAL/APPLY`, fan-out
- [ ] Subqueries (scalar/correlated), `EXISTS/IN/ANY/ALL`, `NOT IN` NULL trap
- [ ] CTEs, recursive CTEs, `UNION/UNION ALL/INTERSECT/EXCEPT`
- [ ] Window functions: ranking, `LAG/LEAD`, running totals, frames, default-frame trap
- [ ] Conditional aggregation, pivot/unpivot, `ROLLUP/CUBE/GROUPING SETS`
- [ ] Views, materialized views, procedures, functions, triggers, temp tables
- [ ] JSON, full-text search, temporal tables, soft delete, keyset pagination
- [ ] SQL pattern catalog (§47): all 32 patterns solved two ways

## Database Design
- [ ] FDs, Armstrong's axioms, closure, candidate-key derivation, canonical cover, FD equivalence
- [ ] 1NF, 2NF, 3NF, BCNF, 4NF, 5NF; MVD/JD
- [ ] Lossless decomposition, dependency preservation, 3NF synthesis, BCNF decomposition
- [ ] Denormalization with consistency strategy
- [ ] Schema design patterns, anti-patterns, multi-tenancy, audit, history
- [ ] 20-step design method applied to 9 case studies

## Transactions and Concurrency
- [ ] Transaction states; ACID mechanisms; commit/rollback/savepoint
- [ ] Schedules, serial/serializable, conflict and view serializability, precedence graph
- [ ] Recoverable, cascadeless, strict schedules
- [ ] S/X/U locks, compatibility, 2PL variants, intention locks, granularity, next-key/gap locks
- [ ] Anomalies: dirty, non-repeatable, phantom, lost update, write skew
- [ ] All four isolation levels + PG/MySQL/SQL Server real behavior
- [ ] Deadlock: conditions, wait-for graph, wait-die, wound-wait, victim selection, app handling
- [ ] Timestamp ordering, OCC, MVCC, snapshot isolation, SSI
- [ ] `FOR UPDATE`, `SKIP LOCKED`, advisory locks, optimistic version columns

## Recovery
- [ ] Failure types; WAL; steal/no-force; undo/redo; deferred/immediate update; checkpoints; shadow paging; ARIES; crash recovery walkthrough

## Storage and Indexing
- [ ] Storage hierarchy; HDD vs SSD; pages/blocks/records; slotted pages; fixed/variable records
- [ ] Heap, sorted, hash, clustered organization; buffer manager and replacement
- [ ] Primary, secondary, clustered, non-clustered, dense, sparse, composite, covering, unique, partial, expression indexes
- [ ] Leftmost-prefix and column-order rules; selectivity; cardinality; fragmentation; maintenance
- [ ] B-tree and B+ tree operations, height/capacity numericals
- [ ] Static, extendible, linear hashing; LSM, GIN, GiST, BRIN, bitmap (awareness)

## Query Engine
- [ ] Parse → bind → rewrite → optimize → execute pipeline
- [ ] Access paths; sort/aggregate/distinct operators; pipeline breakers
- [ ] NLJ, BNLJ, INLJ, hash join, sort-merge join and their costs
- [ ] Heuristic vs cost-based optimization; statistics/histograms; cardinality estimation; join ordering
- [ ] Sargability; parameter sniffing; plan regression
- [ ] `EXPLAIN` / `EXPLAIN ANALYZE` / actual plans; estimated vs actual rows

## Performance and Observability
- [ ] Systematic slow-query workflow; slow query logs; `pg_stat_statements`/Query Store
- [ ] N+1; large OFFSET; connection pool exhaustion; lock contention; CPU/memory/disk/network bottlenecks
- [ ] Metrics, monitoring, alerting; caching strategies

## Security
- [ ] Authentication, authorization, roles, `GRANT/REVOKE`, least privilege, RLS
- [ ] SQL injection (all types) and defenses; ORM raw-SQL risks
- [ ] Encryption at rest/in transit; key and secrets management; password hashing; masking; auditing; compliance awareness

## Operations
- [ ] Backup types, PITR, RPO/RTO, verification, retention, DR patterns
- [ ] Replication models, lag, failover, split brain, conflict resolution, read/write splitting
- [ ] Partitioning types and pruning; sharding, shard-key choice, hot shards, resharding, cross-shard queries/transactions

## Distributed and Alternative Systems
- [ ] CAP, PACELC, consistency models, quorum math, clocks
- [ ] 2PC (with failure cases), sagas, Raft/Paxos basics, distributed locks and fencing
- [ ] Key-value, document, wide-column, graph; access-pattern modeling; partition/clustering keys
- [ ] NewSQL; search/time-series/vector/cache stores; choosing stores
- [ ] OLTP vs OLAP, star/snowflake, fact/dimension/grain, SCD, ETL/ELT, row vs column store

## Backend Engineering
- [ ] Connection strings, pooling, timeouts, PgBouncer-style poolers
- [ ] Prepared statements; app-level transactions; retries; idempotency keys
- [ ] ORM: unit of work, identity map, change tracking, lazy/eager/explicit loading, N+1, cartesian explosion, generated SQL, concurrency tokens
- [ ] Migrations, zero-downtime schema changes (expand/contract), schema versioning
- [ ] CDC, outbox/inbox, CQRS, event sourcing trade-offs
- [ ] PostgreSQL vs SQL Server vs MySQL differences (§45.4)

## Practice
- [ ] 10+ paper problems of each type in §48 solved
- [ ] 9 design case studies completed with rubric (§46.3)
- [ ] 81 interview questions answerable at 1-minute and deep-dive levels (§49)
- [ ] Three full "mock DB interviews" completed (SQL + design + internals)

---

# 53. Recommended Learning Sequence

## 53.1 Dependency-Ordered Path
```text
PHASE 1 — FOUNDATIONS & MODELING
Fundamentals → Architecture → Data Models → Relational Model → Keys & Constraints
→ ER/EER Modeling → Relational Algebra
        ↓
PHASE 2 — SQL (start practicing immediately; continue throughout)
SQL Foundations/DDL/DML → Querying → Joins → Aggregation → Subqueries/CTEs/Set Ops
→ Window Functions → Views/Procedures/Triggers → Modern SQL (JSON, pagination, temporal)
        ↓
PHASE 3 — DESIGN THEORY
Functional Dependencies → Normalization & Decomposition → Practical Schema Patterns
        ↓
PHASE 4 — TRANSACTIONS & CONCURRENCY
Transactions/ACID → Schedules & Serializability → Locking → Isolation Levels & Anomalies
→ Deadlocks → Timestamp/OCC/MVCC → Recovery & Logging
        ↓
PHASE 5 — INTERNALS & PERFORMANCE
Storage → Indexing → B+ Trees → Hashing & Other Indexes → Query Processing & Join Algorithms
→ Query Optimization → Execution Plans → Performance & Observability
        ↓
PHASE 6 — OPERATIONS & SCALE
Security → Backup/DR → Replication/HA → Partitioning & Sharding
        ↓
PHASE 7 — DISTRIBUTED & ALTERNATIVES
Distributed Databases (CAP, consistency, 2PC, Raft) → NoSQL → NewSQL/Specialized Stores
→ OLTP/OLAP/Data Warehousing
        ↓
PHASE 8 — BACKEND ENGINEERING
Application Integration → ORM/EF Core → Data Evolution (migrations, CDC, outbox, CQRS)
→ PostgreSQL/SQL Server/MySQL specifics
        ↓
PHASE 9 — INTERVIEW CONVERSION
Design Method & Case Studies → SQL Pattern Catalog → Paper Problems
→ Interview Question Bank → Comparison Cheat Sheet → Mock Interviews → Revision
```

**Why this order differs slightly from a "theory-first" order:** SQL is introduced right after the relational model and starts early, because practice compounds. Practical schema patterns come immediately after normalization (while it's fresh). Isolation levels come *before* deadlocks and MVCC, so the anomaly vocabulary exists when later mechanisms are explained. Security moves ahead of backup/replication since it is higher-yield in interviews. ORM/migrations/CDC come after distributed concepts because they depend on them (dual writes, eventual consistency).

## 53.2 Suggested Time Plan (flexible; ~2 h/day)

| Weeks | Focus | Output |
|---|---|---|
| 1–2 | Phase 1 + SQL basics through joins | Schema built from an ER diagram; 40 basic/intermediate queries |
| 3–4 | Rest of SQL (subqueries → window functions → modern SQL) | 40 advanced queries; patterns 1–15 solved |
| 5 | Design theory + schema patterns | 25 paper normalization problems; 2 designs |
| 6–7 | Transactions, concurrency, isolation, deadlocks, MVCC, recovery | Reproduce all anomalies in two sessions; 20 schedule/lock/log problems |
| 8–9 | Storage, indexing, B+ trees, join algorithms, optimization, plans, performance | 10 B+ tree problems; tune 10 slow queries with `EXPLAIN ANALYZE` |
| 10 | Security, backup, replication, partitioning, sharding | Role model + PITR walkthrough + shard-key essay |
| 11 | Distributed, NoSQL, OLAP | CAP/PACELC essay; DynamoDB/Cassandra model; star schema |
| 12 | Backend integration, ORM, migrations, vendors | N+1 fix, outbox implementation, zero-downtime migration plan |
| 13–14 | Design case studies, SQL pattern drilling, mock interviews, revision | All 9 case studies; patterns 16–32; 3 mock interviews |

## 53.3 Final Job-Preparation Goal — Three Levels of Understanding

For every major topic, reach all three:

**Level 1 — Definition.** *What is an index?* Give a precise definition.

**Level 2 — Internal mechanism.** *How does a B+ tree help the database find rows?* Explain pages, fan-out, height, leaf links, and cost.

**Level 3 — Practical engineering.** *A production query takes 10 seconds. What do you do?*

```text
Reproduce & measure (real parameters, real data volume)
   ↓
Get the ACTUAL execution plan (EXPLAIN (ANALYZE, BUFFERS))
   ↓
Compare estimated vs actual rows → stale stats / skew / correlation?
   ↓
Find the dominant node: scan? sort spill? bad join? key lookups loop?
   ↓
Check predicates: sargable? implicit conversion? function on column?
   ↓
Check indexes: missing / wrong column order / not covering / unused
   ↓
Check concurrency: waiting on locks? long transaction? blocking chain?
   ↓
Check resources: I/O, memory (work_mem/buffer pool), CPU, network, connection pool
   ↓
Check application: N+1? chatty? over-fetching? ORM-generated SQL?
   ↓
Fix (rewrite / index / stats / schema / caching) → re-measure → verify write impact → monitor
```

A strong candidate combines:

```text
Theory + SQL + Database Design + Transactions + Concurrency + Indexing
+ Query Optimization + Internals + Security + Scaling + Distributed Systems
+ Backend Integration + Practical Troubleshooting
```

The goal is not to memorize SQL syntax. It is to understand how databases **model data, store data, execute queries, maintain consistency, handle concurrency, recover from failures, and scale under real workloads** — and to be able to explain the trade-offs behind every choice.

---

# APPENDIX A — AUDIT REPORT (Gap Analysis of the Original Syllabus)

> The original file (60 sections, ~2,900 lines) was audited against: standard university DBMS curricula (Silberschatz/Korth, Elmasri/Navathe, Ramakrishnan/Gehrke), common SDE/backend interview expectations, SQL interview patterns, and production database engineering.

## A.1 Overall Verdict
The original was **strong on classic theory and SQL syntax lists** but **under-delivered on four fronts**: (1) practical backend engineering (idempotency, outbox, CDC, migrations, observability), (2) real-engine behavior (isolation levels differ materially across PG/MySQL/SQL Server), (3) problem-solving (numericals, SQL pattern catalog, no worked patterns or exit criteria), and (4) design methodology. Its content was mostly *topic names* with little guidance on depth.

## A.2 Missing Topics (added)
| Area | Added |
|---|---|
| Fundamentals | Characteristics of DB approach; disadvantages of DBMS; process/thread server models; deployment architectures (embedded, shared-nothing, managed/DBaaS) |
| Relational model | `IS DISTINCT FROM`; NULL in `UNIQUE`, `NOT IN`, joins, aggregates; bag vs set semantics |
| ER/EER | **Aggregation**; fan/chasm traps; (min,max) notation; notation systems |
| Relational theory | **Tuple and domain relational calculus**, Codd's theorem; semi/anti-joins; extended algebra; algebra equivalence rules |
| Constraints | Surrogate-key generation strategies; UUID v4 vs time-ordered; deferrable constraints; partial unique constraints; constraints as concurrency defense; named constraints |
| SQL | `RETURNING/OUTPUT`; bulk operations; DDL transactionality; online DDL; `LATERAL/APPLY`; `USING`; `FILTER`; conditional aggregation; pivot/unpivot; percentile functions; `ROWS/RANGE/GROUPS` + default-frame trap; named windows; sequences; table variables; cursors; `ON` vs `WHERE` semantics; join fan-out; date half-open ranges; `QUALIFY` |
| Modern SQL | **Keyset/cursor pagination**; JSON/JSONB indexing; full-text search; **temporal tables**; **soft delete**; audit tables; geospatial awareness; RLS |
| Design theory | Minimal/canonical cover; FD-set equivalence; **multivalued and join dependencies**; BCNF/3NF synthesis algorithms; tableau test; counting keys |
| Practical design | Hierarchy models (adjacency, path, nested set, closure); EAV; state machines; ledgers; multi-tenancy; anti-patterns |
| Concurrency | **Write skew, read skew**; **isolation × anomaly matrix with real-engine behavior**; update locks; next-key/gap locks; `SKIP LOCKED/NOWAIT`; advisory locks; Thomas write rule; snapshot isolation + SSI; optimistic version columns |
| Deadlocks | Coffman conditions; victim selection/starvation; engine error codes and diagnostics; livelock, lock convoy, blocking vs deadlock |
| Recovery | Steal/no-force; CLRs; group commit; fuzzy checkpoints; crash walkthrough; recovery models |
| Storage | Slotted pages; SSD write amplification; TOAST/off-row; free-space maps/fill factor; scan-resistant replacement; row vs column |
| Indexing | Multilevel indexes, ISAM; leftmost-prefix; ESR column ordering; `INCLUDE`; online builds; unused/missing index analysis; why indexes aren't used; **LSM, GIN, GiST, BRIN, bitmap, bloom, R-tree, vector** (as awareness) |
| Query processing | Explicit join algorithm costs; Grace/hybrid hash; external sort; Volcano/vectorized execution; subquery unnesting; interesting orders; left-deep vs bushy; parameter sniffing |
| Execution plans | Index-only/bitmap scans; warning signs; tuning workflow; `EXPLAIN` safety on DML |
| Performance | **Large OFFSET**; plan regression; temp storage; write-path performance; hot-row contention; caching strategies; **observability & metrics** |
| Security | Second-order/blind injection; ORM raw-SQL injection; **RLS**; secrets management; key management; compliance; network isolation |
| Backup/DR | Hot/cold/snapshot; WAL archiving; recovery models; DR patterns; ransomware/immutability |
| Replication | Semi-sync; logical vs physical; fencing; replication slots; read/write splitting; monotonic reads |
| Sharding | Consistent hashing; virtual nodes; global secondary indexes; global IDs; online resharding; "when *not* to shard" |
| Distributed | **Raft/Paxos introduction**; quorum math; clocks; sagas/TCC; 3PC awareness; fencing tokens; session guarantees |
| NoSQL | Single-table design; embedding vs referencing; secondary-index consistency; convergence with SQL |
| OLAP | Fact table types; measure additivity; **SCD types**; conformed/degenerate dimensions; columnar engines; data lake/lakehouse |
| Backend | **Idempotency**, **outbox/inbox**, **CDC**, **CQRS/event sourcing**, **zero-downtime migrations**, schema versioning, retry/backoff, distributed locks, pool sizing/PgBouncer, bulk/streaming, EF Core concurrency tokens, execution strategies |
| Vendors | **Difference matrix** across PG/SQL Server/MySQL |
| Practice | **32-pattern SQL catalog + canonical solutions**; **numerical formula sheet**; **20-step design method**; **9 case studies incl. ride-sharing, inventory, payment**; **rubric** |

## A.3 Weakly Covered Topics (expanded)
- **Isolation levels:** original listed anomalies and locks but never gave the isolation × anomaly matrix or vendor behavior → now §22.
- **Window functions:** now includes frames, default-frame trap, named windows, patterns.
- **Deadlocks:** now includes conditions, diagnostics, handling.
- **MVCC:** from a one-line list → mechanics, costs, vendor storage.
- **Index design:** composite ordering rules, maintenance, non-use causes.
- **Join algorithms:** from names → costs and selection criteria.
- **Query optimization:** statistics, estimation errors, join ordering, sargability rewrites.
- **Distributed databases:** consistency/quorum/consensus depth.
- **Security:** from lists → defense-in-depth with practical designs.
- **Design scenarios:** from entity lists → full method + challenges + rubric.
- **Interview questions:** original was a flat list with duplicates; now categorized with senior differentiators.
- **Final checklist:** expanded to include practice and backend items.

## A.4 Duplicate / Overlapping Topics (consolidated)
| Original duplication | Resolution |
|---|---|
| Constraints in §5 (Keys & Constraints) **and** §20 (Constraints & Data Integrity) | Merged into §5; SQL syntax in §8 |
| Transaction definition repeated in §24, §25, and Q&A (twice) | Single home §19; Q bank de-duplicated |
| "What is a view / transaction / index" repeated in beginner/intermediate Q&A | Removed duplicates |
| Joins repeated in §7 (algebra), §12, and implicit in §13 | Keep algebra in §7, SQL in §10; cross-referenced |
| Index types listed in §34 and again in §59 checklist and §58 | Single detailed home §27; checklist references only |
| Join algorithms in §37 and again in §39/§41 | Single home §30 |
| N+1 in §40.5 and §52.3 | Single home §33.3 + §43.2; cross-ref |
| Replication/consistency items spread over §44, §46 | Cross-referenced; consistency models in §38 |
| §41 "Relational Database Internals" overlapped with §30–§32 and §24 | Dissolved into proper homes (storage, MVCC, statistics) |
| §57 comparisons and §58 priorities duplicated priority labelling | Unified in §50/§51 |
| Sections 24/25 (Transactions / ACID) split trivially | Merged §19 |
| Sections 44-based "backup" vs 43 "recovery" naming confusion | Clear separation: logging/recovery (§25) vs backup/DR (§35) |

## A.5 Misplaced Topics (moved)
| Topic | From | To | Reason |
|---|---|---|---|
| Constraints (SQL) | After Views/Triggers (§20) | With Keys (§5) | Conceptual, not programmability |
| Isolation levels | Not present (only anomalies in §26) | Own section §22 after locks | Needed before deadlocks/MVCC |
| MVCC | Grouped with timestamp/OCC | §24 with snapshot isolation, plus engine detail | Practical relevance |
| Database internals (§41) | After performance | Distributed into storage, MVCC, statistics sections | Avoid orphan "internals" |
| Security | After performance | Moved ahead of backup/replication | Higher interview yield |
| Database design scenarios | After vendor knowledge | Practice section Part X; design *patterns* moved up to §18 | Patterns needed earlier |
| Modern SQL (JSON, pagination, temporal) | Scattered in data types/none | §15 | Cohesion |
| ORM/Connectivity | Late | Kept late but split: pooling/transactions (§42) vs ORM (§43) vs data evolution (§44) | Dependency on distributed concepts |
| Comparisons and priority tiers | Mid-document | Practice/planning parts | Navigability |
| Vendor-specific knowledge | After ORM | Kept after backend; plus vendor notes inline in concept sections | Concept-first with vendor hooks |

## A.6 Coverage Verification Against the Requested Audit Checklist
All areas named in the audit request were checked and are now explicitly present:

- **Fundamentals / architecture / data models:** §1–3 ✔ · **Relational model, keys, constraints:** §4–5 ✔ (incl. natural/surrogate, UNIQUE, CHECK, DEFAULT, NULL)
- **ER/EER incl. generalization, specialization, aggregation, ER-to-relational:** §6 ✔
- **Relational algebra and TRC/DRC; selection, projection, join, division, set ops:** §7 ✔
- **SQL (DDL/DML/DCL/TCL, MERGE/UPSERT, aggregates, string/date/numeric functions, type conversion, joins, subqueries, CTE/recursive, set operations, window functions, frames, ranking, LAG/LEAD, running totals, conditional aggregation):** §8–15 ✔ · **SQL interview patterns (all 22 requested + 10 more):** §47 ✔
- **FDs, closure, Armstrong, canonical cover, normal forms 1NF–5NF, MVD, JD, lossless, dependency preservation, denormalization:** §16–17 ✔
- **Transactions, schedules, serializability (conflict/view), precedence graph, recoverability, savepoints:** §19–20 ✔
- **Locks, 2PL variants, multiple granularity, intention locks, timestamp, OCC, MVCC, snapshot isolation, isolation levels with anomalies:** §21–22, §24 ✔
- **Deadlocks (conditions, wait-for graph, detection, prevention, avoidance, wait-die, wound-wait, victim, rollback):** §23 ✔
- **Recovery (types, log-based, WAL, undo/redo, checkpoints, deferred/immediate, shadow paging, ARIES, crash recovery):** §25 ✔
- **Storage (disk, SSD/HDD, pages, blocks, records, slotted pages, heap/sorted files, buffer manager, free space):** §26 ✔
- **Indexing (all requested types incl. covering, partial, expression, B/B+, static/extendible/linear hashing, selectivity, fragmentation, trade-offs):** §27–29 ✔
- **Query processing, optimization, join algorithms (all five), sargability, execution plans:** §30–32 ✔
- **Performance (slow queries, N+1, pooling, contention, bottlenecks, temp storage, plan regression, pagination, large OFFSET, keyset):** §33, §15.1 ✔
- **Security (all requested items incl. RLS):** §34 ✔ · **Backup/DR (all):** §35 ✔ · **Replication (all):** §36 ✔ · **Partitioning/Sharding (all):** §37 ✔
- **Distributed DBs (CAP, PACELC, consistency models, 2PC, Raft/Paxos intro):** §38 ✔ · **NoSQL (4 types, modeling):** §39 ✔ · **OLTP/OLAP/DW:** §41 ✔
- **ORM/backend (UoW, identity map, change tracking, loading strategies, N+1, migrations, pooling, prepared statements, EF Core):** §42–43 ✔
- **Modern/practical list (soft delete, temporal, audit, optimistic concurrency, sequences, UUIDs, JSON, FTS, geospatial, temp tables, materialized views, migrations, schema versioning, read/write splitting, CQRS, event sourcing, outbox, idempotency, distributed locking, advisory locks, CDC, change tracking, observability, metrics, slow-query logs, monitoring):** §14–15, §33, §42, §44 ✔
- **PostgreSQL / SQL Server / MySQL concepts:** §45 + inline vendor notes ✔
- **Design from requirements (20 steps, 9 systems):** §46 ✔
- **Numerical/problem catalog:** §48 ✔

## A.7 Classification of Specialized Topics (not part of the mandatory core)
**🟢 Advanced / Optional:** ARIES internals; B-tree latching/Blink/Bw-tree; optimizer frameworks (Cascades); vectorized execution; SSI internals; Percolator/Calvin/Spanner protocols; CRDTs; Paxos variants; geospatial indexing; graph query optimization; vector indexes (HNSW/IVF); bitmap/GIN/GiST/BRIN internals; columnar engine internals; lakehouse formats; building a toy DBMS.
**🟡 Medium:** relational calculus; 4NF/5NF; view serializability; LSM trees; Raft basics; NewSQL; CQRS/event sourcing; SCD/warehouse modeling; lateral joins; hybrid hash join.

---

# APPENDIX B — SUMMARY OF CHANGES

| Metric | Original | Revised |
|---|---|---|
| Major numbered sections | 60 (flat) | **53** sections in **11 Parts** (+2 appendices) |
| Priority labels | Only in comparisons and a late tier list | On every major section; tiered list in §51 |
| "What You Should Be Able to Do" blocks | 0 | **50** (every substantive section) |
| Paper/numerical problem coverage | Mentioned in passing | Full catalog + formula sheet (§48) |
| SQL interview patterns | A 7-item list | **32-pattern** catalog + 12 canonical solutions (§47) |
| Design methodology | Question list | **20-step method**, 9 case studies, rubric (§46) |
| Interview questions | 68 (with duplicates) | **81** categorized (+ senior ✱ items) |
| Comparison table entries | 32 | **67** |

**Important topics added:** isolation × anomaly matrix with real engine behavior; write skew/SSI; keyset pagination; soft delete/temporal/audit patterns; RLS; idempotency & outbox/inbox; CDC; zero-downtime migrations; CQRS/event sourcing considerations; Raft/Paxos (intro); sagas; distributed locks & fencing; observability & slow-query diagnostics; connection-pool sizing/PgBouncer; calculus (TRC/DRC); aggregation in EER; MVD/JD & synthesis algorithms; LSM/GIN/GiST/BRIN/bitmap awareness; vendor difference matrix; SQL pattern catalog; formula sheet; ride-sharing/inventory/payment case studies.

**Important topics moved:** constraints → keys section; isolation levels → standalone section ahead of deadlocks/MVCC; internals → dissolved into storage/MVCC/optimizer sections; security → before backup/replication; design patterns → right after normalization; scenario practice → dedicated practice part; comparison/priority material → end matter.

**Important topics expanded:** isolation levels, window functions, MVCC, deadlocks, composite-index design, join algorithms and costs, optimizer statistics/cardinality, execution-plan reading, performance investigation, security, replication/failover, sharding, distributed consistency/2PC, NoSQL modeling, ORM/EF Core, vendor-specific behavior.

**Intentionally classified Advanced/Optional:** ARIES depth, latch-free B-trees, optimizer internals, vectorized execution, distributed transaction protocols (Percolator/Calvin/Spanner), CRDTs, geospatial/vector/graph specifics, columnar engine internals, DBMS implementation projects.

**Remaining specialized areas (not essential for most SDE roles):** database-kernel development; DBA-grade tuning per engine (e.g., Oracle RAC, SQL Server internals, PG vacuum tuning at scale); big-data engines (Spark/Hadoop) and data engineering pipelines; time-series/graph/vector database specialization; formal database theory beyond 5NF (dependency theory, Datalog, query containment).

---

*End of syllabus.*
