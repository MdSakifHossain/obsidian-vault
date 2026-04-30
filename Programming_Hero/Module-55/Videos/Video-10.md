# 55-10 Module Summary & Save user data on database

⬅️ [Module 55](../Module-55.md)

> START

**Backend Stuff**

- [ ] Create A `Users Collection` in the `smart deals` db.

```js
const usersCollection = db.collection("users");
```

- [ ] Create `POST /users` Endpoint:

```js
app.post("/user", async () => {
  const newUser = req.body;
  const result = await usersCollection.inserOne(newUser);
  res.send(result);
});
```

---

**Frontend Stuff**

- [ ] Go to the Register page where you just made the `HangleGoogleSignIn` function.

```jsx
import React, { use } from "react";
import { AuthContext } from "@/contexts/AuthContext";

const Register = () => {
  const { signInWithGoogle } = use(AuthContext);
  const handleGoogleButtonCick = () => {
    signInWithGoogle()
      .then((result) => {
        console.log(result);

        // 1. Crete new user variable
        const newUser = {
          name: result.user.displayName,
          email: result.user.email,
          image: result.user.photoURL,
        };

        // 2. Create user in the DB
        // Fetch Start
        fetch("api-url/users", {
          method: "POST",
          headers: {
            "content-type": "application/json",
          },
          body: JSON.stringify(newUser),
        })
          .then((res) => res.json())
          .then((data) => {
            console.log("data after new user save", data);
          });
        // FETCH Completed.
      })
      .catch((err) => {
        console.log(err);
      });
  };

  return (
    <div>
      <p>Register Page...</p>
    </div>
  );
};

export default Register;
```

**Backend Stuff:**

- [ ] With newly made code which is just gonna post on each google login. we will make it a little smart.
- [ ] Open the API File.
- [ ] How do we check the duplicate stuff before actually sending the save signal?

```js
app.post("/user", async () => {
  const newUser = req.body;

  const email = req.body.email; // 1. get the email address
  const query = { email: email }; // 2. make the query with which we will find out with it later
  const existingUser = usersCollection.findOne(query); // 3. get the value if the user is there or not

  if (existingUser) {
    res.send("User Already Exists. No need to insert again!");
  } else {
    const result = await usersCollection.inserOne(newUser);
    res.send(result);
  }
});
```

- [ ] something...

> END

## Navigation

⬅️ [Video-09](./Video-09.md)
➡️ [Video-01](./Video-01.md)
