# 55-5 use Query to get products by email and explain bids collection

⬅️ [Module 55](../Module-55.md)

> START

- [ ] in this video we will work on the `My Products` pages `API` level logic building.
- [ ] for getting products of a specific user, we will add a `query parameter` which is basically `https://api.something.com/v1/products?email=someone@something.com`
- [ ] you can access the `query` by using:

```js
const email = req.query.email;
```

- [ ] so in the `API` we access the `req.query`, after that we will create an `empty query object` and put the email if there is a `req.query.email`.

```js
app.get("/products", async (req, res) => {
  // create an empty query object
  const query = {};
  const email = req.query.email;

  // inject the email into the query object
  if (email) {
    query.email = email;
  }

  // hit the database with the query
  // usually an empty query inside the .find() method will bring out all the items/documents
  const result = await productsCollection.find(query).toArray();

  // finally we will send it to the client
  res.send(result);
});
```

- [ ] Now we will move onto the `My Bids` Page logic on the `API` level

| Field           | Type         | Description                 |
| --------------- | ------------ | --------------------------- |
| `_id`           | ObjectId     | Unique bid ID               |
| `product`       | ObjectId     | Reference to `Products._id` |
| `buyer_image`   | String (URL) | Buyer’s profile pic         |
| `buyer_name`    | String       | Buyer’s name                |
| `buyer_contact` | String       | Buyer’s phone               |
| `buyer_email`   | String       | Buyer’s email               |
| `bid_price`     | Number       | Offer amount                |
| `status`        | String       | `pending` / `confirmed`     |

- [ ] understand the concept of primary key and foreign key and then go and push some data on the `Bids collection`

> END

## Navigation

⬅️ [Video-04](./Video-04.md)
➡️ [Video-06](./Video-06.md)
