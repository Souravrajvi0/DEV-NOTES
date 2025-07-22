---
view-count: 2
---
![NORMALISATION 2-20241225115103524.webp](../../../Images/NORMALISATION%202-20241225115103524.webp)
Normalization is a process in database design that organizes data to minimize redundancy and dependency issues. It breaks data into smaller tables and establishes relationships between them to ensure data is stored efficiently and accurately

### Why Normalize?

- **Reduce Redundancy**: Avoid storing the same data in multiple places.
- **Improve Data Integrity**: Ensure data is accurate and consistent.
- **Simplify Maintenance**: Make it easier to update or modify data.
- **Optimize Queries**: Enhance database performance by reducing the size of tables


### Normal Forms in Normalization

Normalization is done in stages called **Normal Forms** (NFs). Each stage addresses specific issues:


### 1. **First Normal Form (1NF): Eliminate Repeating Groups**

- Ensure every column has atomic (indivisible) values.

![NORMALISATION 2-20241225120256317.webp](../../../Images/NORMALISATION%202-20241225120256317.webp)

- So Pehle Wali Table mein problem ye hai ki in case we change DSA to DATA STRUCTURUE AND ALGORITHMS Now We'll have to change it all those places and usske like  mujhe array mein search karna padega!
- In case agar N students and Total M courses hain toh har student M students Mein enroll Hoskta hai at max so isliye mujhe at MAX N* M Searches krne padenge SIRF DSA WALO KO DHUNDHNE K LIYE!!!
EXAMPLE:
![NORMALISATION 2-20241225120827119.webp](../../../Images/NORMALISATION%202-20241225120827119.webp)

### 2. **Second Normal Form (2NF): Eliminate Partial Dependencies**

- Must be in 1NF.
- Ensure non-key attributes depend on the **entire primary key**, not just part of it (addresses issues with composite keys).
- The table should not have partial dependencies 

EVEN THIS IS 1F AND WE STILL NEED TO MAKE CHANGE IN EVERY ROW WHERE DSA IS PRESENT 
![NORMALISATION 2-20241225121529038.webp](../../../Images/NORMALISATION%202-20241225121529038.webp)

![NORMALISATION 2-20241225122634855.webp](../../../Images/NORMALISATION%202-20241225122634855.webp)

![NORMALISATION 2-20241225122707090.webp](../../../Images/NORMALISATION%202-20241225122707090.webp)


![NORMALISATION 2-20241225123834650.webp](../../../Images/NORMALISATION%202-20241225123834650.webp)


### 3. **Third Normal Form (3NF): Eliminate Transitive Dependencies**

- Must be in 2NF.
- Ensure non-key attributes depend only on the primary key, not on other non-key attributes.
- THE TABLE SHOULD NOT HAVE TRANSITIVE DEPENDENCY

![NORMALISATION 2-20241225124041093.webp](../../../Images/NORMALISATION%202-20241225124041093.webp)

![NORMALISATION 2-20241225124528097.webp](../../../Images/NORMALISATION%202-20241225124528097.webp)

![NORMALISATION 2-20241225125534991.webp](../../../Images/NORMALISATION%202-20241225125534991.webp)
