<h1>
  <span class="headline">MERN Inventory Management API Lab</span>
  <span class="subhead">Setup</span>
</h1>

## Setup


1. Go to [this link](https://github.com/omarakamal/product-inventory-starter-code) to clone our starter template for this lab
2. Once you have the starter code cloned run the app using `nodemon server.js` or `npm run dev`. Notice that `npm run dev` is just a script that runs `nodemon server.js`
3. There is a `/test` route in the starter code. Open postman and test that you can send request to the running app. You should see the following in postman:

```json
{
    "message": "App Works"
}
```

---

We are building an app with the following endpoints:

|  **Endpoint** | **HTTP Method** |
|:-------------:|:---------------:|
|   /products   |       GET       |
|   /products   |       POST      |
| /products/:id |       GET       |
| /products/:id |       PUT       |
| /products/:id |      DELETE     |


