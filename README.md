﻿# URL Shortener
#### Video Demo: https://youtu.be/O8ob7kqvlsc
#### Introduction:

To conclude my CS50 course I made my very own flask website. The website allows the user to register for an account and create a short link that redirects to a longer url submitted by the aforementioned user. The website uses a few core technologies: html and tailwind/css for the front-end and flask for the back-end.


> [!IMPORTANT]
Please, do not use this code in production or use real passwords if you decide to test by yourself!




## Documentation:

## Backend

### [`app.py`](/app.py)

This is where the logic of the website resides. It has two main functions: 

- The first is to register/login users
- The second is to shorten urls and store them 

The user management is handled by the Flask_login, flask_slqalchemy, flask_wtf, flask_wtforms and flask_bcrypt libraries. When the user creates an account, a password hash is automatically created and stored in a sqlite database. The standard secret key is set to "testsecretkey". I recommand changing this value if you plan on using this program.

The user is obligated to log into the site in order to shorten urls.

After the user logs in, he is redirected to the dashboard page by the render_html function. There the user can input a long url in the form and press the submit button. The backend takes the url and assigns a code to it, storing both values.

When the url: http://"server-ip / domain"/code is accessed, the server will redirect the user to the long url that corresponds with that particular code, if it exists. This is achived with the following lines of code:

```
@app.route("/<short_url>")
def redirect_url(short_url):
    long_url = shortened_urls.get(short_url)
    if long_url:
        return redirect(long_url)
    else:
        return "URL not found", 404

```

### database.db

The database.db file is created automatically when you run the code. It is used to store the usernames and the password hashes.

## Frontend


### [`output.css`](/static/css/output.css)

This file was automatically created by the tailwind configuration. It stores the css styles used in the html code.

### [`home.html`](/templates/home.html)

This is the first page the user sees upon entering the website. It gives the user the option to either log in or register.

### [`login.html`](/templates/login.html)

This is the login page. It gives the user the option to either log in with their username and password or go to the register page.

### [`register.html`](/templates/register.html)

This is the register page. It gives the user the option to either register with their username and password or go to the log in page.

### [`dashboard.html`](/templates/dashboard.html)

This is the dashboard page. It is the page where the user is redirected after succesfully logging in. It gives the user a form to complete in order to shorten an url. It aditionally has a button for logging out.


## Possible Imporvements

There are multiple things that could be improved in the future with this project.

- The redirect links could be stored in a database. They are currently stored in a variable, wich gets erased when the server reboots.
- A guest mode, in wich users can shorten urls without having to be logged in, would be usefull for those who want to use our service for one time only.
- The redirect links could be assigned to the users that created them in a relational database.
- Users should get the option to access all the links they have created and delete or modify them from their dashboard.
- Aditionally more security can be added to the site, specifically forcing the users to use an email when registering and completing a capcha, using a better account manager etc.


