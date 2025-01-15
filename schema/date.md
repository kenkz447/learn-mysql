### MySQL Date and Time Data Types

MySQL provides a variety of data types for storing date and time values. These data types help store dates, times, and timestamps efficiently while enabling robust date and time operations.

---

### **Types of Date and Time Data**

| Data Type     | Description                                           | Storage (Bytes) | Range                                  |
|---------------|-------------------------------------------------------|-----------------|----------------------------------------|
| **DATE**      | Stores date only (YYYY-MM-DD).                       | 3               | 1000-01-01 to 9999-12-31               |
| **DATETIME**  | Stores date and time (YYYY-MM-DD HH:MM:SS).          | 8 (5 with fractional seconds) | 1000-01-01 00:00:00 to 9999-12-31 23:59:59 |
| **TIMESTAMP** | Stores UTC date and time with time zone conversion.  | 4 (7 with fractional seconds) | 1970-01-01 00:00:01 UTC to 2038-01-19 03:14:07 UTC |
| **TIME**      | Stores time only (HH:MM:SS).                         | 3               | -838:59:59 to 838:59:59                |
| **YEAR**      | Stores year (YYYY).                                  | 1               | 1901 to 2155                           |

---

### **DATE**

- **Use Case:** For storing dates without time information (e.g., birth dates, event dates).
- **Syntax:**
  ```sql
  CREATE TABLE example_date (
    event_date DATE
  );
  ```
- **Example Insert:**
  ```sql
  INSERT INTO example_date (event_date) VALUES ('2023-12-25');
  ```

---

### **DATETIME**

- **Use Case:** For storing exact date and time, irrespective of time zones (e.g., log timestamps).
- **Syntax:**
  ```sql
  CREATE TABLE example_datetime (
    created_at DATETIME
  );
  ```
- **Example Insert:**
  ```sql
  INSERT INTO example_datetime (created_at) VALUES ('2023-12-25 15:30:00');
  ```

---

### **TIMESTAMP**

- **Use Case:** Stores UTC date and time with automatic time zone conversion based on the server and client time zones.
- **Features:**
  - Automatically updates to current time on `INSERT` or `UPDATE` when configured.
  - Best for audit logs or tracking changes.
- **Syntax:**
  ```sql
  CREATE TABLE example_timestamp (
    last_modified TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
  );
  ```
- **Example Insert:**
  ```sql
  INSERT INTO example_timestamp VALUES ();
  ```

---

### **TIME**

- **Use Case:** For storing time intervals or times of day (e.g., work hours, durations).
- **Syntax:**
  ```sql
  CREATE TABLE example_time (
    duration TIME
  );
  ```
- **Example Insert:**
  ```sql
  INSERT INTO example_time (duration) VALUES ('12:30:45');
  ```

---

### **YEAR**

- **Use Case:** For storing year values (e.g., manufacturing year, year of study).
- **Syntax:**
  ```sql
  CREATE TABLE example_year (
    year_of_manufacture YEAR
  );
  ```
- **Example Insert:**
  ```sql
  INSERT INTO example_year (year_of_manufacture) VALUES (2024);
  ```

---

### **Choosing the Right Data Type**

1. **Use `DATE`** when time is irrelevant (e.g., date of birth).
2. **Use `DATETIME`** for exact date and time tracking without time zone considerations.
3. **Use `TIMESTAMP`** for automatic UTC time zone conversion and tracking updates.
4. **Use `TIME`** for intervals or standalone time values.
5. **Use `YEAR`** when only the year is needed.

By selecting the appropriate date and time type, you can optimize storage, ensure data integrity, and simplify time-related operations in your MySQL database.