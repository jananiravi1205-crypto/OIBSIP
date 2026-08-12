# SQL Injection on DVWA (Low Security)

**Target:** DVWA (Damn Vulnerable Web Application), SQL Injection module, Low security level
**Environment:** Local only — XAMPP (Windows) or LAMP (Linux)

> ⚠️ **Ethics note:** Everything in this repo was performed against a DVWA instance running on `localhost` / a local VM under my control. SQL injection is illegal against systems you don't own or don't have explicit written permission to test. None of these techniques were used against any live, third-party, or production website.

---

## 1. Setup: Installing DVWA Locally

### Option A — Windows (XAMPP)

1. Download and install [XAMPP](https://www.apachefriends.org/) (includes Apache + MySQL/MariaDB + PHP).
2. Start **Apache** and **MySQL** from the XAMPP Control Panel.
3. Download DVWA from GitHub: `https://github.com/digininja/DVWA`
4. Extract the contents into `C:\xampp\htdocs\dvwa`.
5. Inside the DVWA folder, copy `config/config.inc.php.dist` to `config/config.inc.php` and set the database credentials to match XAMPP's defaults (typically `db_user = root`, `db_password = ''`, `db_database = dvwa`).
6. In a browser, go to `http://localhost/dvwa/setup.php` and click **Create / Reset Database**. This creates the `dvwa` database and seeds the default `users` table.
7. Go to `http://localhost/dvwa/login.php` and log in with the default credentials:
   - Username: `admin`
   - Password: `password`

### Option B — Linux (LAMP)

1. Install the stack: `sudo apt install apache2 mariadb-server php php-mysqli`
2. Clone DVWA into the web root: `git clone https://github.com/digininja/DVWA.git /var/www/html/dvwa`
3. Copy and edit the config file as in Option A, matching your local MySQL/MariaDB credentials.
4. Start services: `sudo systemctl start apache2 mariadb`
5. Visit `http://localhost/dvwa/setup.php`, click **Create / Reset Database**, then log in at `http://localhost/dvwa/login.php` with `admin` / `password`.

---

## 2. Setting Security Level to Low

1. After logging in, click **DVWA Security** in the left-hand menu.
2. Select **Low** from the dropdown.
3. Click **Submit**.

At Low security, DVWA applies **no input sanitization or escaping at all** to the SQL Injection module — user input is concatenated directly into the SQL query string. This is intentional; it's the baseline case for learning how the vulnerability works before DVWA's Medium/High/Impossible levels layer on partial and full defenses.

---

## 3. Navigating to the SQL Injection Module

Click **SQL Injection** in the left-hand navigation. You'll see a single form with one field: **User ID**, and a **Submit** button.

Behind the scenes, submitting this form runs the following PHP (this is DVWA's actual Low-security source, found in `vulnerabilities/sqli/source/low.php`):

```php
if( isset( $_REQUEST[ 'Submit' ] ) ) {
    // Get input
    $id = $_REQUEST[ 'id' ];

    // Check database
    $query  = "SELECT first_name, last_name FROM users WHERE user_id = '$id';";
    $result = mysqli_query($GLOBALS["___mysqli_ston"], $query );

    // Get results
    while( $row = mysqli_fetch_assoc( $result ) ) {
        $first = $row["first_name"];
        $last  = $row["last_name"];
        echo "<pre>ID: {$id}<br />First name: {$first}<br />Surname: {$last}</pre>";
    }
}
```

The line that matters is:

```php
$query = "SELECT first_name, last_name FROM users WHERE user_id = '$id';";
```

`$id` — whatever the user typed into the User ID field — is dropped **directly** into the query string with simple quote marks around it. Nothing checks whether `$id` is actually a number, and nothing escapes special SQL characters like `'`. That's the entire vulnerability in one line.

---

## 4. What SQL Injection Is (Plain Language)

A web form usually expects a specific, narrow kind of input — here, a numeric user ID like `1` or `2`. The application builds a database query by gluing that input into a template string and asks the database to run it.

SQL injection happens when the application trusts that input to *only* ever be a value, when actually the input field is just a text box — nothing stops a user from typing something that isn't a plain value but is instead a fragment of SQL syntax itself. If the application doesn't separate "this is data" from "this is code" before handing it to the database, an attacker can type text that changes the *meaning* of the query, not just its value.

In this case, the query template is:

```sql
SELECT first_name, last_name FROM users WHERE user_id = '$id';
```

If `$id` is the string `1`, the final query is harmless:

```sql
SELECT first_name, last_name FROM users WHERE user_id = '1';
```

But if `$id` is something like `' OR '1'='1`, the closing quote in the input terminates the string literal early, and everything after it becomes part of the SQL logic the database actually executes — not data being searched for.

---

## 5. Why the Classic Payload Works

**Payload:** `' OR '1'='1`

Substituted into the template, the query the database actually receives is:

```sql
SELECT first_name, last_name FROM users WHERE user_id = '' OR '1'='1';
```

Breaking that down:
- The `'` in the payload closes the string literal that was supposed to hold the user ID.
- `OR '1'='1'` adds a second condition to the `WHERE` clause that is **always true**, for every single row in the table, regardless of what `user_id` actually is.
- Because SQL's `WHERE` clause returns every row where the condition evaluates to true, and `'1'='1'` is true for all of them, the query returns **every row in the `users` table** instead of just one.

The application was never designed to return the whole table — it was designed to look up one ID. The payload doesn't exploit a bug in the lookup logic itself; it exploits the fact that the lookup logic and the attacker's input were never properly separated.

---

## 6. Payload 1 — Documented Result

**Payload used:** `' OR '1'='1`

**Where entered:** User ID field, then Submit.

**Resulting query on the server:**
```sql
SELECT first_name, last_name FROM users WHERE user_id = '' OR '1'='1';
```

**Data exposed:** Every row in DVWA's `users` table is returned instead of a single user. DVWA's default seed data for this table is:

| user_id | first_name | last_name |
|---|---|---|
| 1 | admin | admin |
| 2 | Gordon | Brown |
| 3 | Hack | Me |
| 4 | Pablo | Picasso |
| 5 | Bob | Smith |

So instead of one name, the page prints all five `first_name` / `last_name` pairs, one after another — proof that the query condition was bypassed and the `WHERE` clause is no longer filtering by the intended ID at all.

*(See `sql_injection_notes.md` for the screenshot placeholder and raw output log for this payload.)*

---

## 7. Payload 2 — Documented Result

**Payload used:** `1' UNION SELECT user, password FROM users #`

**Resulting query on the server:**
```sql
SELECT first_name, last_name FROM users WHERE user_id = '1' UNION SELECT user, password FROM users #';
```

Breaking this one down:
- `1'` closes the string literal, matching `user_id = '1'` as a valid first half.
- `UNION SELECT user, password FROM users` appends a second, attacker-chosen query to the first one. `UNION` combines the result sets of two `SELECT` statements — as long as both statements return the same number of columns, which is why this payload selects exactly two columns (`user`, `password`) to match the original two-column query (`first_name`, `last_name`).
- `#` is a MySQL comment marker, which causes the database to ignore the trailing `'` from the original query, so the whole thing remains valid SQL rather than throwing a syntax error.

**Data exposed:** Instead of first/last names, the page prints the contents of DVWA's `user` and `password` columns — i.e., every username and its password **hash** stored in the database (DVWA stores these as MD5 hashes by default), for example:

| user | password (MD5 hash) |
|---|---|
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 |
| gordonb | e99a18c428cb38d5f260853678922e03 |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b |
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 |

This is materially worse than Payload 1: `UNION`-based injection lets an attacker pull data from **any column, in any table** in the database, not just the columns the application was designed to display — including credentials that were never meant to be exposed by this page at all. (Those hashes are crackable offline with a rainbow table or a simple dictionary attack, since MD5 is fast and unsalted here.)

*(See `sql_injection_notes.md` for the screenshot placeholder and raw output log for this payload.)*

---

## 8. How a Developer Would Fix This

The root cause in both cases is the same: user input is concatenated directly into a SQL string, so the database can't tell the difference between "the value the user typed" and "SQL syntax." The fix is to stop building queries by string concatenation entirely and use **parameterized queries / prepared statements**, where the query structure and the user's data are sent to the database *separately*.

**Vulnerable (current DVWA Low code):**
```php
$id = $_REQUEST['id'];
$query = "SELECT first_name, last_name FROM users WHERE user_id = '$id';";
$result = mysqli_query($conn, $query);
```

**Fixed, using a prepared statement:**
```php
$id = $_REQUEST['id'];

$stmt = mysqli_prepare($conn, "SELECT first_name, last_name FROM users WHERE user_id = ?");
mysqli_stmt_bind_param($stmt, "s", $id);
mysqli_stmt_execute($stmt);
$result = mysqli_stmt_get_result($stmt);

while ($row = mysqli_fetch_assoc($result)) {
    echo "First name: " . htmlspecialchars($row["first_name"]) . "<br>";
    echo "Surname: " . htmlspecialchars($row["last_name"]) . "<br>";
}
```

Why this closes the hole: the `?` placeholder is never treated as part of the SQL syntax — the database engine compiles the query structure first, *then* binds `$id` purely as a data value into that fixed structure. Even if an attacker submits `' OR '1'='1`, the database treats the entire string as a literal value to search for in the `user_id` column (and finds nothing), rather than as SQL code to execute. There is no closing quote to break out of, because the quote was never part of a string the database had to interpret as code in the first place.

Two additional, complementary layers worth applying alongside prepared statements:
- **Input validation** — since `user_id` should always be numeric here, reject or cast anything that isn't (`ctype_digit($id)`), as defense in depth.
- **Output encoding** (`htmlspecialchars()` above) — protects against a related but separate issue (stored/reflected XSS) if attacker-controlled data ever does make it into the database and back out to a page.

For a deeper technical treatment of why parameterized queries work and how different injection techniques (UNION-based, blind, boolean-based, time-based) operate, see PortSwigger's Web Security Academy: [portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection).

---

