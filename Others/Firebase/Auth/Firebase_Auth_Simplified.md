# Firebase Auth Simplified

## Steps

- [ ] Go to firebase Console
- [ ] Create a new `Web App`
- [ ] Name it (e.g., `smart-deals`)
- [ ] Install `firebase` using: `npm i firebase` on the `UI` Project
- [ ] Copy `config` into Project
- [ ] Hide the `firebase Confidentials` using `Environment Variables`
- [ ] Go to `firebase docs` > `web` > `Get Started`
- [ ] Initialize the `Auth SDK`
- [ ] Export the `auth` varible for later usage
- [ ] Enable `Auth Providers` (e.g., `Email/password`, `Google`)

---

- [ ] Create the `AuthContext`
- [ ] Create `AuthProvider`
- [ ] Use `AuthContext` in `AuthProvider` to provide values form `Provider` instead of `AuthContext` directly
- [ ] Create the `createUserWithEmail` function to create users using `email and password`
- [ ] Pass it to the context value object
- [ ] Create `loading and user` state
- [ ] pass both to the context value object
- [ ] Create an `observer` using `useEffect` using an emtpy dependency array, make sure to add the cleanup function.
- [ ] inside the `observer`, we will check if the `Auth State` is CHANGED OR NOT. After setting user, we will make sure the `loading` state is set to `false`.
- [ ] Create `loginWithEmail` function to log in user.
- [ ] pass it to the context value object
- [ ] Create `logOutUser` function
- [ ] Pass it to the context value object

---

- [ ] Setup the `AuthProvider` on `main.tsx` file

---

- [ ] Go to `Register` Page
- [ ] Add `name` prop in each of the `input field(s)`
- [ ] create a `handleSubmit` function for the `form`
- [ ] Attach the handler on the form element using the `onSubmit` property
- [ ] Inside form `e.preventDefault()`
- [ ] Use `FormData` interface of js to extract
- [ ] Extract all the `values` of `form`
- [ ] Import the `createUserWithEmail` function from `AuthContext`
- [ ] Check if the `password` from the form and the `confirmPassword` are the same or not
- [ ] Call the `CreateUserWithEmail` function with the `email` and `password` after checking

> Now you can Create the `User`. And After login that user will be automatically `Login`

---

- [ ] Go to `Header` component
- [ ] Add conditional `Login/Logout` Button based on `User` from `Context`
- [ ] Go to `Login.tsx` page
- [ ] Place `name` prop on all `Input` Fields
- [ ] Create `Handler` for `form submission`
- [ ] Inside form `e.preventDefault()`
- [ ] Use `FormData` interface of js to extract
- [ ] Extract all the `values` of `form`
- [ ] Import the `loginWithEmail` function from `AuthContext`
- [ ] Call the `loginWithEmail` function with the `email` and `password`

> Now `User` can log in with the `email` && `password`

---

- [ ] Inside `Observer`, when user logs in, extract information from `currentUser` in an Object called `userData`
- [ ] Do a `POST /users` with `userData` on `body` of the request
- [ ] `API` will sync user on `userCollection` and send a response on the `Client` 

---

> Open API Code

- [ ] Create a `POST /users` route to receive Firebase user data from frontend.
- [ ] Store `req.body` into a variable: `const user = req.body;`
- [ ] Create a query object using the Firebase UID: `const query = { firebase_uid: user.firebase_uid, };`
- [ ] Use `findOne()` to search MongoDB for existing user: `const existingUser = await userCollection.findOne(query);`
- [ ] Check if user does not exist: `if (!existingUser)`
- [ ] Insert new user into MongoDB using: `insertOne();`
- [ ] Copy all frontend user properties using: `...user`
- [ ] Add account creation timestamp: `created_at: new Date();`
- [ ] Add current login timestamp: `last_login: new Date();`
- [ ] Send success response for new user: `{ success: true, isNewUser: true, }`
- [ ] If user already exists, skip `insertOne()`.
- [ ] Use `updateOne()` to update existing user: `updateOne();`
- [ ] Use `$set` to update only specific field: `$set: { last_login: new Date() }`
- [ ] Send success response for returning user: `{ success: true, isNewUser: false, }`
- [ ] Frontend should call this route every time Firebase login succeeds.

---

- [ ] add proper `async/await` login logic
- [ ] same for `DeleteAccountButton` logic

---

- [ ] Add `PrivatePage` logic without `non stateful redirection`.
- [ ] make every Secure page actually secure with `PrivatePage` Component.

---

- [ ] UI: remove `syncUserToDB` function. its for the old mental model. we are gonna create the user at `signIn` time and update user data when user data is updated at `updateUserData` function call
- [ ] UI: create an `axios` instance named `api` and export it form `@/lib/api.ts` with 10 second timeout and Base url baked in. Use this api instance instead of raw axios
- [ ] instead of syncing user on each `authStateChanged`, we will manually sync it after `creating` user, `updating` user && `deleting` user moments.
- [ ] after login, there will be a `api.post("/users", {})` basically same api call as when user gets created moment api call.
---

- [ ] API: create the `POST /users`, `PATCH /users`, `DELETE /users` route
- [ ] API: create `POST /users` where users will be created on `SingIn` time.
- [ ] API: create `DELETE /users` where users will be deleted at Delete button pressed

---

- [ ] create google login button with full login and other stuffs such as creting user in db, updating and other stuffs when a user logs into the system and do with his account.
- [ ] then go for other ui level and api level logics. fix all the user related problems
- [ ] API: create a `GET /users/firebase/:uid` for just to check if the user is in the db or not.
- [ ] UI: google login button flow will be: `Firebase login first` then `Check DB using Firebase UID`... `Create user only if missing`