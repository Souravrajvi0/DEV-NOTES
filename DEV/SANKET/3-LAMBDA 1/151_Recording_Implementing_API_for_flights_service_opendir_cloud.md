
 ![image-120.png](../../Images/image-120.png)
 ### 🧠 Bonus: When to Use What

![image-152.png](../../Images/image-152.png)

|Type|URL Example|Access in Code|Use When|
|---|---|---|---|
|Route Param|`/airports/:id` → `/airports/2`|`req.params.id`|For resource-specific|
|Query Param|`/airports?id=2&sort=desc`|`req.query.id`|For filtering/sorting|
FLIGHTS SERVICE API
![image-121.png](../../Images/image-121.png)

```javascript
const {FlightService} = require("../services")
const {StatusCodes} = require('http-status-codes')
const { error } = require("winston")
const{SuccessResponse,ErrorResponse}= require('../utils/common')
async function createFlight(req,res) {
    try {
        const flight = await FlightService.createFlight({
        flightNumber : req.body.flightNumber,
        airplaneId : req.body.airplaneId,
        departureAirportId : req.body.departureAirportId,
        arrivalAirportId : req.body.arrivalAirportId,
        arrivalTime : req.body.arrivalTime,
        departureTime : req.body.departureTime,
        price : req.body.price,
        boardingGate : req.body.boardingGate,
        totalSeats : req.body.totalSeats
        })
        SuccessResponse.data = airplane;
     return res
              .status(StatusCodes.CREATED)
              .json(SuccessResponse)
        
    } catch (error) {
        ErrorResponse.error = error;
        console.log("Caught error:", error);

        return res
                  .status(error.statusCode)
                  .json(ErrorResponse)
    }
    
}




module.exports = {
    createFlight
}

```
In your **Flight Controller**, when you're creating a new flight, you usually send an object to the **service** or **model layer** that **matches the Flight model's schema**.

![image-122.png](../../Images/image-122.png)

![image-123.png](../../Images/image-123.png)

`2025-08-01T10`, the `T` is **just a separator** between the **date** and the **time**.
![image-124.png](../../Images/image-124.png)

## ✅ 4. Common Mistakes in Postman:

❌ `"2025/08/01 12:00"` → Wrong format (slashes not accepted)  
❌ `"01-08-2025"` → Ambiguous and not time-aware  
❌ `"2025-08-01 12:00 PM"` → Not ISO compliant


![image-125.png](../../Images/image-125.png)


![image-126.png](../../Images/image-126.png)

Now after creating flights now we just need to create filters!!

Filters jo hai na wo query params mein jate hain!!

```javascript
class FlightRepository extends CrudRepository {
    constructor(){
       super(flights);
    }
    async getAllFlights(filter){
        const response = await flights.findAll({
            where : filter
        });
        return response;
    }
}


```

![image-127.png](../../Images/image-127.png)

![image-128.png](../../Images/image-128.png)

## 🧠 1. Why Do We Need Operators in Sequelize?

In SQL, we don’t just check for equality — we do:

- greater than (`>`)
    
- less than (`<`)
    
- not equal (`!=`)
    
- between values
    
- match a list (`IN`)
    
- etc.
    

In Sequelize (which abstracts SQL in JavaScript), we use **special objects called operators** to express these conditions.


![image-129.png](../../Images/image-129.png)

### 3. Basic SQL vs Sequelize Equivalent

| SQL                            | Sequelize Equivalent                     |
| ------------------------------ | ---------------------------------------- |
| `WHERE age = 25`               | `{ age: { [Op.eq]: 25 } }`               |
| `WHERE age > 30`               | `{ age: { [Op.gt]: 30 } }`               |
| `WHERE age >= 18`              | `{ age: { [Op.gte]: 18 } }`              |
| `WHERE age < 60`               | `{ age: { [Op.lt]: 60 } }`               |
| `WHERE age BETWEEN 18 AND 60`  | `{ age: { [Op.between]: [18, 60] } }`    |
| `WHERE name IN ('John','Ram')` | `{ name: { [Op.in]: ['John', 'Ram'] } }` |
| `WHERE name != 'Rajvi'`        | `{ name: { [Op.ne]: 'Rajvi' } }`         |
## 📦 4. Common Operators in Sequelize

