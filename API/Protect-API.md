# Protect API

⬅️ [API](./API.md)

## Mental Model

```js
// let's say the perosn is here to get his own profile data

// 🚶 Person arrives at border
personArrives()

// STEP-1: Ask for passport (token)
if (person.hasNoPassport) {
  reject("401 Unauthorized - No passport")
}

// STEP-2: Border officer checks passport authenticity
try {
  passportData = borderOfficer.verifyPassport(person.passport)
} catch {
  reject("401 Unauthorized - Fake or invalid passport")
}

// STEP-3: Check if passport is expired
if (passportData.isExpired) {
  reject("401 Unauthorized - Passport expired")
}

// At this point:
// Person is REAL and IDENTIFIED
// passportData contains: { email, uid }

// STEP-4: Ask what data they want
requestedIdentity = person.requestedEmail
if (requestedIdentity is missing) {
  reject("400 Bad Request - No target specified")
}

// STEP-5: Check ownership (CRITICAL)
if (passportData.email !== requestedIdentity) {
  reject("403 Forbidden - Trying to access someone else's data")
}

// STEP-6: Access granted
allowAccess("Here is your data")
```

| Analogy           | Real Code                  |
| ----------------- | -------------------------- |
| passport          | JWT token                  |
| border officer    | Firebase Admin SDK         |
| passportData      | decoded token (`req.user`) |
| requestedIdentity | `req.query.email`          |
| allowAccess       | `res.send(data)`           |

## Code Example

```js
// ==========================
// 🔧 SETUP (server start)
// ==========================

const express = require("express");
const admin = require("firebase-admin");

const app = express();

// (Assume Firebase Admin already initialized with service account)

// ==========================
// 🛂 MIDDLEWARE: verifyToken
// ==========================
// Purpose:
// 1. Extract token from request header
// 2. Verify token using Firebase Admin SDK
// 3. Attach decoded user to req
// 4. Pass control to next step

const verifyToken = async (req, res, next) => {
  console.log("👉 Middleware started");

  // Step 1: Get Authorization header
  const authHeader = req.headers.authorization;

  // Example header:
  // Authorization: Bearer eyJhbGciOi...

  if (!authHeader) {
    console.log("❌ No Authorization header");
    return res.status(401).send("Unauthorized");
  }

  // Step 2: Extract token
  const token = authHeader.split(" ")[1];

  if (!token) {
    console.log("❌ No token found");
    return res.status(401).send("Unauthorized");
  }

  try {
    // Step 3: Verify token with Firebase
    const decoded = await admin.auth().verifyIdToken(token);

    // Example decoded:
    // {
    //   uid: "abc123",
    //   email: "sakif@email.com"
    // }

    console.log("✅ Token verified:", decoded.email);

    // Step 4: Attach user info to request
    // 🔥 THIS is where req.user is created
    req.user = decoded;

    // Step 5: Pass control to next function (route handler)
    next();
  } catch (error) {
    console.log("❌ Token invalid or expired");
    return res.status(401).send("Unauthorized");
  }
};

// ==========================
// 🔐 ROUTE HANDLER
// ==========================
// Purpose:
// 1. Read requested data info (email from query)
// 2. Compare with verified user (req.user)
// 3. Allow or deny access

app.get("/user-data", verifyToken, (req, res) => {
  console.log("👉 Route handler started");

  // Step 6: Get requested email from query
  const requestedEmail = req.query.email;

  // Example request:
  // GET /user-data?email=sakif@email.com

  if (!requestedEmail) {
    console.log("❌ No email provided in query");
    return res.status(400).send("Bad Request");
  }

  console.log("Token email:", req.user.email);
  console.log("Requested email:", requestedEmail);

  // Step 7: Authorization check (VERY IMPORTANT)
  if (req.user.email !== requestedEmail) {
    console.log("❌ Forbidden: trying to access чужой data");
    return res.status(403).send("Forbidden");
  }

  // Step 8: If everything is valid → send data
  console.log("✅ Access granted");

  const fakeUserData = {
    email: requestedEmail,
    data: "Sensitive user data here",
  };

  res.send(fakeUserData);
});

// ==========================
// 🚀 SERVER START
// ==========================

app.listen(3000, () => {
  console.log("Server running on port 3000");
});

// ==========================
// 🎬 WHAT HAPPENS ON REQUEST
// ==========================

// 1. Client sends request:
// GET /user-data?email=sakif@email.com
// Authorization: Bearer <token>

// 2. Express receives request → passes to verifyToken

// 3. verifyToken:
//    - extracts token
//    - verifies with Firebase
//    - attaches req.user
//    - calls next()

// 4. next() → moves to route handler

// 5. Route handler:
//    - reads req.user (from middleware)
//    - reads req.query.email (from request)
//    - compares both

// 6. If match → send data
//    If not → 403 Forbidden

// ==========================
// 🧠 CORE IDEA (burn this in)
// ==========================

// Authentication (middleware):
// 👉 "Who are you?"

// Authorization (route):
// 👉 "Are you allowed to access this?"

// req.user exists ONLY because:
// 👉 middleware added it

// next() is REQUIRED because:
// 👉 it moves request forward

// Without next():
// 💀 request will hang forever
```
