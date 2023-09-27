### API Documentation

We will start our project by first documenting all of the routes and data models for our API. Following best practices we will use _verbs_ to specify the type of operation being done and _nouns_ when naming endpoints.

#### Routes

##### Project pages routes

| HTTP verb | URL                        | Request body | Action                        |
| --------- | -------------------------- | ------------ | ----------------------------- |
| GET       | `/`                        | (empty)      | Returns home page             |
| GET       | `/about`                   | (empty)      | Returns about page            |
| GET       | `/register`                | (empty)      | Returns register page         |
| GET       | `/login`                   | (empty)      | Returns login page            |
| GET       | `/logout`                  | (empty)      | Logout user                   |
| GET       | `/contact`                 | (empty)      | Returns contact page          |
| POST      | `/contact`                 | (empty)      | Send email (*)                |

(*) It sends email with nodemailer. Before using, email and password should be added.


##### Photo routes

| HTTP verb | URL                  | Request body | Action                     |
| --------- | -------------------- | ------------ | -------------------------- |
| POST      | `/photo`             | JSON         | Adds a new photo           |
| GET       | `/photo`             | (empty)      | Returns all photos         |
| GET       | `/photo/:id`         | (empty)      | Returns a photo by id      |
| DELETE    | `/photo/:id`         | (empty)      | Delete a photo by id       |
| PUT       | `/photo/:id`         | JSON         | Update a photo by id       |



##### User routes

| HTTP verb | URL                   | Request Headers                 | Request Body                  |
| --------- | --------------        | ------------------------------- | -------------------------     |
| POST      | `/users/register`     | --                              | { email, password, username}  |
| POST      | `/users/login`        | --                              | { email, password }           |
| GET       | `/users/dashboard`    | Authorization: \< JWT \>        | --                            |
| GET       | `/users`              | Authorization: \< JWT \>        | --                            |
| GET       | `/users/:id  `        | Authorization: \< JWT \>        | --                            |
| PUT       | `/users/:id/follow`   | Authorization: \< JWT \>        | {user._id}                    |
| GET       | `/users/:id/unfollow` | Authorization: \< JWT \>        | {user._id}                    |

<hr>

#### Models

##### Photo Model

```js
{
    name: { type: String, required:true, trim:true },
    description: { type: String, required:true, trim:true },
    uploadedAt: { type: Date, default: Date.now },
    user: { type: Schema.Types.ObjectId, ref: 'User' },
    url: { type: String, required: true },
    image_id : { type: String }
}
```

##### User Model

```js
{
  email: { type: String, unique: true, required: true },
  password: { type: String, required: true },
  username: { type: String, required: true },
  image : { type: String },
  followers: [ { type: Schema.Types.ObjectId, ref: "User" } ],
  followings: [ { type: Schema.Types.ObjectId, ref: "User" } ]
}
```