| Sequelize Operator | SQL Equivalent | Use Case Example         |
| ------------------ | -------------- | ------------------------ |
| `Op.eq`            | `=`            | Exact match              |
| `Op.ne`            | `!=`           | Not equal                |
| `Op.gt`            | `>`            | Greater than             |
| `Op.gte`           | `>=`           | Greater than or equal    |
| `Op.lt`            | `<`            | Less than                |
| `Op.lte`           | `<=`           | Less than or equal       |
| `Op.between`       | `BETWEEN`      | Range queries            |
| `Op.in`            | `IN`           | One of multiple values   |
| `Op.notIn`         | `NOT IN`       | Not in a set             |
| `Op.like`          | `LIKE`         | Pattern match            |
| `Op.or`            | `OR`           | Multiple possibilities   |
| `Op.and`           | `AND`          | Combine multiple filters |
==**BHAI O should be in caps in Op**==
In Sequelize (and most ORMs), **you technically _can_ write raw SQL**, but it's **not the default approach**. Sequelize gives you an **abstraction over SQL** to make your code:
### ✅ **More secure**

Using Sequelize operators like `Op.eq`, `Op.in`, etc., **prevents SQL injection** attacks by safely escaping values.
![image-130.png](../../Images/image-130.png)

![image-131.png](../../Images/image-131.png)

![image-132.png](../../Images/image-132.png)

![image-133.png](../../Images/image-133.png)

![image-134.png](../../Images/image-134.png)

![image-135.png](../../Images/image-135.png)

`req.query` is a **JavaScript object** in Express.js that contains all the **query parameters** from the URL as **key-value pairs** (all values are strings by default).

TRIPS FILTER 
Custom filter object mein keys table ke coulms kok match karegi
![image-153.png](../../Images/image-153.png)
```javascript
let customFilter = {};
    if(query.trips){
        [departureAirportId,arrivalAirportId] = query.trips.split('-');
        customFilter.departureAirportId = departureAirportId;
        customFilter.arrivalAirportId = arrivalAirportId;
        // if there are same then we'll just return an empty object or an error
    }
    try {
     const flights = await flightRepository.getAllFlights(customFilter);
```

Jada custom filter object banana pad raha hai!

```javascript
if(query.price){
    [minPrice,maxPrice] = query.price.split('-');
     customFilter.price = {
        [Op.between] : [minPrice,maxPrice]
    }
   }
```

Now here we can't just do customfilter.minPrice = minPrice!!
Because sare prices usee bade ya uske jitne hone chahiye!! Toh yahan operator ka use hoga !!

![image-136.png](../../Images/image-136.png)

![image-137.png](../../Images/image-137.png)

### ✅ In general: use **operators** when:

- You want to compare values (`<`, `>`, `BETWEEN`, `!=`, etc.)
    
- You want to filter using conditions — not assign new keys
    

---

### 🧠 Tip: Treat `customFilter` as **"where clause for SQL"**

So write it in such a way that it's telling Sequelize **what condition should apply on which column** — and the column names must match your model (like `price`, not `minPrice`).

But happens when we send price : 1000
Here maxPrice will be undefined then!!
![image-142.png](../../Images/image-142.png)

![image-143.png](../../Images/image-143.png)


![image-144.png](../../Images/image-144.png)


![image-145.png](../../Images/image-145.png)


![image-146.png](../../Images/image-146.png)

![image-147.png](../../Images/image-147.png)

## 💡 Purpose of `customFilter`

