### Understanding Integers in MySQL: Types and Ranges

MySQL provides various data types to store integers, each with specific storage requirements and ranges. Choosing the right integer type is essential for efficient and scalable database design.

---

### **Integer Data Types and Ranges**

MySQL offers five primary integer types, along with their storage sizes and value ranges:

| **Data Type** | **Storage** | **Unsigned Range**          | **Signed Range**              |
|---------------|-------------|-----------------------------|-------------------------------|
| `TINYINT`     | 1 byte      | 0 to 255                   | -128 to 127                  |
| `SMALLINT`    | 2 bytes     | 0 to 65,535                | -32,768 to 32,767            |
| `MEDIUMINT`   | 3 bytes     | 0 to 16,777,215            | -8,388,608 to 8,388,607      |
| `INT` (or `INTEGER`) | 4 bytes | 0 to 4,294,967,295        | -2,147,483,648 to 2,147,483,647 |
| `BIGINT`      | 8 bytes     | 0 to 18,446,744,073,709,551,615 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

---

### **Understanding Unsigned and Signed Integers**

- **Unsigned**: Values range from 0 to the positive maximum.
- **Signed**: Allows both positive and negative values by dedicating one bit for the sign.

For example, a `TINYINT`:
- Unsigned: 0 to 255.
- Signed: -128 to 127 (one bit for the sign and seven for the value).

---

### **Choosing the Right Data Type**

Selecting the appropriate data type depends on the range of values you expect to store. Opt for the smallest data type that accommodates your data to save storage and improve query performance.

#### **Example: Storing Book Page Counts**
- **Scenario**: A "books" table with a `number_of_pages` column, where no book has more than 65,000 pages.
- **Solution**: Use `SMALLINT UNSIGNED` since it can hold values from 0 to 65,535, and negative numbers aren't needed.
  
```sql
CREATE TABLE books (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255),
  number_of_pages SMALLINT UNSIGNED
);
```

---

### **The Myth of `INT(11)`**

- **Misconception**: `INT(11)` controls the range of values.
- **Reality**: The number in parentheses only specifies *display width* (deprecated in MySQL 8.0). It doesn't affect storage size or range.
- **Example**: `INT(11)` and `INT` are functionally identical in terms of range and storage.

---

### **Best Practices for Using Integers**

1. **Optimize for Range**:
   - Use the smallest data type that fits your data range to reduce storage requirements.
   - Avoid using `BIGINT` unless the range exceeds `INT`.

2. **Use Unsigned When Appropriate**:
   - Use `UNSIGNED` for columns that will never store negative values, effectively doubling the positive range.

3. **Avoid Deprecated Features**:
   - Ignore display width (e.g., `INT(11)`), as it's deprecated.

4. **Consider Future Growth**:
   - Choose a data type that supports both current needs and reasonable future growth.

---

### **Example: Practical Implementation**

#### Creating a Table:
```sql
CREATE TABLE library (
  book_id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255),
  published_year SMALLINT,
  page_count SMALLINT UNSIGNED,
  copies_sold BIGINT UNSIGNED
);
```

#### Inserting Data:
```sql
INSERT INTO library (title, published_year, page_count, copies_sold)
VALUES ('The Great Book', 2023, 450, 1500000000);
```

#### Querying Data:
```sql
SELECT title, page_count, copies_sold
FROM library
WHERE page_count > 300;
```

---

### **Conclusion**

Understanding MySQL's integer types and ranges helps design efficient schemas. By selecting the correct data type and attributes (e.g., signed vs. unsigned), you can optimize storage, ensure data integrity, and improve query performance.