# MongoDB Tutorial

Welcome to the MongoDB tutorial! This guide covers everything from the basics to advanced features. Perfect for beginners and those looking to deepen their MongoDB expertise.

---

## 1. Introduction
MongoDB is a NoSQL database known for its flexibility, scalability, and developer-friendly nature. Unlike relational databases, MongoDB stores data in flexible, JSON-like documents.

---

## 2. Installation

### Install MongoDB
1. Download MongoDB from [MongoDB Official Site](https://www.mongodb.com/try/download/community).
2. Follow the instructions for your operating system.
3. Verify installation:
   ```bash
   mongod --version
   ```

### Start MongoDB
Run the following command to start the MongoDB server:
```bash
mongod
```

---

## 3. Basic CRUD Operations

### Connect to MongoDB
```bash
mongo
```

### Create a Database
```javascript
use myDatabase
```

### Create a Collection and Insert Data
```javascript
db.myCollection.insertOne({ name: "Alice", age: 25, city: "New York" });
```

### Read Data
```javascript
db.myCollection.find();
```

### Update Data
```javascript
db.myCollection.updateOne({ name: "Alice" }, { $set: { age: 26 } });
```

### Delete Data
```javascript
db.myCollection.deleteOne({ name: "Alice" });
```

---

## 4. Data Modeling
- Use embedded documents for related data.
- Use references for large, complex datasets.

### Example: Embedded Document
```javascript
{
   name: "Alice",
   address: { city: "New York", zip: "10001" }
}
```

### Example: Reference
```javascript
{
   name: "Alice",
   address_id: ObjectId("603d6ecf0f1c2c4f4c4f9f01")
}
```

---

## 5. Indexes
Indexes improve query performance.

### Create an Index
```javascript
db.myCollection.createIndex({ name: 1 });
```

### View Indexes
```javascript
db.myCollection.getIndexes();
```

---

## 6. Aggregation Framework
The aggregation framework processes data and returns computed results.

### Example: Aggregation Pipeline
```javascript
db.myCollection.aggregate([
   { $match: { age: { $gte: 25 } } },
   { $group: { _id: "$city", total: { $sum: 1 } } }
]);
```

---

## 7. Replication
Replication ensures high availability and data redundancy.

### Steps:
1. Start MongoDB with replica set configuration:
   ```bash
   mongod --replSet "rs0"
   ```
2. Initiate the replica set:
   ```javascript
   rs.initiate();
   ```
3. Add members to the replica set:
   ```javascript
   rs.add("hostname:port");
   ```

---

## 8. Sharding
Sharding distributes data across multiple servers for horizontal scalability.

### Steps:
1. Start a config server:
   ```bash
   mongod --configsvr --replSet configReplSet --dbpath /data/configdb --port 27019
   ```
2. Start shard servers.
3. Connect to the mongos router and enable sharding on a database:
   ```javascript
   sh.enableSharding("myDatabase");
   ```

---

## 9. Advanced Features

### Transactions
Perform multi-document transactions for ACID compliance.
```javascript
const session = db.getMongo().startSession();
const myDB = session.getDatabase("myDatabase");
session.startTransaction();
try {
   myDB.myCollection.insertOne({ name: "Bob" });
   myDB.myCollection.updateOne({ name: "Alice" }, { $set: { age: 30 } });
   session.commitTransaction();
} catch (error) {
   session.abortTransaction();
} finally {
   session.endSession();
}
```

### Change Streams
Monitor real-time changes to data.
```javascript
const changeStream = db.myCollection.watch();
changeStream.on("change", (change) => {
   console.log(change);
});
```

---

## 10. Best Practices
1. Use indexes wisely to optimize queries.
2. Design data models based on application needs.
3. Enable authentication for secure access.
4. Use backups and replication for data safety.
5. Monitor performance using tools like MongoDB Compass or Atlas.

---

For more details, check the [official MongoDB documentation](https://docs.mongodb.com/).
