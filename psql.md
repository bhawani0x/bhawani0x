
## PostgreSQL Basics

### Installation
```bash
sudo apt-get install --purge postgresql postgresql-contrib
```

### Check PostgreSQL Service Status
```bash
sudo systemctl status postgresql.service
```

### Access PostgreSQL Shell
```bash
sudo -u postgres psql
```

### Basic PostgreSQL Commands

#### List of Databases
```sql
\l
```

#### List of Relations (Tables)
```sql
\dt
```

#### Describe Table
```sql
\d [table_name]
```

#### Create Database
```sql
CREATE DATABASE [database_name];
```

### Practice Queries

#### Basic Information Retrieval

##### Retrieve all rows from the table
```sql
SELECT * FROM mock_data;
```

##### Fetch details (ID, Name, Email) for a specific ID
```sql
SELECT * FROM mock_data WHERE id = 3;
```

##### Display names and emails of all entries
```sql
SELECT first_name, last_name FROM mock_data;
```

#### Sorting

##### Sort the table based on ID in ascending order
```sql
SELECT * FROM mock_data ORDER BY id;
```

##### Arrange the data alphabetically based on names
```sql
SELECT * FROM mock_data ORDER BY first_name;
```

##### Sort the table by email domain
```sql
SELECT * FROM mock_data ORDER BY SPLIT_PART(email, '@', 2);
```

#### Filtering

##### Show only entries where the name contains a specific substring
```sql
SELECT * FROM mock_data WHERE first_name LIKE '__s%';
```

##### Display rows where the email ends with a certain domain
```sql
SELECT id, email FROM mock_data WHERE SPLIT_PART(email, '@', 2) = 'google.com';
```

#### Count and Aggregation


```sql
-- Count the total number of rows in the table
SELECT COUNT(*) AS total_rows FROM mock_data;

-- Find the number of unique names in the table
SELECT COUNT(DISTINCT first_name) AS unique_names_count FROM mock_data;

-- Calculate the average length of email addresses
SELECT AVG(LENGTH(email)) AS avg_email_length FROM mock_data;
```

### Modification

```sql
-- Update the email address for a specific ID
UPDATE mock_data SET email = 'new_email@example.com' WHERE id = 123;

-- Add a new row to the table with a unique ID, name, and email
INSERT INTO mock_data (id, first_name, last_name, email) VALUES (456, 'John', 'Doe', 'john.doe@example.com');

-- Remove entries where the email domain is 'example.com'
DELETE FROM mock_data WHERE email LIKE '%@example.com';
```

### Grouping and Summarizing

```sql
-- Group entries based on the first letter of names
SELECT LEFT(first_name, 1) AS first_letter, COUNT(*) AS count FROM mock_data GROUP BY first_letter;

-- Find the total number of entries for each email domain
SELECT SPLIT_PART(email, '@', 2) AS domain, COUNT(*) AS count FROM mock_data GROUP BY domain;
```

### Combining Tables

```sql
-- Join the current table with another table based on a common column
SELECT * FROM table1 JOIN table2 ON table1.common_column = table2.common_column;

-- Combine data from two tables to create a new table
CREATE TABLE combined_data AS SELECT * FROM table1 UNION SELECT * FROM table2;
```

### Conditional Operations

```sql
-- Identify and display entries where the name starts with a vowel
SELECT * FROM mock_data WHERE first_name SIMILAR TO '[aeiou]%';

-- Show rows with email addresses longer than a certain length
SELECT * FROM mock_data WHERE LENGTH(email) > 20;
```

### Statistical Analysis

```sql
-- Find the minimum and maximum ID in the table
SELECT MIN(id) AS min_id, MAX(id) AS max_id FROM mock_data;

-- Calculate the standard deviation of the lengths of names
SELECT STDDEV(LENGTH(first_name)) AS name_length_stddev FROM mock_data;
```

### Date and Time Operations

```sql
-- If there's a date column, find entries created after a certain date
SELECT * FROM table WHERE date_column > '2023-01-01';

-- Calculate the time difference between two date entries
SELECT TIMESTAMP_DIFF(end_time, start_time, DAY) AS days_difference FROM table;
```
