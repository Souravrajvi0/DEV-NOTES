
NOW HERE WE'LL TALK ABOUT AIRPORT AS A RESOURCE HERE!!
![Pasted image 20250530145747.png](../../Images/Pasted%20image%2020250530145747.png)

In case agar main ye commarnd src mein nahi chalunga toh ye error aa jaega!

![Pasted image 20250530150432.png](../../Images/Pasted%20image%2020250530150432.png)
In Src you do this! And this happens!

![Pasted image 20250530150519.png](../../Images/Pasted%20image%2020250530150519.png)

JAVASCRIPT CONSTRAINTS!!
![Pasted image 20250530152548.png](../../Images/Pasted%20image%2020250530152548.png)

NOW DB CONSTRAINTS!!
![Pasted image 20250530152627.png](../../Images/Pasted%20image%2020250530152627.png)

![Pasted image 20250530160200.png](../../Images/Pasted%20image%2020250530160200.png)

BUT ABHI KUCH HUA NAHI HAI!!
In Cities table/ City Model the primary key is the id!! And This id will get added as the foreign key for the Airports table!
Now how can we do that!
![Pasted image 20250602111202.png](../../Images/Pasted%20image%2020250602111202.png)

**generates a new empty migration file** with the name `update-city-airport-association`.  
You will later edit this file to define the changes you want to make to your database schema (like adding or updating tables, columns, or associations)
👉 **Create a new migration file** so you can write code to **modify the database schema**, such as:

- Adding or updating tables
    
- Creating or updating associations (like foreign keys)
    
- Renaming or deleting columns
    
- Any structural database change
![Pasted image 20250602111502.png](../../Images/Pasted%20image%2020250602111502.png)
![Pasted image 20250602112658.png](../../Images/Pasted%20image%2020250602112658.png)

```javascript
queryInterface.addConstraint(tableName, options)
```

### **Arguments**

#### 1. **`tableName`** (string)

The name of the table where you want to add the constraint.

#### 2. **`options`** (object)

An object specifying the type and configuration of the constraint.


### 🧱 **Common `options` Fields**

|Field|Type|Description|
|---|---|---|
|`fields`|`Array`|Column(s) the constraint applies to|
|`type`|`string`|Type of constraint — `'FOREIGN KEY'`, `'UNIQUE'`, `'CHECK'`, `'PRIMARY KEY'`, etc.|
|`name`|`string`|Name of the constraint (optional, but recommended for rollback)|
|`references`|`object`|Required for foreign keys: `{ table: 'ReferencedTable', field: 'id' }`|
|`onDelete`|`string`|Action when the referenced row is deleted: `'CASCADE'`, `'SET NULL'`, etc.|
|`onUpdate`|`string`|Action when the referenced row is updated|
|`where`|`object`|For `CHECK` constraints (rare)|
|`deferrable`|`Deferrable`|Used for deferrable constraints (Postgres only)|

---

### 📌 **Example for Foreign Key**

```javascript
await queryInterface.addConstraint('Airports', {
  fields: ['cityId'],
  type: 'FOREIGN KEY',
  name: 'city_fkey_constraint',
  references: {
    table: 'Cities',
    field: 'id',
  },
  onUpdate: 'CASCADE',
  onDelete: 'CASCADE',
});

```

FOR DOWN FUNCTION

```javascript
await queryInterface.removeConstraint(tableName, constraintName);
```
### **What to pass:**

1. **`tableName`** – The name of the table from which you want to remove the constraint (e.g., `'airports'`).
    
2. **`constraintName`** – The exact name of the constraint you want to remove.
![Pasted image 20250602150746.png](../../Images/Pasted%20image%2020250602150746.png)


SO THESE WERE DATABASE CONSTRAINTS!! 

NOW WE NEED TO DO THE JAVASCRIPT CONSTRAINTS!!



```javascript
class Airport extends Model {

    /**

     * Helper method for defining associations.

     * This method is not a part of Sequelize lifecycle.

     * The `models/index` file will call this method automatically.

     */

    static associate(models) {

      // define association here

      this.belongsTo(models.City,{

        foreignKey:'cityId',

        onDelete:'CASCADE',

        onUpdate:'CASCADE'

      })

    }

  }
```


#### What it does:

- Inside the `Airport` model.
    
- Declares that each **Airport belongs to a City**.
    
- Links `Airport.cityId` → `City.id` via a **foreign key**.
    
- Adds cascading behavior:
    
    - **onDelete: 'CASCADE'** → If a City is deleted, its related Airports will be deleted too.
        
    - **onUpdate: 'CASCADE'** → If a City’s ID changes, the foreign key in Airports gets updated automatically.



```javascript
this.hasMany(models.Airport, {
  foreignKey: 'cityId',
});

```

#### ✅ What it does:

- Inside the `City` model.
    
- Declares that each **City has many Airports**.
    
- Also based on the same foreign key: `cityId`.

### 🔗 Together, these two define a **one-to-many** relationship:

> 📍 One **City** → Many **Airports**  
> 📍 Each **Airport** → Belongs to **one City**



