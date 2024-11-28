# Role based authentication

Authentication service made for ExpressJS and MongoDB using JWT. We tried to make it as clean and structured as possible. We also provide this documentation on how to install and integrate it with your own application.

> The code uses MongoDB, in case you are using another database there are few changes that has to be made to the configuration and the routes.
>
> > **It is also not final and always open for reviews and enhancements, especially when it comes to security**

## Installation

```js
$ git clone https://github.com/ShaktiCodes/RBAC.git
$ cd role-based-auth
$ npm install
```

After installing the required packages

- Browse to .env file and setup your mongo link, Secret and token
  expiration duration

```js
DB=[mongodb_link]

SECRET=[32_bits_or_more_complex_secret]

TOKEN_EXPIRATION=[token_expiration_time_in_hours]
```

- Browse to http://localhost:3000/api to check if everything is working fine
- Signup and Login endpoints start from http://localhost:3000/api/auth

> User:
>
> > http://localhost:3000/api/auth/signup
> > http://localhost:3000/api/auth/login

> Other roles: {admin, superadmin}
>
> > http://localhost:3000/api/auth/signup-[role]
> > http://localhost:3000/api/auth/login-[role]

## Structure

- It is preferred to add new feature folder inside controllers folder
- It is preferred to add role folder that exports all routes of that custom role

```
─── Controllers
	└─── auth
	│     └─── register
	│     └─── login
	|     └─── validate
	└─── feature 2 [you can add your own controller]
	└─── feature 3
─── Config
	└─── index.js [it takes configuration from .env]
	└─── roles.js [You add more roles here ]
─── Middlewares
	│
─── Models [It has only User Model]
	│
─── Routes
	│   └─── auth [It has all signup and login routes]
	│   └─── admin [All routes for admin]
	|	└─── [custom role 1]
	|	└─── [custom role 2]
	└─────── index.js [import all routes here]

```

The route takes 2 functions

- userAuth from Passport package
- CheckRole that does the role verification

```
router.get("/profile", userAuth, checkRole([ROLE.user]), async (req, res) => {
	res.status(200).json({ type: ROLE.user, user: serializeUser(req.user) });
});
```

## Packages

All thanks goes to these packages that made role-based authentication possible.\
[Mongoose](https://www.npmjs.com/package/mongoose) : Object modeling tool for MongoDB\
[Passport and passport-jwt](https://www.npmjs.com/package/passport) : Authentication middleware for ExpressJS using strategies plugins like (passport-jwt)\
[jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) : An implementation of JSON Web Tokens\
[joi](https://www.npmjs.com/package/joi): Description language for object schema and data validation\
[consola](https://www.npmjs.com/package/consola): Elegant Console Logger for Node.js\
[bcryptjs](https://www.npmjs.com/package/bcryptjs): Password encryption and decription library\

