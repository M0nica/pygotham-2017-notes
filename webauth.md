### Web Authentication in Python

- Speaker: Randall Degges

- Speaker Notes: 
	- [https://speakerdeck.com/rdegges](https://speakerdeck.com/rdegges)
	- [https://speakerdeck.com/rdegges/almost-everything-you-ever-wanted-to-know-about-web-authentication-in-python](https://speakerdeck.com/rdegges/almost-everything-you-ever-wanted-to-know-about-web-authentication-in-python)


#### 0x00 - Getting Set Up

- Python
- MongoDB or another database for e.g., Postgres
- Flask

Install dependencies:

`pip install flask`

- Create Flask application with templates for login/register, home and dashboard.
- Create views in `server.py` and define which functions are run when users land on a specific url.

#### 0x01 - Forms
- HTML post forms; the data should be captured 
- methods=['GET', 'POST']
	- The default is to only process get request, this tells Flask to run URL specific commads on post requests as well 

#### 0x02 - Database/Storing data
create database (or get one that already exists)
`use test` creates database named test and switches into ti
`show collections;` shows all of the existing tables

`db.users.insert({email: "monica@aboutmonica.com", password: "woot!"});` inserting data into mongo db

`pip install flask-pymongo` use this package to handle connecting the Flask application to MongoDB database [https://flask-pymongo.readthedocs.io/en/latest](https://flask-pymongo.readthedocs.io/en/latest/)

Example:

```from flask import Flask
from flask_pymongo import PyMongo

app = Flask(__name__)
mongo = PyMongo(app)
```

Once a user enters their information, run a command to push them into the database and then redirect them to the dashboard page.

**How do we actually authenticate users?**

- use a similar method for login page, use `mongo.db.users.find_one({'email': request.form['email']} ## pseudocode after this line
if user password is the same as the password in mongodb then you should redirect/log them in!`

Sessions on the web -

- Cookies are the mechanism to remember sessions, this allows users to remain authenticated as they go from page to page on a website. 

HTTP Requests/Responses

HTTP Requests have:

- headers

Cookies are metadata about a request:
` {Set-Cookie: sessions=12345}`


Flask has a built in session object to set cookies and retrieve them.

`from flask import session`

`app.config['SECRET_KEY'] = 'SUPER_SECRET!` this line is helpful for session security - crypographic sign in

`session['id'] = str(user['_id')` the session cookie is set to equal the same as the randomly generated id for that user so that it can be used later to allow users to sign in 


In order to prevent people from accessing dashboard:
- if there are no cookies set then force the user to login (Redirect them to login screen)
-  if there are cookies, search by id to return the user object
-  then if the user login exists then let them view the dashboard!  

#### Passwords
- Password Hashing! 
- Potential hashing techniques to user for passwords:
	- bcrpyt, scrpyt, argon2
	- bcrpyt has been well tested and the go-to safe option


bcrpyt 
`pip install bcrypt passlib`
`from passlib.hash import bcrpyt`
convert the user data to a dictionary and then store new user information with password hashed. 

The login has to be updated to use bcrypyt.verify to compare the user entered password to the password stored in the mongodb database for the user

#### Security best practices 
- always use SSL (required for authentication)
- cookie flags 
- app.config['SESSION_COOKIE_HTTPONLY'] = true [don't let javascript access cookies
-should set how long are cookies accessible
- should only allow cookies to be set in https only  