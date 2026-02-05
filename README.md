# Express PostgreSQL JOIN API 🚀

A simple **Express.js REST API** that demonstrates how to perform **SQL JOIN operations** between multiple tables in **PostgreSQL**.
This project shows how to fetch combined data from **Employee** and **Staff** tables using a JOIN query.

---
## 📂 Project Structure
```
express-postgresql-join-api
│
├── db.js # PostgreSQL connection pool
├── joint.js # Express server & JOIN API
├── package.json
└── README.md
```
## ⚙️ Database Configuration (`db.js`)

```js
const { Pool } = require('pg');

const pool = new Pool({
  user: 'your_username',
  host: 'localhost',
  database: 'your_database_name',
  password: 'YOUR_PASSWORD',
  port: 5432
});

module.exports = pool;
```
## 🗄️ Database Tables (Example)
### 🧑 Employe Table
| id | name | mobile |
| -- | ---- | ------ |
### 🏢 Staff Table
| id | age | city |
| -- | --- | ---- |


## Create Your Express Server
Create a file: joint.js
```js
// joint.js
const express = require('express');
const pool = require('./db');
const bodyParser = require('body-parser');
const app = express();
const PORT = 9000;

app.use((req, res, next) => {
  res.setHeader('Access-Control-Allow-Origin', '*'); // Or specify your origin
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS, PUT, DELETE');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  res.setHeader('Access-Control-Allow-Credentials', true); // If needed
  next();
});
// Middleware to parse JSON
app.use(bodyParser.json());

// Test the connection
app.get('/',(req, res) => {
    res.send(`<h1>EXPRESS JS API</h1>`);
});

//------------------------------------alldataselect------------------------------
// Define a route to query the database
app.get('/employe', async (req, res) => {
    try {
      const result = await pool.query('select name, mobile, age, city from employe,staff where employe.id=staff.id'); // Adjust query to your table
      res.json({status:"200",menucard:result.rows});
    } catch (err) {
      console.error('Error executing query', err.stack);
      res.status(500).send('Internal Server Error');
    }
  });
     // Start the server
  app.listen(PORT,() => {
    console.log(`Server running on http://localhost:${PORT}`);
  });  
  ```
## 🚀 API Endpoints
### 🔹 Test API
GET /

#### Response:
```
<h1>EXPRESS JS API</h1>
```
### 🔹 Get Employee + Staff Data (JOIN)
GET /employe

## 🔹 SQL Query Used
```js
SELECT name, mobile, age, city
FROM employe, staff
WHERE employe.id = staff.id;
```
### 🔹 Response Example
```js
{
  "status": "200",
  "menucard": [
    {
      "name": "Rahul",
      "mobile": "9876543210",
      "age": 25,
      "city": "Raipur"
    }
  ]
}
```  
## 🎯 Learning Outcomes
- Understanding SQL JOIN operations
- Fetching data from multiple tables
- Express.js API structure
- PostgreSQL relational database concepts
- Real-world backend query handling
    
## 👨‍💻 Author

- Kumlesh Kurre
- Backend Developer
- Skills: Express.js | Node.js | PostgreSQL | REST APIs
 
## ⭐ Support
If you like this project, please ⭐ star the repository to support my work!
  
