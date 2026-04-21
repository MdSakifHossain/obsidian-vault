# 55-4 Intro to Query , Project , limit , sort, skip

⬅️ [Module 55](../Module-55.md)

> START

- [ ] add `node_modules` onto the `.gitignore` file
- [ ] go to [smart-deals-resources](https://github.com/ProgrammingHero1/smart-deals-resources) Github, there are structures of both `products && bids collection`
- [ ] copy the `products collection` structure and then go to Chatgpt and create some fake data without the `_id` field

`Product Document` Structure:

| Field            | Type         | Description                  |
| ---------------- | ------------ | ---------------------------- |
| `_id`            | ObjectId     | Auto-generated ID            |
| `title`          | String       | Item name                    |
| `price_min`      | Number       | Minimum acceptable price     |
| `price_max`      | Number       | Maximum asking price         |
| `email`          | String       | Seller's email               |
| `category`       | String       | e.g., Electronics, Furniture |
| `created_at`     | ISODate      | Timestamp of posting         |
| `image`          | String (URL) | Item photo                   |
| `status`         | String       | `pending` / `sold`           |
| `location`       | String       | City or area                 |
| `seller_image`   | String (URL) | Seller profile pic           |
| `seller_name`    | String       | Seller’s full name           |
| `condition`      | String       | `fresh` / `used`             |
| `usage`          | String       | e.g., "6 months old"         |
| `description`    | String       | Full details                 |
| `seller_contact` | String       | Phone or contact             |

- [ ] Generate 20 data in json format and then copy/paste on the code editor and then do some `Mods` and then paste it on the database
- [ ] Open [specify-documents-to-return](https://www.mongodb.com/docs/drivers/node/current/crud/query/specify-documents-to-return/#specify-documents-to-return) under the Query area which is under the CRUD Operations option. we will 
- [ ] [specify-fields-to-return](https://www.mongodb.com/docs/drivers/node/current/crud/query/project/#specify-which-fields-to-return) this is good to check out

> END

## Navigation

⬅️ [Video-03](./Video-03.md)
➡️ [Video-05](./Video-05.md)
