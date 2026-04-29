# 55-8 Set up AuthContext, Provider and auth functions

⬅️ [Module 55](../Module-55.md)

> START

- [ ] Go to `Firebase Console` and then create a new project, e.g. `smart-deals`
- [ ] after the project initialize, we will click on the `+ add app` button.
- [ ] click on the `web app`. Name it `smart-deals` and click on the `Register app` Button
- [ ] install `firebase` using: `npm i firebase` on the `UI` project
- [ ] copy the config from the `web app`
- [ ] paste the config on the `src/firebase/firebase.init.js` file
- [ ] put those important keys in the `Environment Variables`
- [ ] Search for `dotenv` and do the whatnot's
- [ ] search for `firebase docs`, go to the first link, click `Authentication` under the `Build` Dropdown menu form the `Navbar`
- [ ] Search: `firebase docs` > click > Navbar > Build > Authentication > Loading... > Left Sidebar > `Web` > `Get Started` > Go to [Add and initialize the Authentication SDK](https://firebase.google.com/docs/auth/web/start#add-initialize-sdk) > Do the what-nots > also export the `auth` variable so that we can use it on other places.
- [ ] export the `Auth` variable for later use
- [ ] Go to `Firebase Console` > Open the project > Left Sidebar > Search Input > search: `auth` > click on the `Authentication` > Loading...> click on `Sign-In Method` tab.
- [ ] Enable `Email/Password` && `Google` Provider.

---

- [ ] Create `src/contexts/AuthContext.jsx` file.
- [ ] Go to react docs for [Context](https://react.dev/learn/passing-data-deeply-with-context#step-1-create-the-context) and create the context. `Note: Inital Value will be null and export the context for later usage`

```jsx
// src/contexts/AuthProvider.jsxAuthContext.jsx
import { createContext } from "react";

export const AuthContext = createContext(null);
```

- [ ] Create `src/contexts/AuthProvider.jsx` file.
- [ ] Open `AuthProvider.jsx` file and create a Provider; basically its a file with context and its values all baked in one file which we call `Provider`

```jsx
// src/contexts/AuthProvider.jsx
import React from "react";
import { AuthContext } from "./AuthContext";

const AuthProvider = ({ children }) => {
  const authInfo = {};

  return <AuthContext value={authInfo}>{children}</AuthContext>;
};

export default AuthProvider;
```

---

- [ ] Go to `Firebase Auth Docs` > `Web` > `Password Authentication` > and setup that shit on the `AuthProvider`

```jsx
// src/contexts/AuthProvider.jsx
import React from "react";
import { AuthContext } from "./AuthContext";
import { createUserWithEmailAndPassword } from "firebase/auth"; // import this
import { auth } from "./firebase.init"; // import this

const AuthProvider = ({ children }) => {
  // create this
  const createUser = (email, password) => {
    return createUserWithEmailAndPassword(auth, email, password);
  };
  const authInfo = {
    createUser, // pass it to the context value
  };

  return <AuthContext value={authInfo}>{children}</AuthContext>;
};

export default AuthProvider;
```

---

- [ ] create `loading && user` state, send it to `authInfo` && hook it into the `createUser` function.

```jsx
// src/contexts/AuthProvider.jsx
import React, { useState } from "react";
import { AuthContext } from "./AuthContext";
import { createUserWithEmailAndPassword } from "firebase/auth";
import { auth } from "./firebase.init";

const AuthProvider = ({ children }) => {
  // 1. create these states
  const [user, setUser] = useState(null); // 2. by default user will be null;
  const [loading, setLoading] = useState(true); // 3. by default loading state will be true;

  const createUser = (email, password) => {
    setLoading(true); // 6. set loading to true; later when we make state observer then we wil make it false;
    return createUserWithEmailAndPassword(auth, email, password);
  };

  const authInfo = {
    createUser,
    user, // 4. send user state;
    loading, // 5. send loading state;
  };

  return <AuthContext value={authInfo}>{children}</AuthContext>;
};

export default AuthProvider;
```

---

- [ ] make the `SignIn/Login` function and provide the function

```jsx
// src/contexts/AuthProvider.jsx
import React, { useState } from "react";
import { AuthContext } from "./AuthContext";
import {
  createUserWithEmailAndPassword,
  signInWithEmailAndPassword, // 1. import the fucntion
} from "firebase/auth";
import { auth } from "./firebase.init";

const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  const createUser = (email, password) => {
    setLoading(true);
    return createUserWithEmailAndPassword(auth, email, password);
  };

  // 2. Create SignIn Function it will
  const SingInUser = (email, password) => {
    setLoading(true); // 3. set loading to true;
    return signInWithEmailAndPassword(auth, email, password);
  };

  const authInfo = {
    createUser,
    SingInUser, // 4. provide the function for later use;
    user,
    loading,
  };

  return <AuthContext value={authInfo}>{children}</AuthContext>;
};

export default AuthProvider;
```

---

- [ ] something else
- [ ] something else
- [ ] something else

> END

## Navigation

⬅️ [Video-07](./Video-07.md)
➡️ [Video-09](./Video-09.md)
