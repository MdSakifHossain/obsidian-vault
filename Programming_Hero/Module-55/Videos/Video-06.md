# 55-6 setup React, Tailwind, DaisyUI and theme Customization

⬅️ [Module 55](../Module-55.md)

> START

- [ ] Generated some `fake Bids collection data` using chatgpt and pasted onto the `bids collection` in mongodb
- [ ] add the `bids collection's` connection in the `API`

```js
const bidsCollection = db.collection("bids");
```

- [ ] Create a `GET /bids` Endpoint:

```js
app.get("/bids", async (req, res) => {
  // hit the db
  const result = await bidsCollection.find({}).toArray();

  // send the result
  res.send(result);
});
```

- [ ] add the query param check in the `GET /bids` endpoint:

```js
app.get("/bids", async (req, res) => {
  // there could be or could not be Email
  const email = req.query.email;

  // if email is there in the query, inject it to the empty query object
  const query = {};
  if (email) {
    query.buyer_email = email;
  }

  // hit the db
  const result = await bidsCollection.find(query).toArray();

  // send the result
  res.send(result);
});
```

- [ ] Create a `POST /bids` endpoint:

```js
app.post("bids", async (req, res) => {
  // information from the body
  const newBid = req.body;

  // hit the database
  const result = await bidsCollection.insertOne(newBid);

  // send it to the client
  res.send(result);
});
```

- [ ] Create a `DELETE /bids/:id` endpoint
- [ ] Create a single bid by ID, `GET /bid/:id` endpoint
- [ ] Create the UI with react, tailwind && others.

> END

## Navigation

⬅️ [Video-05](./Video-05.md)
➡️ [Video-07](./Video-07.md)
