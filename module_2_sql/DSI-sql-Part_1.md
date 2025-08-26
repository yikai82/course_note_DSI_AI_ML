# Module 2 – SQL Part 1 

### ![server](image/server.svg)  This note covers the activity during **[day 1](https://www.youtube.com/watch?v=ZFFHCdu7h2s) & [day 2](https://www.youtube.com/watch?v=E8Mx-L5OvNM) of the SQL live section** 

* [Requirement](#requirement)  
* [Key notes during the live sections](#key-notes-during-the-live-sections)  
* [1. SQL Database](#1-sql-database)
* [2. Basic commands](#2-common-commands)  
  * [2.1 `SELECT...FROM`, `Order by`, `like`, `limit`, `where`](#21-select-order-by-like-limit-where)  
  * [2.2 `LIKE IS`, `NULL`, `between`, `case`](#22-like-is-null-between-case)  
* [📌 3. ALL about JOIN ](#join)  
  * [JOIN Diagram](#the-diagram-below-illustrate-the-different-type-of-join)  

<br>  

---
> [!NOTE]  
> Not sure where to start 😵‍💫😵‍💫 Try with ![Commonly Use!](https://img.shields.io/badge/++_Commonly_Use!-911919) and **Pin** 📌



---
## System

<div align="left">
  <div style="margin: 2px 0;">
    <img src="image/Linux2.svg" alt="Linux" width="50" style="vertical-align: middle; margin-right: 6px;">
    <span style="vertical-align: middle;">Kubuntu-T2 24.04.2 LTS</span>
  </div>
  <div style="margin: 2px 0;">
    <img src="image/Noble.svg" alt="Noble" width="50" style="vertical-align: middle; margin-right: 6px;">
    <span style="vertical-align: middle;">Codename: Noble</span>
  </div>
</div>  

Release:	24.04
Kernel Version: Linux 6.14.0-1-t2-noble

---
## Requirement 
1. Install **DB Browser for SQlite**

```bash
sudo apt update
sudo apt install sqlitebrowser
```

2. Clone the DSI-SQL repo and make sure you have the dataset **farmersmarket.db**, which is under /sql/05_src/.  

```bash
cd /path/to/work/directory
cd /sql
git status
git switch assignment  # use git switch -c assignment if branch assignment does not exist yet. 
git remote -v # if you don't have the upstream setup, you should set it up now
git remote add upstream [url]
git fetch upstream main
git pull upstream main  # Merge the changes in the upstream main to your local branch
# If there is a conflict, use one of the following commands:
git pull --no-rebase upstream main  
        # You might want to use --no-rebase if:
        # You prefer automatic merge commits.
        # You want to preserve the exact chronological order of all commits.
        # Your team prefers traditional merge-based workflows.
git pull --rebase upstream main
        # Cleaner history but not ideal as it rewrites history.
        # If you are working in your own personal branch, use --rebase only if you're comfortable resolving rebase conflicts.
        # Do not rebase public/shared branches.

git push origin assignment # Push the update to your GitHub fork's assignment branch 
```

---
## 📌 Key notes during the live sections  
1. Some PKs in the Farmers Market database are composite keys.  
2. **Why do we need Primary Keys and Foreign Keys?**  
    - **Formalizing the relationship between PKs and FKs ensures that..**
    - **New records added to tables required....**  
    - **Hekp to ensure that deleted records do not make data elsewhere meaningless**  

3. Why use market_date as the PK in the vendor_inventory table for Farmers Market DB?  
4. If there is no relationship between tables, you write a query for that. 
5. Health Insurance person whose plan expired vs. his/her claim eligibility
6. **ERD**: The flow is from a FK of a table to a PK of a related table. **Flow from FK --> PK**, we cannot delete the 2nd table until we delete the FK.  
7. **Denormalization** sometimes helps us to build a better ERD -> better design
8. **SQL Concept Map**  
<br>

<sub>[↥ back to top](#)</sub>

---
## 1. SQL Database
### **Database and Database Management System**
Different Flavours for SQL (What is flavour?)
- Open Source Systems:
  - Excellent at what they are designed for
  - Varying data types

- Enterprise Systems: 
  - Powerful
  - Hard to move - Migration could be costly, or even outrageous

We are using SQLite
 - Super easy to set up
 - Requires almost no overhead
 - Commonly used as a backend (e.g. Firefox uses a SQLite backend to write a user's history)

Database Type: Relational vs Transactional
- Relational: Relational databases are a collection of tables, views, procedural code, and other SQL-assisting artefacts 
  - The data stored will be related to a real-world concept
  - Backends to data-collecting systems are often databases
    - CRMs
    - EMR software
    - ERPs
    - Web-based apps
- Transactional: data is actively written to by frontend systems
- Most modern relational databases are also transactional.
- NoSQL: non-relational databases 

Data Warehouse vs Data Marts
- Warehouse:
  - Centralized 
  - Highly-structured
  - Tables are **denormalized** 

- Data Mart
  - Designed to make a Data Warehouse easier to use
  - Structured but flexible
  - Some denormalized tables
  - Common for enterprises that have Data Warehouses.

Data Lakes vs Data Swamps
- Data Lakes
  - Allow on-demand access to raw, semi-structured, structured, or unstructured data
  - Highly scalable
  - Can be transactional, depending on the design
  - Inexpensive compared to a Data Warehouse
  - Gained popularity due to supporting tools like Snowflake

- Data Swamps
  - A poorly-maintained Data Lakes, which lack governance and documentation. 

**Relational Database Management Systems (RDBMs)**
- Use a query language
- Allow users to define interactions between objects
- Manage permissions
- Mitigate data corruption and unauthorized access

Data Models: a notation to describe data or information.

Data Models consists of:
- Structure of the data
  - **Entiry: Table title in drawio??**
  - Attribute: columns, which are defined and restricted 
    - `INT`
    - `FLOAT`, `DECIMAL`, `REAL`
    - `VARCHAR`, `NVARCHAR`, `TEXT`
    - `DATE`, `TIME`, `DATETIME` 
  - Observation: rows 
- Constraints: these are rules that must be followed 
  - Referential-Integrity constraints
  - Attribute constraints
  - Common constraints:  
      - `IS NULL` and `IS NOT NULL`
      - `UNIQUE`
      - **PRIMARY KEY (PK)**: Ensure each value in a column is unique; one PK per table; cannot be `NULL`
      - **FOREIGN KEY (FK)**: Not every table requre FKs; it can be NULL
      - **Composite Key**: Sometimes, no single column in a table is unique. Thus we build composite keys to make PK unique.  
<br>

<sub>[↥ back to top](#)</sub>

---
### **Entity Relationship Diagram (ERD)**
**What are ERDs?**
- ERDs are Diagrams depicting the structure of tables within a database

- ERDs are useful for: 
  - Database design
  - Debugging
  - Writing logical, consistent, and efficient queries

- There are three levels of details for ERD depiction
  - **Conceptual models**: **Define** the tables (objects/entities) and their relationships
    - Not all tables share relationships to one another, but all tables have at least one relationship
  - **Logical models**: Add additional **detail to the conceptual model** by adding column names for each table
    - Often indicates the type of relationship: 
      - One-to-One
      - One-to-Many
      - Many-to-Many
  - **Physical models**: Add additional detail to the logical model by adding **key type** and **column data type**  


Attributes of an ERD Entity:
- For a given table:
  - Name
  - Relationship to another table
  - Column Names
  - Column Type
  - PRIMARY KEYs (if present)
  - Foreign Keys (if present)  

Attributes of an ERD Relationship
- Defines which columns are related
- Defines what types of relationships exist
  - One-to-One
  - One-to-Many
  - Many-to-Many


<sub>[↥ back to top](#)</sub>

---
## 2. Basic commands

**### Note: In DB Browser for SQLite, to PRESS FN key + SHIFT toggle the cursor from "I" to "_"** 

I have selected the following command as example :

### 2.1: `SELECT`, `ORDER BY`, `LIKE`, `LIMIT`, `WHERE` 
```sql
-- SELECT*FROM [table_name] -- select *everything* from the [table_name]
-- From product
SELECT* FROM product ORDER BY product_id ASC; 

-- From customer_purchases
SELECT* FROM customer_purchases;
SELECT DISTINCT product_id FROM customer_purchases;

-- From customer 
SELECT* FROM customer;
SELECT*FROM customer
WHERE customer_id IN (3,4,5) -- only customer id = 3, 4, 5
OR	 customer_postal_code IN ('M4H','M1L');

-- From vendor--
SELECT* FROM vendor ORDER BY vendor_name ASC;

-- call out the first 10 customer based on their first name
SELECT* FROM customer ORDER BY customer_first_name LIMIT 10;
```

### 2.2: `LIKE`, `IS NULL`, `BETWEEN`, `CASE`
```sql
-- LIKE: to be used with wildcard(%)
SELECT*FROM product WHERE product_name like '%pepper%';     --any pepper in between 
SELECT*FROM customer WHERE customer_last_name LIKE 'a%';    --last name starts with 'a" 
SELECT*FROM customer WHERE customer_id between 1 and 20;    --output from 1 to 20

-- CASE --
-- use as "if" to add some logic to determine which vendors come on which days 
SELECT* , 
case when vendor_type = 'Fresh Focused' then 'Wednesday'
	when vendor_type = 'Prepared Foods' then 'Thursday'
	else 'Saturday' 
end as day_of_speciality
FROM vendor;

-- Double the Case
-- pie day, otherwise nothing 

Select* ,
case when vendor_name = "Annie's Pies" -- double quotes will work --just this once!
	then 'annie is the best'
	end as annie_is_the_king
	, case when vendor_name LIKE '%pie%'
	then 'Wednesday'
	ELSE 'Friday'	-- with the else, we get values for FALSE statements
END as pie_day
FROM vendor;
```

<sub>[↥ back to top](#)</sub>

---
## 3. `JOIN` 
### To reference data by combining different tables. For example, the table customer_purchase only has customer id and the customer table has both customer id and customer name. You want to combine a table that has customer name, id, and purchase history.  


---
![Commonly Use!](https://img.shields.io/badge/++_Commonly_Use!-911919) 
### 3.1 (INNER) JOIN:  
- is the default join.  
- filter `both` tables to rows present in both tables --> NO NULL  
- **Common error**: **ambiguous columnuse**, use alias to refer to the columns that exist on both tables  
<br>


```sql
-- list the product names and customer name which vendor has sold products to 
SELECT
p.product_name,
vendor_id,
cp.market_date,
cp.customer_id,
c.customer_first_name,
c.customer_last_name

FROM customer_purchases as cp  --"as" can be remove if needed 
INNER JOIN product as p
		ON p.product_id = cp.product_id
INNER JOIN customer as c
		ON c.customer_id = cp.customer_id;

-- output the vendor table to the vendor_booth_assignments table on the and sorts the result by vendor_name, then market_date. */
SELECT
vb.vendor_id,
vendor_name,
booth_number,
market_date

FROM vendor_booth_assignments as vb
	JOIN vendor as v
	ON vb.vendor_id = v.vendor_id

ORDER BY vendor_name ASC, market_date;
```

<sub>[↥ back to top](#)</sub>

---

### 3.2 LEFT JOIN  
- **LEFT** will be preserved so the row in the "right" table will be filtered.   
- will oftern produce NULL.  
- Its direction matters. 
 
```sql
-- output the product that have not been bought
SELECT DISTINCT
p.product_id, 
cp.product_id as [cp.product_id], -- **why do we need to use `[ xxxxxxx ]`**
product_name

FROM product as p
LEFT JOIN customer_purchases as cp
	ON p.product_id = cp.product_id

WHERE cp.product_id IS NULL	  -- only show the NULL 

```

<sub>[↥ back to top](#)</sub>

---

### 3.3 RIGHT JOIN: 
- filter the left table to the row present in the right table.
- will oftern produce NULL.
- **Note: Since we can also flip-flop the ourput from LEFT JOIN to get the same outcome, it is less used.** 

### 3.4 FULL (OUTER) JOIN
-  **Mor than one table** can be joined at a time.
-  We want **to see what is NOT (filter function) in a certain table --> will produce NULL**
-  Match fo where **A.KEY IS NULL OR B.KEY IS NULL**

```sql
SELECT
cp.vendor_id,
v.vendor_name,
p.product_name,
cp.market_date,
cp.customer_id,
c.customer_first_name,
c.customer_last_name

FROM customer_purchases as cp
FULL JOIN product as p
	ON p.product_id = cp.product_id
FULL JOIN customer as c
	ON c.customer_id = cp.customer_id
FULL JOIN vendor as v
	ON v.vendor_id = cp.vendor_id  -- generate 4242 rows why it is more than SELECT*FROM customer_purchases??, Because there is NUULL	
WHERE cp. customer_id IS NULL;  -- return information related to no client purchase


SELECT*FROM customer_purchases;  -- contains 4221 rows
```

<sub>[↥ back to top](#)</sub>

---
![Commonly Use!](https://img.shields.io/badge/++_Commonly_Use!-911919) 

### 3.5 Multiple Table JOIN
- More than one table can be JOIN
- The order and types of JOIN matter
- It is important to decide which table should be the **FROM** table.  
<br>  
  

```sql	
/* which vendor has sold products to a customer 
... and which product was it? 
... AND to whom was it sold*/ 

SELECT 
DISTINCT  			--comment in remove will have the same row number as customer_purchases 
--cp.vendor_id,    	--uncomment if you want to see the vendor_id 
v.vendor_name,
p.product_name,
cp.market_date, 	-- If including the market data, entry include from 200 rows to 3371 rows 
-- cp.customer_id, 	--uncomment in choice if you want to see the  
c.customer_first_name,
c.customer_last_name

FROM customer_purchases as cp
JOIN product as p
	ON p.product_id = cp.product_id
JOIN customer as c
	ON c.customer_id = cp.customer_id
JOIN vendor as v
	ON v.vendor_id = cp.vendor_id
```
<br>  
<br>

### The diagram below illustrate the different type of JOIN: 
![JOIN Diagram](image/SQL%20JOIN.png)

<sub>[↥ back to top](#)</sub>


---
<!-- ### Parking Lot

###  🚧 🚧 🚧 🚧 🚧  Construction Zone  🚧 🚧 🚧 🚧 🚧


---
### ✅ 



---
### 📚 Other References:
1. []() -->