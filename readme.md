# Encrypted User Model Lab

## Introduction

> ***Note:*** _This can be a pair programming activity or done independently._

We've covered `bcrypt` a few ago weeks with Sinatra and just learned about how to do this in an Node/Express app.  Let's, now, try to reproduce the same logic of password encryption, again.  This lab is only about implementing bcrypt in your server logic, so we do not expect any views or front end implementation - the code should just respond with different HTTP statuses and JSON response to handle all the cases.

In the starter code provided, add code to handle two routes - the first one to create a user (where the password will be encrypted) and the second to authenticate users based on an email and a password.

## Exercise

#### Requirements

- Create a user model with these attributes:
  - Name(String)
  - Email(String) (Unique and required)
  - Password(String)

- The app should have these two routes: `/users` and `/users/authenticate`

- `/users` route should expect params like the ones below; if the params are valid, then a user document should be saved and the password encrypted.

  ```javascript
  // `/users` params
  "user": {
    "name"        : "gerry",
    "email"       : "gerry@ga.co",
    "password"    : "sfgdsfpassword"
  }
  ```

- `/users/authenticate` route should expect a user object like the one below; if the params are valid, then a verification of the password passed in params should be performed against the encrypted and a message should be sent back as a response with the result, authenticated or not.

  ```javascript
  // `/users/authenticate` params
  "user": {
    "email"       : "gerry@ga.co",
    "password"    : "sfgdsfpassword"
  }
  ```

- All routes must respond with a JSON object like this:

  ```javascript
  {message: "XXXXXX"}
  ```

- The HTTP response status must be either:
  - `200` if the request params are valid and all the process in the route has been executed as expected
  - `401` if the request params are wrong and/or something wrong happened on the server side

**Bonus:**
- Add extra validation
- Give detailed messages for when the params are incorrect

#### Starter code

Please find the starter code with all the file structure and all the packages required in every file.

The file `app.js` contains Middleware to handle errors and the config to `decode` the JSON received in the body.

#### Deliverable

Take a look at some cURL commands to try for each route:

- For a valid user creation request:

  ```bash
  curl -i -H "Content-Type: application/json" -d '{
    "user": {
      "name"        : "Garry"
      "email"       : "gerry@ga.co",
      "password"    : "password"
    }
  }' http://localhost:3000/users/authenticate
  ```

- For a valid user authentication request:

  ```bash
  curl -i -H "Content-Type: application/json" -d '{
    "user": {
      "email"       : "gerry@ga.co",
      "password"    : "password"
    }
  }' http://localhost:3000/users/authenticate
  ```


- For an invalid request user authentication (note: it's invalid because it doesn't have a password):

  ```bash
  curl -i -H "Content-Type: application/json" -d '{
    "user" :{
      "email"       : "gerry@ga.co"
    }
  }' http://localhost:3000/users/authenticate
  ```

## Additional Resources

- [Bcrypt NodeJS](https://github.com/ncb000gt/node.bcrypt.js/)
- [How Bcrypt Works](http://codahale.com/how-to-safely-store-a-password/)
