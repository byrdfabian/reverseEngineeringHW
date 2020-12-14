# ReverseEngineeringAuthentication
## Unit 14 Sequelize: Reverse Engineering Code
_The following folders are contained within the Develop directory_
***
#### ***config*** -- Contains the following files:
1. *middleware* contains:
- *isAuthenticated.js* - Contains a function that will be used as middleware in our html-routes file, this function has 3 parameters - the third parameter being the function that will be called by `next()` if the user is logged in, otherwise, the user is redirected to the login page.
2. *config.json* - Contains properties for the development, test, and production environments.
3. *passport.js* - The models folder is required within this file and Local Strategy is used so that our user can sign in with a username or email and a password. The npm password package is used to authenticate requests. There is validation within this file for username, email, and password usage.

#### ***models*** -- Contains the following files:
- *index.js* - Created by sequelize cli - makes it easier for us to require our models by putting model information in a db object that is put in modules.exports - this allows us to access all our models by requiring just the directory this file is in, models. We are using dotenv so that we do not share our database login credentials - which is then required in the server.js file. 

- *user.js* - Creates our user model so that we can store user information within the database. We are using the bcrypt npm package to hash our users password to protect it before it is stored in the database.

*example of a hashed password*
![hashedpassword](hshdPsswrdEx.png)

#### ***public*** -- Contains the following files:
1.  *js* contains:
- *login.js* - Validation for email/password that is entered by the user takes place in this file. We have a loginUser function which does a `POST` to a api/login route and redirects us to the members page.
- *members.js* - Contains a `GET` request for the user that is logged in and updates their page accordingly.
- *signup.js* - For sign-up we validate that the email/password is not blank. We have a `POST` for the signup route which redirects us to the members page.

2. *stylesheets* contains:
- *style.css* - We have some CSS styling for the margin of our forms.
3. *login.html* - Presents us with a login form for email address and password, a login button that takes the user to their member page or a "sign up here" link that takes the user to the sign-up page.
4. *members.html* - Presents a members page for the user that logged in and contains a "logout" button that takes the user to the login page.
5. *signup.html* - Presents us with a sign-up form with email address and password input areas, a signup button that takes the user to their member page or a "login here" link that directs the user to the login page.

#### ***routes*** -- Contains the following files:
- *api-routes.js* - We are requiring our models and passport. Using the passport.authenticate middleware with our local strategy. We have a `POST` route if the user has valid login credentials and send them to the members page. And a `POST` route for signing up a new user, if the user is created successfully they will be redirected to the login page to sign in. We have two different `GET` routes to log user out and redirect to the home page and/or to send back the users info without their password.

- *html-routes.js* - This file has routes that take the user to a login page, signup page, and members page. If the user has an account we direct them to the members page in a `GET` routes. We require our *isAuthenticated* middleware in this file. We have another `GET` route for our *isAuthenticated* middleware, if the user is not logged in and tries to access this route they will be redirected to the signup page. The *isAuthenticated* middleware is not used for the login or signup pages.


#### ***package.json*** -- Contains the metadata for our application, the dependencies for our application - which makes it easier for other developers to quickly install the same versions of these dependencies, and provides script tags that make it easier to run our code.

#### ***package-lock.json*** -- This is automatically generated for any operations where npm modifies the node_modules tree, or package.json. This is used to lock dependencies to a specific version number.

#### ***server.js*** -- Sets up our server to listen to requests from the client. Our port is set up and we require our models for sync. This file requires express session to keep track of our users login status. We require our api and html routes and sync our database.

---
 Changes I would add:

The members.js file is missing a catch for error handling if there is a problem with the request route.
