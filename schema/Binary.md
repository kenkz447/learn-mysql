### Understanding Binary Data Storage in MySQL

Binary columns in MySQL (`BINARY` and `VARBINARY`) offer an effective way to store raw binary data without involving character sets or collations. These are particularly useful when dealing with data like hashes, UUIDs, or other byte-oriented values.

---

### **Key Features of Binary Data Types**

1. **Raw Binary Storage**:
   - Unlike `CHAR` and `VARCHAR`, which store characters according to a character set, `BINARY` and `VARBINARY` store raw byte data.
   - No need to worry about collations or encodings.

2. **Fixed vs. Variable Length**:
   - `BINARY`: Fixed-length column, always uses the specified number of bytes.
   - `VARBINARY`: Variable-length column, uses only the number of bytes required by the actual data (up to the specified limit).

3. **Compact and Efficient**:
   - Ideal for data that doesn’t require human-readable formats, such as cryptographic hashes or unique identifiers.

---

### **How to Use Binary Columns**

#### **Table Definition**
Here’s an example of creating a table with `BINARY` and `VARBINARY` columns:

```sql
CREATE TABLE bins (
  bin BINARY(16),          -- Fixed-length, 16 bytes
  varbin VARBINARY(100)    -- Variable-length, up to 100 bytes
);
```

#### **Inserting Binary Data**
To store binary data, use functions like `UNHEX` to convert hexadecimal strings to binary:

```sql
INSERT INTO bins (bin, varbin) 
VALUES (UNHEX(MD5('hello')), UNHEX(MD5('hello')));
```

- `MD5('hello')` generates a hash: `5d41402abc4b2a76b9719d911017c592`.
- `UNHEX` converts the hash from hexadecimal to binary.

#### **Retrieving Binary Data**
Binary data can be retrieved as-is or converted back into a readable hexadecimal format using `HEX`:

```sql
SELECT HEX(bin), HEX(varbin) FROM bins;
```

This displays the stored binary data as hexadecimal strings.

---

### **Practical Example with MD5 Hashes**

1. **Generate Binary Data**:
   Use the `MD5` function and convert it to binary:
   ```sql
   SELECT UNHEX(MD5('example'));
   ```

2. **Insert Data**:
   ```sql
   INSERT INTO bins (bin, varbin) 
   VALUES (UNHEX(MD5('example')), UNHEX(MD5('example')));
   ```

3. **Query Binary Data**:
   View binary data:
   ```sql
   SELECT * FROM bins;
   ```
   Retrieve hexadecimal representation:
   ```sql
   SELECT HEX(bin), HEX(varbin) FROM bins;
   ```

---

### **Why Use Binary Columns?**

1. **Efficiency**:
   - Binary columns store data more compactly compared to storing hexadecimal strings in character columns.
   - Avoid the overhead of character set conversion.

2. **No Collation Rules**:
   - Binary data isn’t subject to sorting or comparison rules based on collations, which can simplify certain operations.

3. **Use Cases**:
   - Storing cryptographic hashes (e.g., MD5, SHA256).
   - Managing UUIDs in a compact format.
   - Encoding raw binary files or serialized data.

---

### **Conclusion**
`BINARY` and `VARBINARY` are essential for applications where raw binary data needs to be stored efficiently and without the constraints of character encoding. They provide a flexible option for handling data like hashes, UUIDs, and binary blobs. By leveraging functions like `UNHEX` and `HEX`, you can easily convert between readable and binary representations, enabling smooth integration into your MySQL-based applications.