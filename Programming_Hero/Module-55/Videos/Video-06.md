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
  
})
```

- [ ] asdf
- [ ] asdf
- [ ] asdf

> END

## Navigation

⬅️ [Video-05](./Video-05.md)
➡️ [Video-07](./Video-07.md)
