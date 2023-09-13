## MONGODB-TASK

# Product Database MongoDB Queries

This repository contains MongoDB queries for a product database.
The database contains information about various products, including their names, prices, materials, colors, and unique IDs.
Below are the queries you can use to retrieve specific information from the database.

## Prerequisites

- MongoDB installed and running on your local machine or server.
- A MongoDB database containing the product data.
- Installed mongosh for delete the products.

## Queries

1. **Find all the information about each product:**

    ```javascript
    db.products.find({})
    ```

2. **Find the product price which is between 400 to 800:**

    ```javascript
    db.products.find({ "product_price": { $gte: 400, $lte: 800 } })
    ```

3. **Find the product price which is not between 400 to 600:**

    ```javascript
    db.products.find({ "product_price": { $lt: 400, $gt: 600 } })
    ```

4. **List the four products which are greater than 500 in price:**

    ```javascript
    db.products.find({ "product_price": { $gt: 500 } }).limit(4)
    ```

5. **Find the product name and product material of each product:**

    ```javascript
    db.products.find({}, { "product_name": 1, "product_material": 1, "_id": 0 })
    ```

6. **Find the product with a row ID of 10:**

    ```javascript
    db.products.find({ "id": "10" })
    ```

7. **Find only the product name and product material:**

    ```javascript
    db.products.find({}, { "product_name": 1, "product_material": 1, "_id": 0 })
    ```

8. **Find all products which contain the value "soft" in product material:**

    ```javascript
    db.products.find({ "product_material": /soft/i })
    ```

9. **Find products which contain the product color "indigo" and product price 492.00:**

    ```javascript
    db.products.find({ "product_color": "indigo", "product_price": 492.00 })
    ```

10. **Delete the products which have the same product price value:**

    **Warning: Be cautious when using this query as it performs deletions.**

    ```javascript
    db.getCollection("products").aggregate([
    {
    $group: {
      _id: '$product_price',
      count: { $sum: 1 }
    }
       },
    {
    $match: {
      count: { $gt: 1 }
    }
    }
     ]).forEach((e) => {
     db.getCollection("products").deleteMany({ product_price: e._id });
    });
    ```

## Usage

1. Connect to your MongoDB database.

2. Open the MongoDB shell or use a MongoDB client.

3. Copy and paste the desired query from the list above into the shell or client.

4. Execute the query to retrieve the desired information from your product database.

## Disclaimer

Be cautious when performing deletions in your database. Always make sure to have proper backups and test queries in a safe environment. Deleting data cannot be undone.
