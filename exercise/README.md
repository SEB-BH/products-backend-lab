<h1>
  <span class="headline">MERN Inventory Management API Lab</span>
  <span class="subhead">Exercise</span>
</h1>

## Requirements

We are building an app with the following endpoints:

| HTTP Method | Response | Endpoint       | Use Case           |
| ----------- | -------- | ------------- | ------------------ |
| POST        | 201      | `/products`     | Create a product     |
| GET         | 200      | `/products`     | List all products    |
| GET         | 200      | `/products/:id` | Get a single product |
| PUT         | 200      | `/products/:id` | Update a product     |
| DELETE      | 200      | `/products/:id` | Delete a product     |




## Part 2: Create the Product Model

1. Create a models folder
2. In your models folder create a file `Product.js`
3. The client asked for the following things to track about the products:


|  **Field**  | **Data Type** |                               **Validation**                              |
|:-----------:|:-------------:|:-------------------------------------------------------------------------:|
|    Title    |     String    |                               Required, trim                              |
| description |     String    |                               maxLength: 500                              |
|   category  |     String    | required, enum: ["electronics", "food", "clothing", "furniture", "other"] |
|    price    |     Number    |                             required, min: 0.1                            |
|   quantity  |     Number    |                              required, min:0                              |


4. Add `{timestamps:true}` to the Schema
5. Create the model and export it


## Part 3: Create the controller and mount it

1. Create a controller folder and in the folder create a product.controller.js
2. Import the model here and also import the router from express and export it at the bottom of the file. (If you don't remember the exact syntax refer to your project 2)
3. Mount the controller in your app.js on `/products`


## Part 4: Creating the core endpoints

Now that we have created the model and controller file it's time to build our endpoints. Remember to test every single route after creating it in the controllers file

### POST /create

1. Create the POST route for creating a new product here. This endpoint should take in the data for a new Product in the requests body and create a new product in the database if it passes the validation
2. Make sure to send back the status of `201` when the product is created
3. wrap all your routes in `try catch` and send back the error message for now
4. Test your route in postman. Below is a sample body you can use:

```json
{
  "title": "Wireless Keyboard",
  "description": "Bluetooth mechanical keyboard",
  "category": "Electronics",
  "price": 49.99,
  "quantity": 20
}
```


### GET /products

1. Now create the GET route for getting all the products from the database
2. This route should return all the products from the database as `JSON`
3. Test this route on postman


#### GET /products/:id

1. Create the route for 1 product. When a request is sent to `/products/:id` the product with this id should be fetched and returned as a response
2. Test this route on Postman


### PUT /products/:id
1. Create a `PUT` route that recieves a request at `/products/:id` and updates the product with this id based on the request body
2. Test this route in postman


### DELETE /products/:id
1. Create a `DELETE` route that recieves a request at `/products/:id` and deletes the product with this id
2. Test this route in postman



## Bonus 1: Statistics Endpoints

1. Add 2 more endpoints: `/low-stock` and `/statistics`
2. The `/low-stock` endpoint should return an array of objects of all the items that are `quantity` below 3
3. For the `/statistics` endpoint return something like this:
```json
{
  "totalProducts": 82,
  "totalValue": 54343,
  "lowStockItems": 5
}
```



## Bonus 2: Add API Tests with Supertest

1. Install Supertest and jest as dev dependancies:

```bash
npm install --save-dev supertest jest
```

Create tests that verify:

* POST creates a product.
* GET returns products.
* PUT updates a product.
* DELETE removes a product.

Your tests should confirm your API works correctly without manually using Postman.

---

## Bonus 3: Add GitHub Actions CI Testing

Create a GitHub Actions workflow that automatically runs your test suite whenever code is pushed.

1. Create a `.github` folder and inside it create a `workflows` folder.
2. In this folder create a `ci.yaml` file and add the following inside:

```yaml
name: Run Tests

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    env:
      MONGODB_URI: ${{ secrets.MONGODB_URI }}

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - run: npm install

      - run: npm test
```
