# 55-9 Implement Register & Social Login feature

⬅️ [Module 55](../Module-55.md)

> START

- [ ] said something about login, register kinda stuff that i shall complete that
- [ ] made the `register.jsx` page
- [ ] added path in the router `/register`
- [ ] copied the `register` jsx from daisyUI and did some what-nots to make it look reasonable
- [ ] added Google login button on the register page
- [ ] gone to the `Sign in with Google` of `Firebase docs`
- [ ] now we will work on `Google Provider` in the `AuthProvider.jsx` file

```jsx
// src/contexts/AuthProvider.jsx
import React, { useEffect, useState } from "react";
import { AuthContext } from "./AuthContext";
import {
  createUserWithEmailAndPassword,
  signInWithEmailAndPassword,
  onAuthStateChanged,
  GoogleAuthProvider, // 1. import provider
  signInWithPopup, // 4. import fucntion
} from "firebase/auth";
import { auth } from "./firebase.init";

// 2. Create Provider
const googleProvider = new GoogleAuthProvider();

const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  const createUser = (email, password) => {
    setLoading(true);
    return createUserWithEmailAndPassword(auth, email, password);
  };

  const singInUser = (email, password) => {
    setLoading(true);
    return signInWithEmailAndPassword(auth, email, password);
  };

  // 3. Create the Google Sing-In fucntion
  const signInWithGoogle = () => {
    setLoading(true); // 5. set loading to true
    return signInWithPopup(auth, googleProvider); // 6. return this
  };

  useEffect(() => {
    const unsubscribe = onAuthStateChanged(auth, (currentUser) => {
      setUser(currentUser);
      setLoading(false);
    });

    return () => {
      unsubscribe();
    };
  }, []);

  const authInfo = {
    createUser,
    singInUser,
    signInWithGoogle, // 7. provide it for later usecase
    user,
    loading,
  };

  return <AuthContext value={authInfo}>{children}</AuthContext>;
};

export default AuthProvider;
```

---

- [ ] Import that shit in in the `Register.jsx` page. (this is probably it for google login thing)

```jsx
import React, { use } from "react";
import { AuthContext } from "@/contexts/AuthContext"; // 1. Import the context

const Register = () => {
  const { signInWithGoogle } = use(AuthContext); // 2. import needed things from the context
  // 3. create a google login button onclick handler
  const handleGoogleButtonCick = () => {
    // 4. if in confusion
    // head to Docs:
    // https://firebase.google.com/docs/auth/web/google-signin#handle_the_sign-in_flow_with_the_firebase_sdk
    signInWithGoogle()
      .then((result) => {
        console.log(result);
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

---

- [ ] something
- [ ] something
- [ ] something

> END

## Navigation

⬅️ [Video-08](./Video-08.md)
➡️ [Video-10](./Video-10.md)
