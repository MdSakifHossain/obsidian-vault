# Ask AI

so, i have a logger function which logs in the console. i know, logging in the production is like a bad thing. it causes resource. but im a really new dev on this world of web dev. i am making an api.

```js
// logger.js

const padZero = (num, size = 2) => num.toString().padStart(size, "0");
export function getLogTime() {
  const now = new Date();
  const day = padZero(now.getDate());
  const month = padZero(now.getMonth() + 1);
  const year = now.getFullYear();
  const hours = padZero(now.getHours());
  const minutes = padZero(now.getMinutes());
  const seconds = padZero(now.getSeconds());

  return `[${day}-${month}-${year} ${hours}:${minutes}:${seconds}]`;
}

const isDev = process.env.NODE_ENV !== "production";
const logger = (...args) => isDev && console.log(`${getLogTime()} `, ...args);
export default logger;
```

```js
// index.js
import "dotenv/config";
import express from "express";
import cors from "cors";
import { MongoClient, ObjectId, ServerApiVersion } from "mongodb";
import logger from "./lib/logger.js";

const app = express();
const port = process.env.PORT || 3000;

app.use(cors());
app.use(express.json());

const uri = process.env.MONGO_URI;

const client = new MongoClient(uri, {
  serverApi: {
    version: ServerApiVersion.v1,
    strict: true,
    deprecationErrors: true,
  },
});

async function run() {
  try {
    await client.connect();
    logger("Connected to MongoDB");

    const db = client.db("smart_deals_db");
    const userCollection = db.collection("users");
    const productCollection = db.collection("products");
    const bidCollection = db.collection("bids");

    // ========================================================================
    // ---  USERS  ------------------------------------------------------------
    // ========================================================================

    /**
     *  POST /users
     * */
    app.post("/users", async (req, res) => {
      logger("POST /users");
      const user = req.body;

      const query = {
        firebase_uid: user.firebase_uid,
      };

      const existingUser = await userCollection.findOne(query);

      if (!existingUser) {
        const reult = await userCollection.insertOne({
          ...user,
          created_at: new Date(),
          last_login: new Date(),
        });

        return res.json({
          success: true,
          message: "Account Created Successfully",
          isNewUser: true,
        });
      }

      // returning user - just update last_login
      const result = await userCollection.updateOne(
        query, // which to update
        // what to update
        {
          $set: {
            last_login: new Date(),
          },
        },
      );

      res.json({
        success: true,
        message: "Welcome back User",
        isNewUser: false,
      });
    });

    /**
     *  GET /users
     * */
    app.get("/users", async (req, res) => {
      const query = {};
      const result = await userCollection.find(query).toArray();
      res.json(result);
    });

    /**
     *  GET /users/:id
     * */
    app.get("/users/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: new ObjectId(id) };
      const result = await userCollection.findOne(query);
      res.json(result);
    });

    /**
     *  DELETE /users/:id
     * */
    app.delete("/users/:id", async (req, res) => {
      const firebase_uid = req.params.id;
      const query = { firebase_uid };
      const result = await userCollection.deleteOne(query);
      res.json({ success: true, message: "Account Deleted Successfully" });
    });

    // ========================================================================
    // ---  PRODUCTS  ---------------------------------------------------------
    // ========================================================================

    /**
     *  POST /products
     * */
    app.post("/products", async (req, res) => {
      const newProduct = req.body;
      const result = await productCollection.insertOne(newProduct);
      res.json(result);
    });

    /**
     *  DELETE /products/:id
     * */
    app.delete("/products/:id", async (req, res) => {
      const id = req.params.id;
      const query = {
        _id: new ObjectId(id),
      };
      const result = await productCollection.deleteOne(query);
      res.json(result);
    });

    /**
     *  PATCH /products/:id
     * */
    app.patch("/products/:id", async (req, res) => {
      const id = req.params.id;
      const docFromBody = req.body;
      const query = {
        _id: new ObjectId(id),
      };
      const updatedDoc = {
        $set: docFromBody,
      };
      const result = await productCollection.updateOne(query, updatedDoc);
      res.json(result);
    });

    /**
     *  GET /products
     * */
    app.get("/products", async (req, res) => {
      const query = {};
      const result = await productCollection.find(query).toArray();
      res.json(result);
    });

    /**
     *  GET /products/:id
     * */
    app.get("/products/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: new ObjectId(id) };
      const result = await productCollection.findOne(query);
      res.json(result);
    });

    // ========================================================================
    // ---  BIDS  -------------------------------------------------------------
    // ========================================================================

    /**
     * POST /bids
     * */
    app.post("/bids", async (req, res) => {
      const newBid = req.body;
      const result = await bidCollection.insertOne(newBid);
      res.json(result);
    });
  } finally {
    // await client.close();
  }
}
run().catch(console.dir);

app.listen(port, () => {
  logger(`It's alive on port: ${port}`);
});
```

i know its just the starting. but i was wondering that, this logger will run. but it will not run. since it will just run but not log, and i was willing to be this thing on each line for the dev environment. i mean the essential. e.g., "id synced", "db error", or something like that. so, i was wondering that if theres a better way that it will not run. not even the checking. just not run. i know its nothing as a new dev. but i know that computers are expensive. and im wasting this resource which technically im using. i guess im not good enough to explain but you might understand. am i wondering that if i can just reduce the amount of carbon footprint? also, this is form a newly made web devs mind. so, am i wondering too much or im thinking in a good but overengineered way? that i can just make it work as i want in the development environment and no logging except the error loggin in the production. also, error loggin is a good thing? also i know that i have to make this login a little more good. every kinda edge cases will be cover once ill be a little more of a senior dev. but for now i guess `console.error()` is something i want. also, lets go with the main problem in my head. is this a kinda problem a seniro dev have to think about? what would a senior dev do if he faces this perticular problem?

Be full descriptive in one big huge response so that one response will be ok for me.
i was wondering a full future proof solution. maybe this solution will be added into the codebase but i guess this solution is good and easy to comprehend for me as a newly self made dev.
