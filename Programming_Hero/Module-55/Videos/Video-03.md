# 55-3 Recap CRUD API for delete, update , get products

⬅️ [Module 55](../Module-55.md)

> START

- [ ] Open the `DELETE /products/:id` endpoint and after getting `ID` form `req.body` and store it in the `id` variable which will be const

```js
const id = req.params.id;
```

- [ ] we will create a `query object` and inside there will be:

```js
const query = {
  _id: new ObjectId(id),
};
```

- [ ] Send a `DELETE /products/:id` Signal:

```js
const resule = await productsCollection.deleteOne(qwery);
```

- [ ] Send the result to Client:

```js
res.send(result);
```

- [ ] Create a `PATCH /products/:id` Endpoint:

```js
app.patch("/product/:id", () => {
  // ...
});
```

- [ ] extract the `id` from the `req.params.id`:

```js
const id = req.params.id;
```

- [ ] create the query so that we can identify that product:

```js
const qwery = {
  _id: new ObjectId(id),
};
```

- [ ] create the payload / the Updated Product:

```js
// Example Used:
// https://www.mongodb.com/docs/drivers/node/v6.x/crud/update/modify/#updateone---example--full-file

const updatedProduct = {
  name: "new Name", // from the req.body
  price: "new Price", // from the req.body
};

const result = await productCollection.updateOne(qwery, updatedProduct);
res.send(result);
```

- [ ] Create a `GET /product` Endpoint:

```js
app.get("/products", async (req, res) => {
  const result = await productscollection.find({}).toArray();
  res.send(result);
});
```

- [ ] Create a `GET /products/:id` Endpoint:

```js
app.get("/products/:id", async (req, res) => {
  // get the id from the body
  const id = req.params.id;

  // make the qwery
  const qwery = { _id: new ObjectId(id) };

  // options
  // we will look for the options later

  // hit the database:
  const result = await productsCollection.findOne(qwery);

  // send it to the client
  res.send(result);
});
```

## Note

_No need to Handle any sorta Errors or Validate any Madafaqing Payload from the Client_

> END

## Navigation

⬅️ [Video-02](./Video-02.md)
➡️ [Video-04](./Video-04.md)
