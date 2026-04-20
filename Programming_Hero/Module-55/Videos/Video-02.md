# Module 55 Video 2

⬅️ [Module 55](../Module-55.md)

> START

- [ ] Goto mongodb atlas > log into your account
- [ ] setup mongodb on the api
- [ ] get the username, password and set a role of the user
- [ ] go to `mongodb docs > client library > Node.js > CRUD Operatoins > Insert Documents && Others...`
- [ ] create `const db = client.db("smart_db");`
- [ ] create `const productsCollection = db.collection("products");`
- [ ] create `POST /products`
- [ ] create a new `Document` aka `Product` from `req.body`
- [ ] insert the new product in the `DB`. NO SANITIZATION OR CHECK NEEDED. just blindly believe that whatever is coming is authentic
- [ ] the response of the DB insertion will be in the `res.status().json(result)`

> END

## Navigation

⬅️ [Video-01](./Video-01.md)
➡️ [Video-03](./Video-03.md)
