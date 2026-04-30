# 55-10 Module Summary & Save user data on database

⬅️ [Module 55](../Module-55.md)

> START

**Backend Stuff**

- [ ] Create A `Users Collection` in the `smart deals` db.

```js
const usersCollection = db.collection("users");
```

- [ ] Create `Post /users`

```js
app.post("/user", async () => {
  const newUser = req.body;
  const result = await usersCollection.inserOne(newUser);
  res.send(result);
});
```

---

**Frontend Stuff**

- [ ] Go to the Register page where you just made the 

> END

## Navigation

⬅️ [Video-09](./Video-09.md)
➡️ [Video-01](./Video-01.md)