`customFilter` is an object that holds all the dynamic conditions you want to apply in a SQL `WHERE` clause. Sequelize allows you to use this with `findAll({ where: customFilter })` to filter results based on runtime query params.

![image-148.png](../../Images/image-148.png)

![image-149.png](../../Images/image-149.png)


![image-150.png](../../Images/image-150.png)

![image-151.png](../../Images/image-151.png)

## 🧠 Sequelize Operators Cheat Sheet

|**SQL Equivalent**|**Sequelize Operator**|**Usage Example**|
|---|---|---|
|`=`|`Op.eq`|`{ age: { [Op.eq]: 25 } }`|
|`!=`|`Op.ne`|`{ name: { [Op.ne]: 'John' } }`|
|`>`|`Op.gt`|`{ price: { [Op.gt]: 100 } }`|
|`>=`|`Op.gte`|`{ quantity: { [Op.gte]: 10 } }`|
|`<`|`Op.lt`|`{ age: { [Op.lt]: 18 } }`|
|`<=`|`Op.lte`|`{ discount: { [Op.lte]: 30 } }`|
|`BETWEEN X AND Y`|`Op.between`|`{ price: { [Op.between]: [100, 200] } }`|
|`NOT BETWEEN`|`Op.notBetween`|`{ rating: { [Op.notBetween]: [1, 3] } }`|
|`IN (a, b, c)`|`Op.in`|`{ category: { [Op.in]: ['food', 'drink'] } }`|
|`NOT IN (a, b)`|`Op.notIn`|`{ country: { [Op.notIn]: ['India', 'China'] } }`|
|`LIKE '%abc%'`|`Op.like`|`{ name: { [Op.like]: '%john%' } }`|
|`NOT LIKE`|`Op.notLike`|`{ email: { [Op.notLike]: '%@gmail.com' } }`|
|`IS NULL`|`Op.is`|`{ deletedAt: { [Op.is]: null } }`|
|`IS NOT NULL`|`Op.not`|`{ deletedAt: { [Op.not]: null } }`|
|`AND`|`Op.and`|`{ [Op.and]: [{ status: 'active' }, { age: { [Op.gte]: 18 } }] }`|
|`OR`|`Op.or`|`{ [Op.or]: [{ role: 'admin' }, { role: 'moderator' }] }`|
|`!= NULL`|`Op.not`|`{ deletedAt: { [Op.not]: null } }`|
|`NOT` (generic inverse)|`Op.not`|`{ status: { [Op.not]: 'inactive' } }`|
|`REGEXP` (MySQL/PG)|`Op.regexp`|`{ username: { [Op.regexp]: '^admin' } }`|
|`NOT REGEXP`|`Op.notRegexp`|`{ username: { [Op.notRegexp]: '^user' } }`|
|`ANY`|`Op.any` (Postgres only)|`{ role: { [Op.any]: ['admin', 'user'] } }`|
|`ALL`|`Op.all` (Postgres only)|`{ score: { [Op.gt]: { [Op.all]: [50, 60] } } }`|





![image-138.png](../../Images/image-138.png)


![image-140.png](../../Images/image-140.png)

![image-154.png](../../Images/image-154.png)

![image-155.png](../../Images/image-155.png)

```javascript
  if(query.sort){
    const params = query.sort.split(',')
    const sortFilters = params.map((param)=>param.split('_'));
    sortFilter = sortFilters
   }
```

```javascript
  async getAllFlights(filter,sort){
        const response = await flights.findAll({
            where : filter,
            order : sort
        });
        return response;
    }
```

![image-156.png](../../Images/image-156.png)


![image-157.png](../../Images/image-157.png)

![image-158.png](../../Images/image-158.png)
![image-159.png](../../Images/image-159.png)



### 🔁 Summary

- Sequelize allows **multi-level ordering**.
    
- It **does not override** previous order clauses — instead, it adds another layer.
    
- The order you specify in the array **matters a lot**.